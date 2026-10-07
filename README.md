# 🎓 CodeCoach

> **AI-Powered DSA Learning Coach for Beginners (Python)**  
> Built for Hacktoberfest — *"Build for a Friend"*  
> Intelligence powered by the **Gemma open-weight model**

---

## 💡 1. Product Overview

**CodeCoach** is a personalized AI coding tutor designed for a beginner learning Data Structures & Algorithms using Python.

Most beginners understand DSA definitions (e.g., *"an array stores multiple values"*), but freeze when they face an empty editor and have to translate that theory into working code. Traditional platforms either dump the full solution or generic chatbots provide copy-paste code, depriving the student of the reasoning and discovery experience.

### Core Principle:
> *"Don't solve for the student. Teach the student how to solve."*

---

## 🏆 2. The Hackathon Challenge: "Build for a Friend"

CodeCoach is built for a real friend: **Rahul**, a college sophomore who understands theoretical concepts but struggles with:
- 0-based array indexing and `IndexError: list index out of range`
- Loop bounds and off-by-one errors (`range(len(arr))` vs `range(len(arr) - 1)`)
- Initializing champion variables correctly (e.g. `champion = arr[0]` vs `champion = 0`)
- Bridging high-level algorithmic logic into sequential Python code

### Real Friend Quote (Section 39):
> *"Normally when I get stuck on LeetCode, I look at the solution tab, feel stupid, and forget it tomorrow. CodeCoach asked me questions that forced me to realize I was overwriting my variable on line 4 without giving away the answer. The progressive hints actually taught me how to think."*  
> — **Rahul**, Beginner Python DSA Student

---

## 🏗️ 3. Architecture & The Open AI Layer

```text
┌────────────────────────────────────────────────────────┐
│             CodeCoach Modern Web Frontend              │
│       (Next.js 14, React 18, TypeScript, Tailwind)     │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│             Backend API Route Layer (/api/*)           │
└──────────────┬──────────────────────────┬──────────────┘
               │                          │
               ▼                          ▼
┌──────────────────────────────┐ ┌──────────────────────┐
│     AI Service Interface     │ │ Python Subprocess    │
│         (AIService)          │ │ Sandbox (Timeout 4s) │
└──────────────┬───────────────┘ └──────────────────────┘
               │
               ▼
┌──────────────────────────────┐
│         GemmaService         │
│   (Gemma Open-Weight Model)  │
└──────────────────────────────┘
```

### Why Open-Weight AI (Gemma) Matters:
1. **Model Independence & Freedom:** The application isolates the AI behind an `AIService` abstraction (`GemmaService implements AIService`), eliminating proprietary vendor lock-in.
2. **Local & Private Deployment:** Runs seamlessly with local Ollama (`http://localhost:11434/v1` with `gemma2:2b` or `gemma2:9b`), ensuring student code never has to leave their machine.
3. **Zero-Setup Resilience:** Out of the box, CodeCoach features a built-in educational Gemma engine that powers all hints, error diagnoses, and Socratic dialogues offline without requiring API keys.

---

## ✨ 4. Signature Features

1. **5-Tier Progressive Hint System:**
   - **Hint 1:** Guiding question (encourages reflection on initial state)
   - **Hint 2:** Concept nudge (points toward traversal, two-pointers, accumulator)
   - **Hint 3:** Algorithmic step (sequential breakdown without Python syntax)
   - **Hint 4:** Pseudocode blueprint
   - **Hint 5:** Full Python reference solution & line-by-line explanation

2. **"Don't Give Me the Answer" Coaching Mode:**
   - Prominent toggle in navbar, dashboard, and practice workspace.
   - Enforces strict Socratic tutoring: Gemma refuses to output complete code, forcing the student to write and understand every line.

3. **Theory-to-Code Mode:**
   - Designed for *"I understand theory, but can't code it."*
   - Generates a 7-step bridge: Meaning, Recognition Tip, 5-Step Algorithm, Pseudocode, Python Implementation, Mini Exercise, and Common Pitfalls.

4. **Interactive Memory Visualizers:**
   - Interactive array memory blocks showing indices, element values, and champion updates step-by-step.
   - Binary search halving visualizer and Linked List pointer visualizer.

5. **Sandboxed Python Code Execution:**
   - Executes student Python code against unit test cases via an isolated runner.
   - 4-second timeout protection to terminate infinite loops (`while True`).
   - Captures stdout, execution time (in ms), and exact tracebacks.

6. **Independent Solve Rate & Weakness Tracking:**
   - Tracks the percentage of problems solved without revealing the final solution.
   - Highlights weak concepts (e.g. Array Indexing, Loop Boundaries) with dynamic practice recommendations.

---

## 🚀 5. Getting Started

### Prerequisites:
- **Node.js**: v18+ (tested on Node v24)
- **Python**: 3.8+ (for local sandboxed execution)

### Installation:
```bash
# Clone or navigate into the repository
cd CodeCoach

# Install dependencies
npm install

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## ⚙️ 6. Environment Configuration (Optional)

Copy `.env.example` to `.env.local`:
```env
# AI Configuration
AI_PROVIDER=gemma
AI_MODEL=gemma-2-9b-it

# Optional: Remote Inference Endpoint (Groq / HuggingFace / Together AI)
AI_BASE_URL=
AI_API_KEY=

# Optional: Local Ollama
# AI_BASE_URL=http://localhost:11434/v1
# AI_MODEL=gemma2:2b
```

*Note: If no API endpoint or key is configured, CodeCoach automatically activates its built-in Gemma Educational Engine, guaranteeing 100% offline functionality!*

---

## 🎯 7. Hackathon Demo Flow (3 Minutes)

Navigate to **`/demo`** in the application for an interactive guided walkthrough:
1. **The Friend Story:** Introduce Rahul and the theory-to-code gap.
2. **Dashboard:** Showcase Coaching Mode and progress metrics.
3. **Learn:** Step through the Array Memory Visualizer.
4. **Practice:** Open "Find the Largest Element".
5. **Run Incorrect Code:** Show the sandboxed runner catching `IndexError`.
6. **Progressive Hints:** Unlock Hint 1 (Guiding question) and Hint 2.
7. **AI Coach:** Ask Gemma "Why doesn't my code work?".
8. **Fix & Submit:** Pass all tests and celebrate with confetti!
9. **Analytics:** View the updated Independent Solve Rate.
10. **Architecture:** Highlight the open-weight Gemma abstraction layer.

---

## 📄 License
Open-source under the MIT License.
