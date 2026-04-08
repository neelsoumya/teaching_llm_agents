# Multimodal

- [OpenAI multimodal](https://developers.openai.com/cookbook/topic/multimodal)

## Sarvam models

```python
import os
import tempfile
import gradio as gr
from sarvamai import SarvamAI
from sarvamai.play import save

client = SarvamAI(api_subscription_key=os.getenv("SARVAM_API_KEY"))

def process_audio(audio_file):
    # audio_file = path to uploaded/recorded audio
    
    # --- STT ---
    with open(audio_file, "rb") as f:
        stt_response = client.speech_to_text.transcribe(
            file=f,
            model="saaras:v3",
            mode="transcribe"
        )
    
    transcript = getattr(stt_response, "transcript", "")
    
    if not transcript:
        return "No speech detected", None

    # --- Simple reply ---
    reply = f"I heard: {transcript}"

    # --- TTS ---
    tts_response = client.text_to_speech.convert(
        text=reply,
        model="bulbul:v3",
        target_language_code="en-IN",
        speaker="shubh"
    )

    # Save output audio
    out_path = tempfile.mktemp(suffix=".wav")
    save(tts_response, out_path)

    return transcript, out_path


iface = gr.Interface(
    fn=process_audio,
    inputs=gr.Audio(type="filepath"),
    outputs=[
        gr.Textbox(label="Transcript"),
        gr.Audio(label="Response")
    ],
    title="Multilingual Voice Assistant (India)",
    description="Speak in any Indian language. The system will transcribe and respond."
)

if __name__ == "__main__":
    iface.launch()
```