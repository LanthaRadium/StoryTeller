# AI Storyteller — Proof of Concept / Demo

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)](#)
[![UI](https://img.shields.io/badge/UI-Gradio-informational)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **NOTICE**  
> This repository will continue to evolve based on feedback gathered during my bachelor’s thesis interviews (teachers, researchers, and software engineers).  
> Planned upgrades include improved validation, UX refinements for children (ages 5–8), and more modular audio controls. See **Roadmap** below.

A modular, end-to-end **AI storytelling application** that generates short children’s stories, narrates them with TTS, and layers background music. Built as a research-driven demo to explore **promptable, swappable components** in an AI pipeline.

---

## Highlights (Portfolio Summary)

- ✨ **Metadata-driven prompts:** users choose **setting**, **characters**, and **themes**
- 🧠 **LLM story generation:** Llama 3.1 with a **three-act structure**
- ✅ **Quality gate:** readability & word-count checks (TextStat), basic safety filtering
- 🔊 **Narration:** MeloTTS voice generation
- 🎵 **Music:** MusicGen-Small background loops per scene
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
  combine_audio.py      # merge narration + music with gain controls
data/
  frontend_metadata.json
  prompts/              # story + music prompt templates
doc/
  steps.txt
  summary.txt
generated/              # (gitignored) outputs
  stories/              # .txt
  narrations/           # .wav/.mp3
  music/                # .wav/.mp3
  final_audio/          # mixed outputs
licenses/
  llama3_1_license.txt
  melotts_license.txt
  musicgen_license.txt
tests/                  # optional test scripts (gitignored)
```

---

## Requirements

- **Python 3.10+**
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

# 4) (optional) fetch local model with Ollama
# ollama pull llama3.1

# 5) run the app
python app/app.py
```

Open the URL printed in the terminal (default `http://127.0.0.1:7860`) and:
1) choose setting/characters/themes, 2) click **Create your custom story!**, 3) listen & export.

---

## Configuration

Most switches live in **`app/config.py`**.

Optional `.env` example:

```
# .env
STORY_MODEL=llama3.1
USE_OLLAMA=true
MUSIC_MODEL=facebook/musicgen-small
OUTPUT_DIR=generated
READABILITY_TARGET=grade_3
MUSIC_GAIN_DB=-12
```

- **Models**: swap LLM, TTS, or music backends without touching the UI code  
- **Audio**: set narration/music sample rates and mix levels  
- **Validation**: adjust readability targets and restricted-word filters

---

## Validation & Testing

- **Readability** with TextStat (Flesch, grade level) targeting ages **5–8**  
- **Simple safety filters** for restricted words  
- Optional tests (place in `tests/`):

```bash
pytest -q
```

---

## Screenshots / Demo

- Add a UI screenshot at `doc/ui.png` and reference it here:
  
```
![Gradio UI](doc/ui.png)
```

- (Optional) short GIF demo of the story flow

---

## Roadmap (Next Iterations Informed by Interviews)

- [ ] **UX**: clearer child-friendly controls, preset “story packs”
- [ ] **Validation**: richer checks (age-level vocabulary, theme consistency)
- [ ] **Audio**: multi-scene timelines, smoother transitions, per-scene volume ramps
- [ ] **Export**: storybook PDF with images + QR to audio
- [ ] **Languages**: extend beyond English; simple accent & voice presets
- [ ] **Modularity**: adapter layer for alternative LLMs/TTS/music engines

---

## Troubleshooting

- **No audio in final mix** → ensure `ffmpeg` is installed (`ffmpeg -version`)
- **Very slow generation** → use smaller models, shorten story length, enable CUDA
- **Music overpowers narration** → lower `MUSIC_GAIN_DB` in `combine_audio.py`
- **TTS/model import errors** → check versions in `requirements.txt` and reinstall in a fresh venv

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

This proof of concept was developed as part of my bachelor thesis on **modular AI pipelines for educational storytelling**.  
Thanks to mentors and interview participants for insights on readability, pedagogy, and UX.

---

## About the Author

**Lara Mestdagh** — AI Engineer  
- GitHub: https://github.com/LanthaRadium  
- LinkedIn: https://www.linkedin.com/in/<your-profile>
