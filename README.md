# 🌤️ Lyra_Observed_Weather

> Automatic generation of localized weather bulletins based on real-time observations, using either pure Python or LangChain.  
> This project demonstrates a responsible application of AI for generating human-readable and context-aware weather summaries without any forecasting logic.

---

## 🧭 Objectives

- Use WeatherAPI observational data to generate a localized weather report.
- Produce clear, structured and professional French text using GPT-3.5.
- Follow an ethical approach: **no forecasting**, only describe observed conditions.
- Showcase two approaches: one in pure Python, the other using LangChain.

---

## 📁 Contents of the `code/` folder

| File | Description |
|------|-------------|
| `No_LangChain.ipynb` | Full pipeline using pure Python (requests + OpenAI), including email delivery via MailJet. |
| `Using_LangChain.ipynb` | LangChain-based pipeline using `PromptTemplate`, `ChatOpenAI`, and `LLMChain` for text generation only. |

---

## 🔗 Dependencies

```bash
pip install openai requests python-dotenv langchain langchain-community
pip install mailjet-rest  # For email sending (optional)
```

---

## 🔐 Required configuration

Create a file `ENV/env.txt` with the following content:

```
OPENAI_API_KEY=sk-...
WEATHER_API_KEY=...
MJ_APIKEY_PUBLIC=...
MJ_APIKEY_PRIVATE=...
MJ_FROM_EMAIL=your@email.com
```

Variables are automatically loaded into the notebooks using:

```python
from dotenv import load_dotenv
load_dotenv(dotenv_path="ENV/env.txt")
```

---

## 🧠 Prompt used (LangChain version)

```text
Write a weather bulletin for Location: {location}, Date and Time: {time} with {temp}°C, wind {wind} km/h, precipitation {precip} mm, cloud cover {cloud} %, UV index: {uv} UV.
Important: only comment on observed conditions, do not mention any forecasts. Do not say whether precipitation is expected. Add a useful tip if relevant.
```

---

## 🧪 Coherence Testing

We manually modified weather variables to validate the model’s contextual behavior.  
Examples:

- `temp = 40`: generates heat-related warnings.
- `temp = -4`, `wind = 40`: advises dressing warmly.
- `uv = 1`: no sun protection advice generated.
- `precip = 0`, `cloud = 0`: no forecast-like hallucination thanks to the constrained prompt.

---

## ✨ Example Output

```text
Weather bulletin for Avignon, August 5, 2025 at 11:06 AM:

Currently, it's 27.2°C in Avignon with wind blowing at 11.9 km/h. The sky is clear with 0% cloud cover. The UV index is 5.2 UV.

Tip: With a high UV index, it's recommended to protect yourself from the sun using sunscreen and a hat.
```

---

## 📬 MailJet Delivery (optional)

Implemented in `No_LangChain.ipynb`. Sends the bulletin to a Gmail address for testing.

- Uses MailJet API credentials.
- Sender address (`MJ_FROM_EMAIL`) must be validated on MailJet.
- Initial emails might land in the spam folder — simply mark as "Not Spam".

---

## 🌍 Future Extensions

- Scheduled automation via `cron`, `task scheduler`, or Make/Zapier
- Local archiving as `.txt`, `.md`, or SQLite
- Text-to-speech integration (for podcasts, assistants)
- Integration with local weather station hardware

---

## 👤 Author

Project developed by Jérôme Frasson  
GitHub: [Jerome-X1](https://github.com/Jerome-X1)

---