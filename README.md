# Conversational Time-Coded Data Analyzer (CTDA)

[![Project Status](https://img.shields.io/badge/Project%20Status-Complete-green.svg)](https://github.com/SurajBhadavkar08/Time-Series-Driven-Conversational-Analytics-for-Understanding-Temporal-Chat-Dynamics)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](#)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![React](https://img.shields.io/badge/React-18.x-cyan.svg)](https://react.dev/)

**CTDA (Conversational Time-Coded Data Analyzer)** is a web-based conversational analytics platform developed as an undergraduate B.Tech thesis project. The application transforms unstructured messaging exports (specifically WhatsApp chat logs) into rich, interactive, time-aware visualizations and metrics that reveal individual and group-level communication rhythms, engagement balances, and emotional/sentiment dynamics.

---

## 🎓 Project Context
* **Thesis Title**: *Time-Series Driven Conversational Analytics for Understanding Temporal Chat Dynamics*
* **Department/Degree**: Bachelor of Technology (B.Tech) in Biomedical Engineering
* **Institution**: School of Engineering, Ajeenkya DY Patil University, Pune, Maharashtra, India
* **Project Members**: 
  * Sakshi Adhagale (2022-B-29032003 / 2022-B-29052003)
  * Suraj Bhadavkar (2023-B-08022005)
  * Sanika Bari (2022-B-22052004C)
* **Supervisor**: Prof. Aarti Kumari

---

## ✨ Features
CTDA adopts a staged data pipeline that parses, cleans, processes, and visualizes chat logs:

1. **Robust Preprocessing & Parsing**
   * Automatically handles different WhatsApp date/time formats (12-hour AM/PM vs. 24-hour clocks).
   * Segments text messages, sender IDs, and timestamps into structured tabular records (Pandas DataFrame).
   * Identifies and excludes system-generated notifications (e.g., encryption notices, invitation joins).
2. **Privacy & Security Shielding**
   * Employs regular expressions to detect and exclude sensitive data (such as Aadhaar card and PAN numbers) before analytics execution.
   * Operates completely **database-free** and **stateless**—all uploads are processed in-memory and discarded upon session reset.
3. **Quantitative Metrics**
   * Calculates overall message counts, total word counts, shared media counts (`<Media omitted>`), and shared hyperlinks (using `urlextract`).
4. **Temporal Time-Series Analysis**
   * Identifies busiest days, peak hours, busiest weeks, and peak months.
   * Generates continuous group timelines mapping message frequency from group inception.
5. **Conversational Balance & Engagement**
   * Visualizes participant contribution percentages to reveal engagement symmetry or asymmetry.
   * Identifies top active and quietest users.
6. **Sentiment & Linguistic Analysis**
   * Integrates the **NLTK VADER** Sentiment Analyzer to classify each message as Positive, Negative, or Neutral.
   * Visualizes daily timelines of sentiment trends, sentiment contribution per participant, day-wise sentiment distributions, and most common sentiment-aligned keywords.
7. **Interactive Dashboard**
   * Responsive UI built with Vite and Tailwind CSS.
   * Renders interactive Plots (bar charts, line graphs, pie charts, and heatmaps) using Plotly.js.
   * Dynamically generates customizable Word Clouds of the chat content.

---

## 🛠️ Technology Stack
* **Frontend**: ReactJS (v18), Vite, Tailwind CSS, Plotly.js, Framer Motion, Lucide-React.
* **Backend**: Flask (Python), Pandas, NumPy, NLTK (VADER), Matplotlib, Wordcloud, urlextract, emoji.

---

## 🔒 WARNING: GitHub & Privacy (Important!)
> [!IMPORTANT]
> **DO NOT UPLOAD EXPORTED CHAT LOGS OR SENSITIVE DATASETS TO GITHUB.**
> 
> WhatsApp exported chats contain private conversations, phone numbers, email addresses, and potentially confidential personal/financial data. Even with the integrated Aadhaar/PAN filter, **raw export files (`.txt` logs) must remain strictly local.**
> 
> To safeguard this project:
> 1. A root-level `.gitignore` file has been configured to automatically block all `.txt`, `.pdf`, `.venv`, and `node_modules` folders from being tracked by git.
> 2. Ensure your repository on GitHub is set to **Private**.
> 3. Never commit test files (such as `WhatsApp Chat with BE IT A Official 2024-25.txt` or `WhatsApp Chat with Kunal Jadhav.txt`) into version control.

---

## 🚀 Process to Run Locally

### Prerequisites
* **Python 3.8 or above** installed on your system.
* **Node.js (v16+) and npm** installed.

---

### Step 1: Run the Backend Flask API
1. Open a terminal and navigate to the backend directory:
   ```bash
   cd ctda-main/backend
   ```
2. Create a virtual environment (if not already fully created):
   ```bash
   python -m venv venv
   ```
3. Activate the virtual environment:
   * **Windows (PowerShell)**:
     ```powershell
     .\venv\Scripts\Activate.ps1
     ```
   * **Windows (Command Prompt)**:
     ```cmd
     .\venv\Scripts\activate.bat
     ```
   * **macOS/Linux**:
     ```bash
     source venv/bin/activate
     ```
4. Install all python dependencies:
   ```bash
   pip install -r requirements.txt
   ```
5. Download the NLTK VADER Lexicon dataset (required for sentiment analysis):
   ```bash
   python -c "import nltk; nltk.download('vader_lexicon')"
   ```
6. Start the Flask server:
   ```bash
   python app.py
   ```
   *The backend server will run on `http://127.0.0.1:8080`.*

---

### Step 2: Run the Frontend React App
1. Open a new terminal window and navigate to the React app folder:
   ```bash
   cd ctda-main/frontend/ctda
   ```
2. Install the frontend dependencies:
   ```bash
   npm install
   ```
3. Start the Vite development server:
   ```bash
   npm run dev
   ```
   *The frontend dashboard will run locally on `http://localhost:5173` (or the next available port).*

---

### Step 3: Use the Dashboard
1. Open your web browser and navigate to `http://localhost:5173`.
2. Tap the **Upload** button and select your exported WhatsApp `.txt` file (without media).
3. Wait for the file content preview to load, then click **Get Users**.
4. Choose a user from the dropdown (or select **Overall** for group-level metrics).
5. Click **Analyze** to unlock the interactive dashboard!

---

## 📂 Codebase Structure
```dir
ctda-main/
│
├── .gitignore                    # Prevents sensitive logs/libs from uploading to GitHub
├── README.md                     # Main documentation file
│
└── ctda-main/                    # Main source directory
    ├── backend/                  # Python Flask API
    │   ├── app.py                # Main Flask driver routes
    │   ├── preprocessing.py      # Chat parsing, Aadhaar/PAN regex, and VADER analyzer
    │   ├── stats.py              # Word/link counting, temporal & emoji statistics
    │   ├── charts.py             # Plotly bar, line, pie, heatmap & wordcloud generators
    │   ├── nlp_charts.py         # Sentiment-based Plotly visualizers
    │   ├── stop_hinglish.txt     # Custom stopwords list for code-mixed English/Hindi
    │   ├── requirements.txt      # Python package requirements
    │   └── venv/                 # Local Python virtual environment
    │
    └── frontend/
        └── ctda/                 # Vite React application
            ├── package.json      # Frontend npm dependency configuration
            ├── index.html        # SPA index page HTML
            ├── tailwind.config.js# Styling configuration
            ├── src/
            │   ├── App.jsx       # Routing and page layout manager
            │   ├── assets/       # Visual guidelines and assets
            │   └── components/   # Modular React visualizers (Results, Heatmaps, Emojis, etc.)
```



