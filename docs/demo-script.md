# 🎬 Hackathon Video Demo Script (2.5 - 3 Minutes)

This script provides a second-by-second guide for recording your submission demo video.

*   **Presenter**: Sanskar (or split between Sanskar, Ansh, and Krishna)
*   **Recording Tool**: OBS Studio, Loom, or Screenity.
*   **Resolution**: 1080p, Full Screen, Browser open at `localhost:8000` (or your live hosted URL).

---

## ⏱️ Video Chronology

### 0:00 - 0:25 | The Intro & Problem Statement
*   **Action on Screen**: Start on the Dashboard homepage. Show a clean empty workspace dashboard (zeros showing, no populated files except the two default clean notes).
*   **Voiceover**:
    *   *“Hi judges! Today we are showing you the Smart College AI Assistant, a focused workspace built for students to convert flat study notes into interactive personal study systems. We solved the problem of fragmented study resources. Instead of searching through folders, students upload their notes here and get instant revision tools.”*

### 0:25 - 0:55 | Note-Grounded Q&A (The RAG Engine)
*   **Action on Screen**: Click on **Study** next to the `Chemical_Bonding_Study_Notes.pdf`. The workspace shifts to the chat panel. 
*   **Voiceover**:
    *   *“Let’s select our Chemical Bonding notes. Our system splits this note into semantic chunks with overlap. When we ask a doubt, it performs a local TF-IDF similarity query to retrieve matching paragraphs, ensuring the AI answer is 100% grounded in the text.”*
*   **Action on Screen**: Type: *"What constitute an ionic bond?"* and hit Enter. Show the answer returning with page citation `(Page 1 (Chemical_Bonding_Study_Notes.pdf))`.

### 0:55 - 1:30 | Voice-to-Voice Multimodal Assistant
*   **Action on Screen**: Click the **Microphone** icon. It will flash red. 
*   **Voiceover**:
    *   *“We’ve integrated a browser-native Voice-to-Voice Assistant. Watch as I ask a doubt hands-free.”*
*   **Action on Screen**: Speak clearly: *"How do covalent bonds differ from ionic compounds?"*. 
*   **Action on Screen**: The speech recognizer will print the text and automatically send it. Once the reply is generated, click the **speaker icon** on the AI reply to let the judges hear the text-to-speech reading the answer.
*   **Voiceover**:
    *   *“The system transcribes my speech, submits the query, and allows us to vocalize the response for auditory learners.”*

### 1:30 - 2:00 | Active Recall (3D Flashcards)
*   **Action on Screen**: Click on **Revision Flashcards** in the sidebar. The generated cards will load. 
*   **Voiceover**:
    *   *“To reinforce what we studied, our system generates flashcards compiled from key terms in the notes. We can read them out loud using the voice synthesizer, and flip them in 3D to check our knowledge.”*
*   **Action on Screen**: Click the speaker icon on a flashcard front face, then click the card to flip it in 3D. Do it for 1 or 2 cards.

### 2:00 - 2:30 | Self-Assessment (Interactive Practice Quiz)
*   **Action on Screen**: Click on **Practice Quiz** in the sidebar. 
*   **Voiceover**:
    *   *“Finally, we can test our comprehension with generated multiple-choice quizzes. It validates our choices instantly and reveals AI-generated explanations for incorrect selections.”*
*   **Action on Screen**: Choose a correct answer (green highlight), select an incorrect option on another question (red highlight with slide-down AI explanation). Click **Finish Quiz** to view the final scorecard.

### 2:30 - 3:00 | Dashboard Progress & Conclusion
*   **Action on Screen**: Navigate back to **Dashboard** in the sidebar. Show that "Doubts Solved", "Revision Flashcards Seen", and "Average Quiz Score" stats have all updated dynamically based on your actions.
*   **Voiceover**:
    *   *“Back on the dashboard, our metrics tracker shows exactly what we have revised and how we performed. Smart College AI Assistant is a zero-dependency, private, and highly interactive learning companion. Thank you judges!”*
