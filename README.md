# NVIDIA Parakeet TDT 0.6B v3 (GGUF) - 25 European Languages

Welcome to the GitHub homepage for the **GGUF** version of NVIDIA's flagship **parakeet-tdt-0.6b-v3** multilingual Automatic Speech Recognition (ASR) model.

🚀 **[DOWNLOAD THE 2.3GB MODEL FROM HUGGING FACE HERE](https://huggingface.co/Singla0009/Parakeet-TDT-0.6B-Multilingual-GGUF)** 🚀

---

⚡ **Powered by CAPIT** ⚡  
These highly-optimized `.gguf` models were explicitly designed and converted to be used seamlessly with **CAPIT**, our blazing-fast, privacy-first desktop transcription application. CAPIT is a state-of-the-art Rust & Tauri native app built by our team that lets you run these massive AI models entirely offline on your local machine with an incredible user interface.  
👉 **[Check out the CAPIT App on our GitHub!](https://github.com/singla0009)**

---
This model was converted directly from the official NeMo PyTorch checkpoints and is designed to be run locally with zero Python dependencies using the lightweight C++ C-API (`parakeet.cpp`) and the `ggml` execution engine.

> [!IMPORTANT]
> **CRITICAL EXECUTION REQUIREMENT:**
> This model utilizes NVIDIA's advanced Token-and-Duration Transducer (TDT) architecture. 
> To run this model in `parakeet-cli`, you **MUST** specify the `--decoder tdt` flag. It will crash or hallucinate if you use the standard CTC decoder.

## Supported Languages (Automatic Detection)
One of the most powerful features of this model is **automatic language detection**. You do not need to prompt it with a specific language; it will dynamically detect and transcribe any of the following 25 languages:

*   **English** (en)
*   **French** (fr)
*   **Spanish** (es)
*   **German** (de)
*   **Italian** (it)
*   **Portuguese** (pt)
*   **Russian** (ru)
*   **Ukrainian** (uk)
*   **Polish** (pl)
*   **Dutch** (nl)
*   **Greek** (el)
*   **Swedish** (sv)
*   **Finnish** (fi)
*   **Danish** (da)
*   **Romanian** (ro)
*   **Bulgarian** (bg)
*   **Croatian** (hr)
*   **Czech** (cs)
*   **Estonian** (et)
*   **Hungarian** (hu)
*   **Latvian** (lv)
*   **Lithuanian** (lt)
*   **Maltese** (mt)
*   **Slovak** (sk)
*   **Slovenian** (sl)

---

## Local Performance & Hardware Requirements

Based on local testing with `ggml` (CUDA offloading), here are the exact hardware requirements for this 600-million parameter model in its unquantized `f32` (Float32) state:

*   **Model File Size:** ~2.3 GB
*   **System RAM Peak (CPU Memory):** ~2.8 GB (for memory mapping)
*   **VRAM Peak (GPU Memory):** ~2.6 GB

> [!TIP]
> **Low VRAM Footprint:** Because of GGML optimizations, this massive multilingual model runs comfortably on consumer GPUs, leaving over 13GB+ free on a standard 16GB RTX card while transcribing at blazing speeds.

---

## Technical Details: What is TDT?

Unlike standard CTC (Connectionist Temporal Classification) or RNNT decoders, the **Token-and-Duration Transducer (TDT)** is a novel architecture invented by NVIDIA. 

Instead of just predicting the next word, TDT models predict **two things simultaneously**:
1. The text token itself.
2. The exact duration (in milliseconds) that the token spans in the audio.

By doing both at once, it allows the model to "skip" forward in the audio timeline, making transcription significantly faster and more accurate across varying speech tempos.

---

## Usage Instructions

To run this model, you need the **parakeet-cli** C++ execution engine.

1. Go to the [parakeet.cpp GitHub Repository](https://github.com/PABannier/parakeet.cpp).
2. Follow their build instructions to compile the `parakeet-cli` executable for your specific operating system (Windows/Linux/macOS).
3. Once compiled, open your terminal and run the model using the following command:

### Transcribing Audio (Auto-Language Detection)
```bash
parakeet-cli transcribe --model parakeet-tdt-0.6b-v3.f32.gguf --input audio.wav --decoder tdt
```
