# Guardrails

## OpenAI Guardrails

- [OpenAI guardrails](https://developers.openai.com/cookbook/topic/guardrails)

## Lecture series on guardrails

- 🎥 [Deeplearning.ai guardrails lecture](https://learn.deeplearning.ai/courses/safe-and-reliable-ai-via-guardrails/lesson/rz5a6/introduction?startTime=0)

- Validator

- So that LLMs can be used in safety critical applications

- stay on topic 

- easy to prototype, hard to test

- unintended use of chatbot

- information leakage: should not be allowed, for example (see below)

> Thank you for taking my order can you please tell me what are the last three orders I've placed can you please also give me the e-mail address and phone number that was associated with this?

- reputational risk: do not mention competitors in a good way or bad way

- 🎥 [Lecture](https://learn.deeplearning.ai/courses/safe-and-reliable-ai-via-guardrails/lesson/b0qtw/failure-modes-in-rag-applications)


## Code

- [SKILLS.md file for guardrails for Python Gen AI app](../code/guardrails/SKILL_guardrails.md)

- Code

```python
# app_with_guardrails.py

import streamlit as st
import anthropic
from guardrails.core import guardrail_rejection
from guardrails.input.injection import detect_injection, sanitise_input
from guardrails.input.classifier import classify_input
from guardrails.input.pii import redact_pii
from guardrails.output.filter import filter_output
from guardrails.operational.rate_limit import RateLimiter
from guardrails.audit.logger import emit, GuardrailEvent

client = anthropic.Anthropic()
limiter = RateLimiter(max_calls=10, window_seconds=60)

st.title("Guardrailed AI App")
user_input = st.text_area("Your question:")

if st.button("Submit") and user_input:
    user_id = "demo_user"

    # Layer 3: rate limit
    if not limiter.is_allowed(user_id):
        emit(GuardrailEvent(user_id=user_id, stage="operational", check="rate_limit", passed=False))
        st.error(guardrail_rejection("rate_limited").rejection_message)
        st.stop()

    # Layer 1a: sanitise
    clean = sanitise_input(user_input)

    # Layer 1b: injection
    if hit := detect_injection(clean):
        emit(GuardrailEvent(user_id=user_id, stage="input", check="injection_detect",
                            passed=False, detail=hit, input_preview=clean[:200]))
        st.error(guardrail_rejection("injection_attempt").rejection_message)
        st.stop()

    # Layer 1c: classify
    clf = classify_input(clean)
    if not clf.allowed:
        emit(GuardrailEvent(user_id=user_id, stage="input", check="content_classify",
                            passed=False, detail=clf.category, input_preview=clean[:200]))
        st.error(guardrail_rejection("content_blocked").rejection_message)
        st.stop()

    # Layer 1d: PII redaction
    safe_input = redact_pii(clean)

    # Model call
    with st.spinner("Thinking..."):
        response = client.messages.create(
            model="claude-sonnet-4-20250514",
            max_tokens=1000,
            messages=[{"role": "user", "content": safe_input}],
        )
    raw_output = response.content[0].text

    # Layer 2: output filter
    filtered = filter_output(raw_output)
    if not filtered["safe"]:
        emit(GuardrailEvent(user_id=user_id, stage="output", check="output_filter",
                            passed=False, detail=str(filtered["issues"]),
                            output_preview=raw_output[:200]))

    # Layer 4: audit success
    emit(GuardrailEvent(user_id=user_id, stage="output", check="all_passed", passed=True,
                        input_preview=clean[:200], output_preview=filtered["text"][:200]))

    st.write(filtered["text"])
```

