# 🎯 Habit Tracker Analyzer

A comprehensive habit tracking system with streak computation, completion rate analytics, habit correlation discovery, gamified achievements (6 types), calendar heatmaps, weekly/monthly reports, and AI-powered behavioral analysis — running 100% locally.

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB.svg?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Local LLM](https://img.shields.io/badge/Local_LLM-Ollama-000000.svg?style=for-the-badge&logo=ollama&logoColor=white)](https://ollama.com)
[![Privacy-First](https://img.shields.io/badge/100%25-Privacy--First-2ea043.svg?style=for-the-badge&logo=shield&logoColor=white)](#privacy-first)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![FastAPI](https://img.shields.io/badge/FastAPI-REST_API-009688.svg?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Streamlit](https://img.shields.io/badge/Streamlit-Web_UI-FF4B4B.svg?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)

---

## ✨ Features

- **🔗 Habit Tracking** - Log daily habit completion with timestamps
- **🔥 Streak Computation** - Automatic streak calculation and tracking
- **📊 Analytics** - Completion rates, trends, and performance metrics
- **🎯 Habit Correlation** - Discover which habits support each other
- **🏆 Gamification** - 6 achievement types for motivation
- **📅 Calendar Heatmap** - Visual representation of your habit consistency
- **📈 Reports** - Weekly and monthly behavioral analysis
- **🤖 AI Analysis** - Personalized insights on your habit patterns
- **🔒 100% Local** - All habit data stays private on your machine
- **🎨 Web UI & API** - Web dashboard, CLI, or REST endpoints

---

## 🏗️ Architecture

```
┌─────────────────┐
│  Habit Input    │
│ (Web/CLI/API)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Habit Engine   │
│ - Tracking      │
│ - Correlation   │
│ - Scoring       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Local LLM      │
│ (Ollama/Gemma)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Insights &     │
│  Reports        │
└─────────────────┘
```

---

## 📋 Project Structure

```
habit-tracker-analyzer/
├── src/habit_tracker/
│   ├── __init__.py              # Package initialization
│   ├── core.py                  # Habit tracking logic
│   ├── analytics.py             # Streak & correlation analysis
│   ├── achievements.py          # Gamification system
│   ├── cli.py                   # Click CLI interface
│   ├── api.py                   # FastAPI endpoints
│   └── web_ui.py                # Streamlit dashboard
├── tests/
│   ├── test_core.py             # Unit tests
│   └── __init__.py
├── config.yaml                  # Configuration
├── requirements.txt             # Dependencies
├── docker-compose.yml           # Docker setup
└── README.md                    # This file
```

---

## 🚀 Quick Start

### Prerequisites

- **Python 3.11+**
- **Ollama** (for local LLM)
- **Gemma 4 model** (via Ollama)

### Installation

```bash
# Clone the repository
git clone https://github.com/kennedyraju55/habit-tracker-analyzer.git
cd habit-tracker-analyzer

# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Pull the AI model
ollama pull gemma4

# Verify installation
python -m habit_tracker.cli --help
```

### First Run

```bash
# Start Ollama
ollama serve &

# Create a new habit
python -m habit_tracker.cli add-habit --name "Daily Exercise" --category health

# Log completion
python -m habit_tracker.cli log --habit "Daily Exercise"

# View your dashboard
streamlit run src/habit_tracker/web_ui.py

# Or use REST API
uvicorn src.habit_tracker.api:app --reload --port 8000
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Runtime** | Python 3.11+ | Core application |
| **CLI** | Click 8.1+ | Command-line interface |
| **Web** | Streamlit 1.28+ | Interactive dashboard |
| **API** | FastAPI | REST endpoints |
| **LLM** | Ollama + Gemma 4 | Behavioral AI analysis |
| **Data** | JSON/SQLite | Storage |
| **Testing** | pytest | Unit tests |
| **Deployment** | Docker | Container orchestration |

---

## 📖 CLI Reference

```bash
python -m habit_tracker.cli [COMMAND] [OPTIONS]
```

### Available Commands

| Command | Description | Example |
|---------|-------------|---------|
| dd-habit | Create new habit | --name "Morning Run" --category health |
| log | Log habit completion | --habit "Morning Run" |
| streak | View streak info | --habit "Morning Run" |
| nalytics | View completion stats | --days 30 |
| correlations | Find related habits | --habit "Morning Run" |
| chievements | View unlocked achievements | — |
| eport | Generate monthly report | --month current |

---

## 🌐 Web UI

Launch the interactive dashboard:

```bash
streamlit run src/habit_tracker/web_ui.py
```

Access at **http://localhost:8501**

Features:
- 📅 Calendar heatmap visualization
- 🔥 Streak tracking with milestones
- 📊 Completion rate charts
- 🎯 Habit correlation insights
- 🏆 Achievement showcase
- 📈 Weekly/monthly trends
- 🤖 AI behavioral analysis

---

## ⚡ REST API

All features via FastAPI endpoints.

```bash
uvicorn src.habit_tracker.api:app --reload --port 8000
```

Interactive docs: **http://localhost:8000/docs**

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /health | Health check |
| POST | /habits | Create habit |
| POST | /log | Log completion |
| GET | /streak/{habit} | Get streak info |
| GET | /analytics/{habit} | Habit analytics |
| GET | /correlations | Find habit correlations |

---

## 🐳 Docker Deployment

```bash
git clone https://github.com/kennedyraju55/habit-tracker-analyzer.git
cd habit-tracker-analyzer

docker compose up

# Access at http://localhost:8501
```

---

## 🧪 Testing

```bash
# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ --cov=habit_tracker --cov-report=term-missing

# Run specific test
pytest tests/test_core.py::test_streak_calculation -v
```

---

## ⚙️ Configuration

Create a config.yaml:

```yaml
habits:
  categories:
    - health
    - productivity
    - learning
    - personal
  default_tracking_days: 90

achievements:
  types:
    - "Streak Milestone"
    - "Perfect Week"
    - "100 Days"
    - "Consistency"
    - "Habit Master"
    - "Synergy"

analytics:
  track_correlations: true
  min_correlation_threshold: 0.6
  heatmap_months: 12
```

---

## 🏆 Achievement System

Earn 6 types of achievements:

1. **Streak Milestone** - Reach 7, 30, 100 day streaks
2. **Perfect Week** - 100% completion for 7 days
3. **100 Days** - Any habit at 100 days
4. **Consistency** - 95%+ completion over 30 days
5. **Habit Master** - Track 10+ habits simultaneously
6. **Synergy** - Discover habit correlations

---

## 🔒 Privacy-First

100% local processing:
- ✅ No cloud API calls
- ✅ No tracking or telemetry
- ✅ Your habit data stays private
- ✅ Full AI control
- ✅ GDPR/HIPAA compliant

---

## 📚 Python API

```python
from habit_tracker.core import add_habit, log_completion
from habit_tracker.analytics import get_streak, get_correlations

# Add a new habit
habit = add_habit(
    name="Morning Meditation",
    category="health",
    target_days=365
)

# Log completion
log_completion(habit_id=habit['id'])

# Get streak info
streak_info = get_streak(habit_id=habit['id'])
print(f"Current streak: {streak_info['days']} days")

# Find correlated habits
correlations = get_correlations(habit_id=habit['id'])
print(f"Related habits: {correlations}")
```

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: git checkout -b feature/amazing-feature
3. Commit changes: git commit -m 'Add amazing feature'
4. Push to branch: git push origin feature/amazing-feature
5. Open a Pull Request

---

## 📄 License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 👤 Author

**Nrk Raju Guthikonda**
- GitHub: [@kennedyraju55](https://github.com/kennedyraju55)
- Dev.to: [@kennedyraju55](https://dev.to/kennedyraju55)
- LinkedIn: [Nrk Raju Guthikonda](https://linkedin.com/in/nrk-raju-guthikonda)

---

<div align="center">

**Made with ❤️ by kennedyraju55**

[⭐ Star this repo if you found it helpful!](https://github.com/kennedyraju55/habit-tracker-analyzer)

</div>
