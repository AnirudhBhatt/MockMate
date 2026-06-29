
# 🧠 AI-Powered Technical Interview Prepper

A full-stack application designed to simulate real-world technical interviews. It allows users to practice answering conceptual and coding questions verbally and programmatically, receiving instant, AI-driven feedback on their performance.

## ✨ Key Features

* **Customizable Interviews**: Select Role (MERN, Python, Data Science), Difficulty Level, and Interview Type (Oral vs. Coding Mix).
* **Hybrid Input System**:
* **🎙️ Voice Response**: Uses **OpenAI Whisper** to transcribe verbal answers for conceptual questions.
* **💻 Code Editor**: Integrated **Monaco Editor** for solving coding challenges directly in the browser.


* **AI Microservice Architecture**:
* **Question Generation**: dynamically creates unique interview questions using **Ollama (Mistral)**.
* **Smart Evaluation**: Analyzes both code logic and verbal transcription to provide a **Technical Score** and **Confidence Score**.


* **Detailed Analytics**:
* Session history with global scores.
* Per-question breakdown showing user submission vs. ideal implementation.
* Performance charts using **Chart.js**.


* **Secure Authentication**: JWT-based user login and registration.

---

## 🛠️ Tech Stack

### **Frontend**

* **Framework**: React (Vite)
* **State Management**: Redux Toolkit
* **Styling**: Tailwind CSS
* **Editor**: `@monaco-editor/react`
* **Visualization**: Chart.js / React-Chartjs-2
* **Routing**: React Router Dom

### **Backend (API Gateway)**

* **Runtime**: Node.js
* **Framework**: Express.js
* **Database**: MongoDB (Mongoose)
* **Authentication**: JSON Web Tokens (JWT) & bcryptjs

### **AI Microservice**

* **Runtime**: Python 3.9+
* **Framework**: FastAPI
* **LLM Engine**: Ollama (running `mistral` locally)
* **Speech-to-Text**: OpenAI Whisper (`base.en` model)
* **Audio Processing**: PyDub / FFMPEG

---

## 🚀 Getting Started

### Prerequisites

1. **Node.js** (v16+) and **npm**.
2. **Python** (v3.9+) and **pip**.
3. **MongoDB**: Local instance or Atlas URI.
4. **Ollama**: Installed and running locally.
* Install from [ollama.com](https://ollama.com).
* Pull the model: `ollama pull mistral`.


5. **FFmpeg**: Required for audio processing (should be in your system PATH).

### 1. Clone the Repository

```bash
git clone https://github.com/AnirudhBhatt/MockMate.git
cd MockMate
```

### 2. Backend Setup (Node.js)

```bash
cd backend
npm install

# Create a .env file
echo "PORT=5001" > .env
echo "MONGO_URI=your_mongodb_connection_string" >> .env
echo "JWT_SECRET=your_jwt_secret" >> .env
echo "NODE_ENV=development" >> .env

# Run the server
npm run dev
```

### 3. AI Service Setup (Python)

```bash
cd ../ai-service

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create a .env file
echo "AI_SERVICE_PORT=8000" > .env
echo "GROQ_API_KEY=your_groq_api_key" >> .env
echo "GROQ_MODEL_NAME=llama-3.3-70b-versatile" >> .env

# Run the microservice
uvicorn main:app --reload --port 8000
```

### 4. Frontend Setup (React)

```bash
cd ../frontend
npm install

# Create a .env file
echo "VITE_API_URL=http://localhost:5001/api" > .env
echo "VITE_GOOGLE_CLIENT_ID=your_google_client_id" >> .env

# Run the frontend
npm run dev
```
### or shortcut

```
CLICK ON FOR-FIRST-TIME.BAT FILE AND RUN

```
---

## 📐 Architecture Overview

The application follows a microservices-inspired architecture to separate heavy AI processing from the main application logic.

1. **Client (React)**: Handles UI, Audio Recording, and Code Editing. Sends data to Node.js.
2. **Node.js Server**: Acts as the API Gateway. Handles Auth, Database storage, and forwards AI tasks to the Python service.
3. **Python Service**:
* Receives `POST /generate-questions`.
* Receives `POST /transcribe` (Audio -> Text).
* Receives `POST /evaluate` (Text/Code -> Score/Feedback JSON).


4. **Ollama / Groq Cloud**: The LLM engine that powers the generation and evaluation logic. Locally, it can use Ollama (`mistral`); in production, it queries Groq's cloud-hosted `llama-3.3-70b-versatile` for sub-second evaluations.

---

## 🌐 Production Deployment (Hybrid Architecture)

This application is configured and deployed online using a hybrid hosting strategy:
- **Frontend**: Hosted on **Vercel** (with Vite framework preset pointing to the `frontend` root).
- **Backend (API Gateway)**: Hosted on **Render** as a Node Web Service (connected to MongoDB Atlas).
- **AI Microservice**: Hosted on **Render** as a Python Web Service (querying the Groq API).

---

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a pull request.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.