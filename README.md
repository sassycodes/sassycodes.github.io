# 🎥 AI Video Generator (n8n Powered)

**A full-stack, AI-powered video generation pipeline orchestrating LLMs, Image-to-Video models, and Cloud Editing APIs to turn simple text prompts into complete, narrated videos.**

[**View Frontend Demo**](https://sassycodes.github.io)

---

## 🚀 Vision

The goal of this project is to democratize video production. We aim to create a seamless web experience where users can generate professional-grade videos with synchronized audio simply by typing a linear text prompt. By abstracting complex AI interactions behind a simple UI, we solve the problem of slow and expensive video production for content creators and agencies.

---

## ⚙️ System Architecture

The core of this application is a sophisticated **No-Code Backend** built on **n8n**. The workflow handles the logic, asset generation, and media stitching.

![n8n Workflow Visualization](517527286-70a65efe-6b13-4ada-916a-71e63ffd75b7.png)

### The Workflow Explained

Our n8n pipeline executes the following distinct stages:

1.  **Input & Scripting:**
    * The workflow receives a raw user idea.
    * **Gemini API** acts as a "World-Class Direct Response Video Director" to generate a structured script using the PAS (Problem, Agitation, Solution) or AIDA framework.
2.  **Structural Parsing:**
    * A secondary system prompt converts the script into a strict JSON object containing:
        * `voiceover_text`: ~60 words for a 30-second spot.
        * `prompt_part_1`, `prompt_part_2`, `prompt_part_3`: Detailed visual descriptions for 10-second segments.
3.  **Parallel Asset Generation:**
    * **Video (Visual Continuity):** We utilize **Veo 3 models** to generate video in three 10-second chunks. Crucially, we use custom JavaScript to **extract the last frame** of the previous video and feed it into the next generation step. This ensures character, setting, and lighting consistency across the entire 30-second clip.
    * **Audio (TTS):** The JSON voiceover text is sent to **Gemini TTS**, converting the output from PCM to WAV format for editing compatibility.
4.  **Final Assembly:**
    * **Shotstack API** is utilized to stitch the three video segments and the audio track together.
    * The workflow polls for render status and formats the final response for the frontend.

---

## 🛠️ Tech Stack

* **Orchestration:** [n8n](https://n8n.io/) (No-code backend)
* **LLM & Scripting:** Google Gemini API
* **Video Generation:** Veo 3 Models
* **Audio/TTS:** Gemini TTS (Generative Language API)
* **Video Editing/Stitching:** [Shotstack API](https://shotstack.io/)
* **Frontend:** HTML5, CSS3, Vanilla JavaScript (Hosted on GitHub Pages)

---

## 🧠 Prompt Engineering

The quality of our output relies on rigorous prompt engineering. Below are the core system prompts driving the agent:

<details>
<summary><strong>Click to view Script Generation Prompt</strong></summary>

```text
Act as a world-class Direct Response Video Director. I need a video ad script for the following:

Product/Service: [Insert Name]
Target Audience: [Insert Audience]
Problem Solved: [Insert Problem]
Key Benefit: [Insert Benefit]
Tone: [Insert Tone]
Platform: [Insert Platform]
Duration: [e.g., 30 seconds]

Instructions:
1. Use the PAS Framework (Problem, Agitation, Solution) or AIDA.
2. The first 3 seconds must contain a "Visual Hook".
3. Format output as a Markdown Table with columns: Time, Visual Scene, Audio/Dialogue.
4. Include a specific Call to Action (CTA).

   Our website is made we just need to setup with our backend to make it complete interactive...
Open: https://sassycodes.github.io
## About
</details>

<details> <summary><strong>Click to view JSON Structure Prompt</strong></summary>

Plaintext

You are an expert video script generator. Based on the user's video topic, generate a JSON object with exactly 4 fields: 

1. 'voiceover_text' (approx 60 words for 30s video)
2. 'prompt_part_1' (detailed visual prompt for first 10s)
3. 'prompt_part_2' (detailed visual prompt for second 10s, continuing from part 1)
4. 'prompt_part_3' (detailed visual prompt for final 10s, continuing from part 2)

Ensure visual continuity across all three parts - the same character, setting, and visual style must be maintained throughout.
</details>

💻 Frontend
The frontend is currently a lightweight, static implementation hosted via GitHub Pages.

Structure: Single index.html file containing all markup, styles, and logic.

Status: The UI is live. We are currently in the process of wiring the n8n webhook endpoints to the frontend form to enable real-time user interaction.
This site is a single `index.html` file that contains HTML, CSS and JavaScript.
