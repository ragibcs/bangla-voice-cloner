<div align="center">

# 🌍 Bangla TTS with OmniVoice

### Bangla text-to-speech, voice cloning, and voice design in Google Colab

Generate Bangla speech from text with three simple workflows—**voice cloning**, **voice design**, and **automatic voice generation**—using [OmniVoice](https://huggingface.co/k2-fsa/OmniVoice).

<p>
  <a href="https://colab.research.google.com/drive/1DNujDErwHIPBWN9YEWwseZjJF7H86aU_?usp=sharing">
    <img alt="Open in Google Colab" src="https://colab.research.google.com/assets/colab-badge.svg">
  </a>
  <a href="https://github.com/ragibcs/bangla-voice-cloner">
    <img alt="GitHub repository" src="https://img.shields.io/badge/GitHub-bangla--voice--cloner-181717?logo=github">
  </a>
  <img alt="Python" src="https://img.shields.io/badge/Python-Colab-blue?logo=python">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-green.svg">
</p>

**[🚀 Open the Colab Notebook](https://colab.research.google.com/drive/1DNujDErwHIPBWN9YEWwseZjJF7H86aU_?usp=sharing)** · **[📦 Source Repository](https://github.com/ragibcs/bangla-voice-cloner)**

</div>

---

> [!IMPORTANT]
> **Educational and research use only.** Use voice cloning only when you have the speaker’s informed consent and the necessary rights. Do not use this project for fraud, scams, impersonation, harassment, misinformation, or other unlawful or harmful activities.

## ✨ Features

| Mode | What it does | Reference audio |
|---|---|---|
| 🎙️ **Voice Cloning** | Generates Bangla speech using an authorized reference voice. | Required |
| 🎨 **Voice Design** | Generates speech from a text description of voice characteristics. | Not required |
| 🤖 **Auto Voice** | Generates speech using the model’s default voice behavior. | Not required |

Additional capabilities:

- 🇧🇩 Designed for experimenting with Bangla text-to-speech.
- 🔊 Exports generated speech as WAV audio.
- 🎚️ Adjustable speech speed and generation steps.
- 📝 Optional reference transcript to help voice cloning.
- 📥 Downloads generated audio directly from Google Colab.
- 🧩 Sentence splitting to help process longer text.
- ☁️ Runs in a hosted Colab environment without requiring a local GPU.

## 🚀 Quick Start

### 1. Open the notebook

Click the badge or use this link:

**[Open Bangla TTS in Google Colab](https://colab.research.google.com/drive/1DNujDErwHIPBWN9YEWwseZjJF7H86aU_?usp=sharing)**

### 2. Enable a GPU

In Colab, select:

`Runtime → Change runtime type → T4 GPU`

GPU availability depends on your Colab account and current resource limits.

### 3. Start with a clean runtime

If you have already run other notebooks or installed conflicting packages, select:

`Runtime → Disconnect and delete runtime`

This resets the current runtime environment. Unsaved runtime files may be lost.

### 4. Run the cells in order

- Run the installation cell **once**.
- If Colab prompts you to restart the session, restart it.
- Continue with the next cell after installation; **do not rerun the installation cell**.
- Load the model before running any generation mode.

### 5. Generate and download speech

Choose a mode, enter Bangla text, and run its cell. The notebook can create these files:

- `omnivoice_clone.wav`
- `omnivoice_design.wav`
- `omnivoice_auto.wav`

Use the notebook’s download cell to download any generated files that exist.

## 🧰 Requirements

The notebook is intended to run in **Google Colab**.

- A Google account with access to the notebook.
- A GPU runtime is recommended; a T4 GPU is suggested.
- Internet access to install the package and download the model.
- A short, clear reference recording for voice cloning.
- Permission to use the reference recording and voice.

The installation cell currently installs:

```bash
pip install -q omnivoice soundfile
```

The notebook also relies on dependencies provided by the Colab environment, including PyTorch, and uses `ffmpeg` to convert uploaded reference audio.

> [!WARNING]
> **Avoid dependency conflicts.** Do not force-reinstall `transformers`, and do not install `parler-tts` in this notebook. These changes may introduce incompatible dependency versions and break imports. If the environment becomes inconsistent, reset the runtime and run the installation cell once.

## 🎙️ How to Use Each Mode

### Voice cloning

1. Upload a clear recording of a **single speaker**, ideally around **5–15 seconds**.
2. Use audio you own or have explicit permission to use.
3. Enter the Bangla text you want to generate.
4. If available, provide the exact transcript of the reference recording in `ref_text`.
5. Adjust `speed` and `num_step` if needed, then run the cell.

The notebook converts the uploaded audio to mono, 24 kHz WAV and limits the reference clip to 15 seconds.

**Output:** `omnivoice_clone.wav`

### Voice design

Describe the desired voice in the `instruct` field—for example:

```text
female, young adult, moderate pitch
```

The generated voice may not match every requested characteristic exactly.

**Output:** `omnivoice_design.wav`

### Automatic voice generation

Enter Bangla text and run the Auto Voice cell without a reference recording or voice instruction.

**Output:** `omnivoice_auto.wav`

## 🎛️ Generation Settings

| Setting | Purpose |
|---|---|
| `text` | Bangla text to synthesize |
| `ref_audio_path` | Path to the uploaded reference audio used for cloning |
| `ref_text` | Optional transcript of the reference recording |
| `instruct` | Voice description for voice design |
| `speed` | Speech-speed control |
| `num_step` | Number of generation steps |
| `pause_between_sentences` | Pause inserted between text chunks |
| `seed` | Random seed used by the cloning workflow |

The notebook’s default output sample rate is **24 kHz**. Results can vary with the input text, reference recording, model behavior, and generation settings.

## 🗂️ Repository Structure

The core workflow is provided as a Google Colab notebook. A typical repository layout could look like this:

```text
bangla-voice-cloner/
├── README.md
├── LICENSE
└── bangla_tts_omnivoice_fixed.ipynb
```

The notebook may be stored under a different filename. Update the filename above to match the actual file committed to the repository.

## 🛠️ Troubleshooting

| Problem | Suggested fix |
|---|---|
| `transformers` import error or `PreTrainedConfig` error | Reset the runtime using **Runtime → Disconnect and delete runtime**, then run the installation cell once. |
| `NameError: name 'model' is not defined` | Run the model-loading cells successfully before the generation cell. |
| GPU not detected | Select **Runtime → Change runtime type → T4 GPU**, reconnect, and check GPU availability. |
| CUDA out-of-memory error | Restart the runtime, shorten the input text, and try `num_step` ≤ 32. |
| Poor or inconsistent cloned voice | Use a clean, single-speaker recording with minimal background noise and provide its accurate transcript in `ref_text`. |
| Reference audio conversion fails | Try a valid WAV, MP3, AAC, or M4A file and confirm that the recording can be played. |
| No output file appears | Confirm that the relevant generation cell completed successfully before running the download cell. |

## 🔐 Ethics, Consent, and Responsible Use

Voice generation can be useful for language technology research, accessibility, education, content creation, and prototyping. It can also be misused.

**Please follow these principles:**

- **Consent first:** Clone a person’s voice only with informed consent and appropriate authorization.
- **No impersonation:** Do not use generated audio to deceive listeners into believing that a real person said something they did not say.
- **No fraud or abuse:** Do not use the notebook for scams, threats, harassment, identity deception, or other harmful or illegal conduct.
- **Respect rights:** Follow applicable privacy, copyright, publicity/personality, and data-protection laws.
- **Disclose synthetic audio:** Clearly label AI-generated speech when needed to avoid misleading people.
- **Protect recordings:** Do not upload private or sensitive voice recordings unless you have the right to use them and understand the service’s data-handling terms.

## ⚖️ Disclaimer

This repository and notebook are provided **for educational and research purposes**. The repository owner and contributors do not endorse, encourage, or authorize illegal, deceptive, or abusive uses.

Users are responsible for the way they use, modify, and distribute the code and generated audio, including obtaining any required consent, licenses, and permissions. The repository owner and contributors make no guarantee that generated audio will be accurate, suitable, or lawful for a particular use. To the extent permitted by applicable law, they disclaim responsibility for misuse by users.

This project uses third-party software and a separately hosted model. **The license of this repository does not automatically apply to OmniVoice, its model weights, its dependencies, uploaded reference recordings, or generated outputs.** Review the applicable model and dependency licenses and terms before using or redistributing them.

## 📄 License

The original code and documentation in this repository are intended to be released under the **MIT License**. See [`LICENSE`](LICENSE) for the full text.

This license applies only to material that the repository owner has the right to license. It does not grant rights to third-party models, datasets, audio recordings, or other separately licensed components.

## 🙌 Acknowledgements

- [OmniVoice](https://huggingface.co/k2-fsa/OmniVoice) — speech-generation model used by the notebook.
- [Google Colab](https://colab.research.google.com/) — hosted notebook environment.
- The open-source community and researchers advancing speech technology.

## 🔗 Links

- **Colab notebook:** https://colab.research.google.com/drive/1DNujDErwHIPBWN9YEWwseZjJF7H86aU_?usp=sharing
- **GitHub repository:** https://github.com/ragibcs/bangla-voice-cloner
- **OmniVoice model:** https://huggingface.co/k2-fsa/OmniVoice

---

<div align="center">

**Built for learning. Use responsibly. Respect every voice.** 🎙️

</div>
