# Customer Feedback Analyzer

An AI-powered **Customer Feedback Analyzer** that analyzes customer reviews using Google's Gemini API and generates meaningful insights from the feedback.

The project uses **Streamlit** for the frontend, **FastAPI** for the backend API, **SQLite** for storing feedback/data, and **Gemini** for AI-powered analysis.

---

## 🚀 Features

* Analyze customer reviews using AI
* Generate sentiment and insights from reviews
* Accept multiple customer reviews
* Streamlit-based interactive frontend
* FastAPI backend for handling requests
* Gemini API for AI-powered responses
* SQLite database for storing application data
* `uv` for Python dependency and virtual-environment management
* `.env` support for securely storing API keys

---

## 🛠️ Tech Stack

| Technology | Purpose                                   |
| ---------- | ----------------------------------------- |
| Python     | Main programming language                 |
| Streamlit  | Frontend / UI                             |
| FastAPI    | Backend REST API                          |
| Gemini API | AI-powered review analysis                |
| SQLite     | Local database                            |
| uv         | Python package and environment management |
| Uvicorn    | ASGI server for FastAPI                   |

---

# 🏗️ Project Architecture

The application follows a simple frontend → backend → AI architecture.

```text
                 Customer
                    │
                    │ Submit Reviews
                    ▼
          ┌─────────────────────┐
          │      Streamlit      │
          │     Frontend        │
          │      app.py         │
          └──────────┬──────────┘
                     │
                     │ HTTP Request
                     ▼
          ┌─────────────────────┐
          │       FastAPI       │
          │      Backend        │
          │       api.py        │
          └──────────┬──────────┘
                     │
                     │ Review / Prompt
                     ▼
          ┌─────────────────────┐
          │     Gemini API      │
          │    Gemini Model     │
          └──────────┬──────────┘
                     │
                     │ AI Response
                     ▼
          ┌─────────────────────┐
          │       FastAPI       │
          └──────────┬──────────┘
                     │
                     │ JSON Response
                     ▼
          ┌─────────────────────┐
          │      Streamlit      │
          │       Frontend      │
          └─────────────────────┘
```

---

# 🔄 How It Works

The application works in the following steps:

### 1. User enters reviews

The user provides one or more customer reviews through the Streamlit interface.

For example:

```text
The room was clean and comfortable.
The staff was very friendly.
The Wi-Fi connection was disappointing.
The breakfast was excellent.
```

### 2. Streamlit sends the reviews to FastAPI

The Streamlit frontend sends an HTTP request to the FastAPI backend.

Conceptually:

```text
Streamlit
    │
    │ POST /analyze
    │
    ▼
FastAPI
```

The review data is sent as part of the API request.

### 3. FastAPI receives the request

FastAPI receives the reviews and prepares them for AI analysis.

The backend is responsible for:

* Receiving the request
* Validating the input
* Preparing the prompt
* Calling Gemini
* Processing the Gemini response
* Returning the result to Streamlit

### 4. FastAPI sends the review to Gemini

The backend sends the review together with an analysis prompt to the Gemini API.

Conceptually:

```text
Customer Reviews
       +
Analysis Prompt
       │
       ▼
   Gemini API
       │
       ▼
 AI-generated analysis
```

### 5. Gemini analyzes the feedback

Gemini processes the reviews and generates an AI response.

Depending on the prompt, the response can contain information such as:

* Overall sentiment
* Positive feedback
* Negative feedback
* Common complaints
* Customer satisfaction
* Important issues
* Suggestions for improvement
* Overall summary

### 6. FastAPI returns the result

Gemini's response is returned to the FastAPI backend.

FastAPI then sends a JSON response back to Streamlit.

```text
Gemini
   │
   │ AI Response
   ▼
FastAPI
   │
   │ JSON Response
   ▼
Streamlit
```

### 7. Streamlit displays the analysis

The frontend receives the response and presents the analysis to the user.

---

# 📁 Project Structure

A typical project structure looks like:

```text
feedback_analyzer/
│
├── app.py                 # Streamlit frontend
├── api.py                 # FastAPI backend
├── database.py            # SQLite database functionality
├── feedback.db            # Local SQLite database
│
├── sample_review.txt      # Sample customer reviews
│
├── .env                   # API keys (not committed to Git)
├── .gitignore
│
├── pyproject.toml         # Project configuration and dependencies
├── uv.lock                # Locked dependency versions
│
└── README.md
```

> `feedback.db` and `.env` should normally be excluded from Git using `.gitignore`.

---

# ⚡ Why `uv`?

This project uses **uv** to manage the Python environment and dependencies.

`uv` provides a fast way to:

* Create virtual environments
* Install packages
* Manage dependencies
* Run Python applications
* Lock dependency versions

Instead of manually using:

```bash
python -m venv .venv
pip install ...
```

you can use `uv` to manage the project.

---

# 🧰 Setup

## 1. Install uv

If `uv` is not installed, install it using the official installation method for your operating system.

After installation, verify:

```bash
uv --version
```

---

# 2. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/feedback_analyzer.git
```

Move into the project:

```bash
cd feedback_analyzer
```

---

# 3. Create the virtual environment

Create a `.venv` environment using:

```bash
uv venv
```

This creates:

```text
.venv/
```

---

# 4. Activate the virtual environment

### macOS / Linux

```bash
source .venv/bin/activate
```

After activation, your terminal should show something similar to:

```text
(feedback-analyzer) user@MacBook feedback_analyzer %
```

### Windows

```powershell
.venv\Scripts\activate
```

---

# 5. Install dependencies

If dependencies are already defined in `pyproject.toml`, run:

```bash
uv sync
```

This installs the project's dependencies and uses the versions recorded in `uv.lock`.

If setting up the project from scratch, dependencies can be added with:

```bash
uv add fastapi
uv add uvicorn
uv add streamlit
uv add google-genai
uv add python-dotenv
uv add requests
```

SQLite is included with Python, so it does not need to be installed separately.

---

# 🔐 Gemini API Key

The backend requires a Gemini API key.

Create a `.env` file in the root of the project:

```text
feedback_analyzer/
│
├── .env
├── app.py
├── api.py
└── ...
```

Add:

```env
GEMINI_API_KEY=your_api_key_here
```

Replace:

```text
your_api_key_here
```

with your actual Gemini API key.

---

## ⚠️ Important Security Rule

**Never commit your `.env` file to GitHub.**

Your `.gitignore` should contain:

```gitignore
.env
.venv/
__pycache__/
*.db
.DS_Store
```

Your API key should remain local.

If an API key is accidentally pushed to GitHub, revoke/rotate the key immediately.

---

# ▶️ Running the Application

The application has two main components:

```text
Streamlit Frontend
        +
FastAPI Backend
```

Both need to be running.

---

## 1. Start FastAPI

Open a terminal inside the project directory and run:

```bash
uv run fastapi dev api.py
```

FastAPI will start the development server.

Typically:

```text
http://127.0.0.1:8000
```

FastAPI also provides interactive API documentation at:

```text
http://127.0.0.1:8000/docs
```

The `/docs` page can be used to test the backend API directly.

---

## 2. Start Streamlit

Open another terminal in the same project directory.

Activate the environment if necessary:

```bash
source .venv/bin/activate
```

Then run:

```bash
uv run streamlit run app.py
```

Streamlit will provide a local URL, usually:

```text
http://localhost:8501
```

Open that URL in your browser.

---

# 🔌 Backend API Flow

The backend exposes an API endpoint that receives customer feedback.

The general flow is:

```text
POST Request
     │
     ▼
/analyze
     │
     ▼
Receive reviews
     │
     ▼
Create Gemini prompt
     │
     ▼
Gemini API
     │
     ▼
Generate analysis
     │
     ▼
Return JSON
```

For example, the frontend can send:

```json
{
  "reviews": [
    "The room was clean and comfortable.",
    "The staff was very friendly.",
    "The Wi-Fi connection was disappointing."
  ]
}
```

The backend processes the reviews and returns the AI-generated analysis.

---

# 🧠 AI Analysis

Gemini is used as the reasoning and analysis layer.

The backend can provide Gemini with instructions such as:

```text
Analyze the following customer reviews.

Identify:
1. Overall sentiment
2. Positive aspects
3. Negative aspects
4. Common complaints
5. Important issues
6. Suggestions for improvement
7. Overall summary

Customer reviews:
...
```

Gemini then generates the response based on the provided reviews.

---

# 🗄️ Database

The project uses **SQLite** for local data storage.

The database file is:

```text
feedback.db
```

Database-related functionality is handled by:

```text
database.py
```

SQLite is useful for local development because it does not require a separate database server.

---

# 🧪 Testing with Sample Reviews

A sample review file can be used for testing:

```text
sample_review.txt
```

Example:

```text
The rooms were clean, comfortable, and well-maintained.
The staff was friendly and provided excellent service.
The hotel location was convenient and close to major attractions.
The breakfast was delicious with plenty of good options.
The room was spacious, but the Wi-Fi connection was disappointing.
The check-in process was quick and hassle-free.
The bathroom was clean, but the water pressure was quite low.
The hotel was overpriced considering the facilities provided.
The room was noisy at night, making it difficult to sleep.
Overall, the stay was disappointing due to poor service and maintenance.
```

This can be used to test the complete frontend → backend → Gemini flow.

---

# 🧑‍💻 Development Workflow

During development, the recommended workflow is:

```text
1. Start virtual environment
        ↓
2. Start FastAPI
        ↓
3. Start Streamlit
        ↓
4. Enter customer reviews
        ↓
5. Streamlit sends API request
        ↓
6. FastAPI calls Gemini
        ↓
7. Gemini analyzes reviews
        ↓
8. FastAPI returns response
        ↓
9. Streamlit displays results
```

---

# 🛠️ Useful Commands

### Create environment

```bash
uv venv
```

### Activate environment

```bash
source .venv/bin/activate
```

### Install dependencies

```bash
uv sync
```

### Add a dependency

```bash
uv add package-name
```

Example:

```bash
uv add requests
```

### Remove a dependency

```bash
uv remove package-name
```

### Run FastAPI

```bash
uv run fastapi dev api.py
```

### Run Streamlit

```bash
uv run streamlit run app.py
```

### Check Git status

```bash
git status
```

---

# 📌 Future Improvements

Possible future improvements include:

* Google Reviews integration
* Bulk CSV review upload
* Advanced sentiment scoring
* Review categorization
* Aspect-based sentiment analysis
* Interactive charts and dashboards
* Review trends over time
* Automatic business recommendations
* Authentication
* Cloud database
* Deployment to a cloud platform
* Export reports as PDF/CSV

---

# 📄 License

This project is currently intended for educational and development purposes.
