# AI Storyteller — Proof of Concept / Demo

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](#)
[![UI](https://img.shields.io/badge/UI-Gradio-informational)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **NOTICE**  
> This repository will continue to evolve based on feedback gathered during my bachelor’s thesis interviews.  
> Planned upgrades include improved narration, UX refinements for children (ages 5–8), and more control of the story options. See **Roadmap** below.

A modular, end-to-end **AI storytelling application** that generates short children’s stories, narrates them with TTS, and adds small music clips. Built as a research-driven demo to explore the usage of AI for creating and narrating children's stories.

---

## Highlights (Portfolio Summary)

- ✨ **Metadata-driven prompts:** users choose a **setting**, up to 3 **characters**, and a **theme**
- 🧠 **LLM story generation:** Llama 3.1 with a **three-act structure**
- ✅ **Quality gate:** readability & word-count checks (TextStat), basic safety filtering
- 🔊 **Narration:** MeloTTS voice generation
- 🎵 **Music:** MusicGen-Small music transition clips
- 🧪 **Modular by design:** each stage can be replaced independently
- 🖥️ **Gradio UI:** simple interface to run the whole pipeline

---

## Project Structure

```
app/
  app.py                # Gradio UI entrypoint
  config.py             # central config & paths
  story_gen.py          # Llama 3.1 story generation
  tts_gen.py            # MeloTTS narration
  music_gen.py          # MusicGen background music
  combine_audio.py      # merge narration + music
data/
  frontend_metadata.json
  prompts/              # story + music prompt templates
doc/
  steps.txt
  summary.txt
generated/              # (gitignored) outputs
  stories/              # .txt
  narrations/           # .wav
  music/                # .wav
  final_audio/          # mixed outputs
licenses/
  llama3_1_license.txt
  melotts_license.txt
  musicgen_license.txt
thesis/
  BachelorThesis_MCT_Lara_Mestdagh.pdf
tests/                  # optional test scripts (gitignored)
```

---

## Requirements

- **Python 3.10+**
- **Docker**
- **ffmpeg** available on PATH (for audio processing)
- (Optional) **CUDA** for faster inference with PyTorch
- Access to **Llama 3.1** (e.g., via **Ollama** or your preferred provider)

---

## Quickstart

```bash
# 1) clone & enter
git clone https://github.com/<your-username>/ai-storyteller.git
cd ai-storyteller

# 2) create & activate venv
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
# source .venv/bin/activate

# 3) install dependencies
pip install --upgrade pip
pip install -r requirements.txt

# 4) fetch local model with Ollama
ollama pull llama3.1

# 5) run the app
python app/app.py
```

Open the URL printed in the terminal (default `http://127.0.0.1:7860`) and:
1) choose setting/characters/themes, 2) click **Create your custom story!**, 3) listen & export.

---

## Screenshots / Demo

- Add a UI screenshot at `doc/ui.png` and reference it here:
  
```
![Gradio UI](doc/ui.png)
```

- (Optional) short GIF demo of the story flow

---

## Roadmap (Next Iterations Informed by Interviews)

- [ ] **Deployment**: fully dockerize the entire application 
- [ ] **Audio**: improve TTS model and final speech
- [ ] **UX**: clearer controls, dashboard for children or adults
- [ ] **Music**: option to choose if user wants music, look into continous background track

---

## Credits & Licenses

This repository is released under the **MIT License** (see [`LICENSE`](LICENSE)).

**Third-party models & licenses (not included in MIT):**
- **Llama 3.1 (Meta)** — see `licenses/llama3_1_license.txt`
- **MeloTTS** — see `licenses/melotts_license.txt`
- **MusicGen (Meta)** — see `licenses/musicgen_license.txt`

Please review and comply with each model’s license before redistribution or commercial use.

---

## Acknowledgements

This proof of concept was developed as part of my bachelor thesis on **usage of AI for children's stories creation and narration**.  
Thanks to mentors and interview participants for insights on readability, pedagogy, and UX.

---

## About the Author

**Lara Mestdagh** — AI Engineer  
- GitHub: https://github.com/LanthaRadium  
- LinkedIn: https://www.linkedin.com/in/lara-mestdagh-077385309
