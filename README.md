# Flow for our AI genration model 
Our Vision - 
To create a AI powered Website which gives a AI genrated video with Sound you want.
Our Execution step :- 
We have used n8n as no code backend and this is how our work flow look like - 
<img width="1706" height="269" alt="image" src="https://github.com/user-attachments/assets/70a65efe-6b13-4ada-916a-71e63ffd75b7" />

1. where First we take Input idea from user and then we use gemini api which genrates our system script :- 

// system prompt for Script genration:-  
  Act as a world-class Direct Response Video Director. I need a video ad script for the following:

  **Product/Service:** [Insert Name Here, e.g., IrisOS]
  **Target Audience:** [Insert Audience, e.g., Content Creators, Agencies]
  **Problem Solved:** [Insert Problem, e.g., Video production is too slow and expensive]
  **Key Benefit:** [Insert Benefit, e.g., Text-to-video in seconds]
  **Tone:** [Insert Tone, e.g., Cinematic, High-energy, Professional]
  **Platform:** [Insert Platform, e.g., Instagram Reel (9:16), YouTube Pre-roll (16:9)]
  **Duration:** [e.g., 15 seconds, 30 seconds]

  **Instructions:**
  1. Use the **PAS Framework** (Problem, Agitation, Solution) or **AIDA** (Attention, Interest, Desire, Action).
  2. The first 3 seconds must contain a "Visual Hook" to stop the scroll.
  3. Format the output as a **Markdown Table** with these columns:
   - **Time** (e.g., 0:00-0:03)
   - **Visual Scene** (Detailed prompt for video generation)
   - **Audio/Dialogue** (Voiceover or Text-on-Screen)
  4. Include a specific Call to Action (CTA) at the end.


2. After that there is system prompt which genrates video into 3  and seprates voice over part :- 

//You are an expert video script generator. Based on the user's video topic, generate a JSON object with exactly 4 fields: 'voiceover_text' (approximately 60 words for a 30-second video), 'prompt_part_1' (detailed visual prompt for the first 10 seconds), 'prompt_part_2' (detailed visual prompt for the second 10 seconds, continuing from part 1 with the same character/setting), and 'prompt_part_3' (detailed visual prompt for the final 10 seconds, continuing from part 2 with the same character/setting). Ensure visual continuity across all three parts - the same character, setting, and visual style must be maintained throughout. Each prompt should be highly detailed with specific descriptions of subject, action, setting, lighting, camera movement, and visual style suitable for AI video generation.



3. There we have inserted 3 veo 3 modeles which genrates 3 videos of our script seperately and that Js code helps to feed last part of video to next agent .

4. For voice or audio we have used gemini tts audio which provides us the audio

5. At the end we are using Shotstock Which stiches all the three videos with audio 

6. We are planing to host the complete working website which generates complete video with simple liner prompt

   Our website is made we just need to setup with our backend to make it complete interactive...
Open: https://sassycodes.github.io
## About
This site is a single `index.html` file that contains HTML, CSS and JavaScript.
