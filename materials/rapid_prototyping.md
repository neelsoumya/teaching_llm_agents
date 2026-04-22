# Rapid prototyping

- [Lecture on deeplearning.ai](https://learn.deeplearning.ai/courses/fast-prototyping-of-genai-apps-with-streamlit/lesson/egrcal/scoping-an-mvp)

- ⬆️📎 [Code github](https://github.com/https-deeplearning-ai/fast-prototyping-of-genai-apps-with-streamlit)

## Co-creating an MVP with GenAI

- [Lecture](https://learn.deeplearning.ai/courses/fast-prototyping-of-genai-apps-with-streamlit/lesson/i1aro4/lab-1%3A-co-creating-an-mvp-plan-with-genai)

- Use a GenAI app to prototype (turn PDF notes into clinical insight)

- Brainstorm end goal

- Who is audience? (non-technical people)

- What does the app look like?

- Features (drag and drop, export to csv, etc.)

- be specific (do not give open ended tasks to GenAI apps)

⚠️ _NOTE_

> Give the AI a role _act as a product manager_


## ⬆️📎 Tools

[Lecture](https://learn.deeplearning.ai/courses/fast-prototyping-of-genai-apps-with-streamlit/lesson/hl2zjx/setting-up-your-environment)

- Google Colab

- Streamlit

- ngrok account and auth token

- Sarvam AI API key


Optional


- Python

- Local files



## Streamlit

- [streamlit](https://streamlit.io/playground?example=charts)

- [Interactive streamlit GDP dashboard](https://github.com/neelsoumya/gdp-dashboard)

- [Deploy on _streamlit.io_](https://streamlit.io/cloud)

- Click on [_New app_](https://share.streamlit.io/new)

- [Here](https://gdp-dashboard-t19rvs9nq2m.streamlit.app/) is a deployed app

- Push your code to github and deploy

- [Course on deeplearning.ai on streamlit](https://learn.deeplearning.ai/courses/fast-prototyping-of-genai-apps-with-streamlit/lesson/79cfr0/setting-up-your-environment)

- Setup a repository in _github_

- Or run in Google _Colab_

- Run _streamlit_ using

```bash
streamlit run script.py
```

- Here is an example script

```python
import streamlit as st
import pandas as pd
import numpy as np

st.write("Streamlit supports a wide range of data visualizations")

all_users = ["Alice", "Bob", "Charly"]
with st.container(border=True):
    users = st.multiselect("Users", all_users, default=all_users)
    rolling_average = st.toggle("Rolling average")

np.random.seed(19)
data = pd.DataFrame(np.random.randn(20, len(users)), columns=users)

if rolling_average:
    data = data.rolling(7).mean().dropna()

tab1, tab2 = st.tabs(["Chart", "Dataframe"])
tab1.line_chart(data, height=250)
tab2.dataframe(data, height=250, use_container_width=True)

```

- [ngrok signup](https://dashboard.ngrok.com/signup)

- [create an auth token](https://dashboard.ngrok.com/authtokens/new)

- [Google Colab notebook](https://github.com/neelsoumya/visualization_lecture/blob/main/streamlit.ipynb)

- To save your `ngrok` authtoken securely in Google Colab, you should use Colab's **Secrets** feature. This allows you to store sensitive information like API keys or tokens without embedding them directly in your code, which is important for security and when sharing notebooks.

1.  **Open the Secrets Panel:** In the left sidebar of your Colab notebook, click on the **"🔑 Secrets"** icon (it looks like a key).
2.  **Add a new secret:** Click the **"+ Add new secret"** button.
3.  **Name the secret:** For your `ngrok` authtoken, you could name it `YOUR_AUTHTOKEN` (or any other descriptive name you prefer, but remember it for later).
4.  **Enter the secret value:** Paste your `ngrok` authtoken into the "Value" field.
5.  **Save:** Click "Save secret".

Once saved, you can access this secret in your Python code using `from google.colab import userdata` and then `userdata.get('YOUR_AUTHTOKEN')` (replacing `'YOUR_AUTHTOKEN'` with the name you gave your secret).
