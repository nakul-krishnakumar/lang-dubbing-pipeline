# 🎙️ Video Dubbing Pipeline (English to Malayalam)
---

## Dubbing workflow / pipeline
![pipeline-design](image.png)

---

This repository outlines a complete pipeline for automatically dubbing English videos into Malayalam using a combination of state-of-the-art APIs and models for audio processing, transcription, translation, and synthesis.

---

## 🧩 Workflow Overview

This pipeline takes an English input video and produces a Malayalam dubbed output video with preserved background music. Here's the detailed step-by-step flow:

### 📥 Input

* **Input**: English Video File (`.mp4`, `.mov`, etc.)

---

## ⚙️ Processing Pipeline

1. **Extract Audio from Video**

   * Tool: `ffmpeg`
   * Output: `input_audio.wav` and `muted_input_video.mp4`

2. **Separate Audio into Vocals & BGM**

   * Tool: [`Spleeter`](https://github.com/deezer/spleeter) (2 stems)
   * Output:

     * `vocals.wav` (speech)
     * `accompaniment.wav` (background music)

3. **Transcribe English Speech**

   * API: [AssemblyAI API](https://www.assemblyai.com/)
   * (Optionally use Sarvam Batch API)
   * Output: English text chunks

4. **Text Preprocessing (Optional)**

   * Combine or chunk transcriptions if necessary

5. **Translate to Malayalam**

   * API: [Sarvam Mayura API](https://sarvam.ai/)
   * Input: English Text
   * Output: Malayalam Text

6. **Generate Malayalam Speech Audio**

   * Model: **Sarvam Bulbul\:v2**
   * Input: Malayalam Text
   * Output: `malayalam_audio.wav`

7. **Merge Dubbed Audio + Background Music**

   * Tool: `ffmpeg`
   * Input: `malayalam_audio.wav` + `accompaniment.wav`
   * Output: Combined dubbed audio

8. **Generate Dubbed Output Video**

   * Tool: `ffmpeg`
   * Input: `muted_input_video.mp4` + Combined audio
   * Output: Final dubbed video in Malayalam

---

## 📦 APIs & Tools Used

| Tool/API                          | Purpose                                |
| --------------------------------- | -------------------------------------- |
| **ffmpeg**                        | Audio/video extraction & recombination |
| **Spleeter**                      | Audio source separation                |
| **AssemblyAI**                    | Speech-to-text transcription           |
| **Sarvam Mayura API**             | English → Malayalam translation        |
| **Sarvam Bulbul\:v2**             | Malayalam text-to-speech synthesis     |
| **Sarvam Batch API** *(optional)* | Alternate transcription source         |

---

## 📂 Output

* `final_output_video.mp4` – Final Malayalam-dubbed video

---

