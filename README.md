# 🎵 Spotify Wrapped Platform: Year-Round Listening Analytics & Audio Trivia Web App

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-Full--Stack-092E20.svg?logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Spotify API](https://img.shields.io/badge/Spotify-Web%20API%20OAuth2-1DB954.svg?logo=spotify&logoColor=white)](https://developer.spotify.com/documentation/web-api)
[![Course](https://img.shields.io/badge/Georgia%20Tech-CS%202340%20Objects%20%26%20Design-B3A369.svg)](https://www.gatech.edu/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> A full-stack web application that brings the excitement of **Spotify Wrapped** to any time of the year. Built with **Django** and the **Spotify Web API**, the platform empowers users to authenticate with their Spotify accounts, generate personalized listening summaries (both regular and holiday-themed), persist historic wraps, play an interactive audio-snippet guessing game, and toggle between multiple languages.

---

## 📌 Features

- 🎧 **On-Demand Wrapped Analytics**: Connect your Spotify account to instantly generate listening recaps covering top artists, most-streamed tracks, top genres, and acoustic profiles across customizable time frames (short, medium, long term).
- 🎄 **Themed Wrap Experiences**: Generate specialized **Holiday Wraps** alongside standard recaps, featuring customized holiday visual themes and seasonal music filtering.
- 💾 **Historic Wrap Persistence**: Stores generated wraps with flexible **Django JSONField** schemas, allowing users to revisit, compare, and showcase past music recaps.
- 🕹️ **Interactive Audio Trivia Game**: Test your music knowledge with an in-browser guessing game that streams 30-second preview audio snippets directly from Spotify's CDN.
- 🌍 **Internationalization (i18n)**: Multi-language localization infrastructure supporting dynamic language switching.
- 🔐 **Secure Spotify OAuth 2.0**: Implements Spotify's Authorization Code flow, ensuring secure credential exchange and automatic token refreshes.

---

## 🏗️ Architecture & Data Flow

```
                                 ┌─────────────────────────┐
                                 │     User's Browser      │
                                 └────────────┬────────────┘
                                              │
                      ┌───────────────────────┴───────────────────────┐
                      │ 1. OAuth Redirect                             │ 4. Rendered HTML / Audio
                      ▼                                               ▼
       ┌──────────────────────────────┐                ┌──────────────────────────────┐
       │   Spotify Accounts Service   │                │   Django Web Application     │
       │   - Auth Code Grant          │                │   - OAuth Callback Handler   │
       │   - Access & Refresh Tokens  │                │   - Wrap Analytics Engine    │
       └──────────────┬───────────────┘                │   - Audio Game Controller    │
                      │ 2. Callback Code               └──────────────┬───────────────┘
                      ▼                                               │
       ┌──────────────────────────────┐                               │
       │     Spotify Web API CDN      │◄──────────────────────────────┘
       │     - Top Tracks / Artists   │  3. Authenticated Data Retrieval
       │     - 30s Audio Previews     │
       └──────────────────────────────┘
```

---

## 🛠️ Tech Stack

- **Backend**: Python 3.10+, Django MVC
- **APIs & SDKs**: Spotify Web API (REST, OAuth 2.0 Authorization Code Flow)
- **Database**: SQLite with dynamic JSONField storage
- **Frontend**: HTML5 Audio API, CSS3, JavaScript, Django Template Language
- **Localization**: Django `gettext` / locale translation framework

---

## 📂 Repository Structure

```
spotify-wrapped-project/
├── SpotiProject/            # Root Django project settings & configuration
│   ├── settings.py          # App registry, i18n settings, Spotify client config
│   ├── urls.py              # Root router
│   └── wsgi.py              # WSGI entry point
├── music/                   # Music & Wrapped application module
│   ├── models.py            # Wrap (JSONField) and ContactMessage models
│   ├── views.py             # Spotify OAuth, API fetching, and Wrap generation
│   ├── urls.py              # Music application routes
│   ├── locale/              # Multi-language translation binaries (.po / .mo)
│   └── templates/           # Wrap display, audio game, and account templates
├── static/                  # Dark-mode styled CSS, animations, and icons
├── manage.py                # Django CLI tool
└── README.md
```

---

## 🚀 Getting Started

### 1. Prerequisites
- Python 3.10+
- A [Spotify Developer Account](https://developer.spotify.com/dashboard) to obtain API credentials.

### 2. Spotify App Setup
1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard) and create a new App.
2. In the App settings, add the redirect URI:
   ```
   http://127.0.0.1:8000/callback/
   ```

### 3. Installation & Configuration
```bash
# Clone the repository
git clone https://github.com/byohros6/spotify-wrapped-project.git
cd spotify-wrapped-project

# (Optional) Create and activate virtual environment
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install django requests spotipy
```

Set your credentials in your environment:
```bash
# Windows PowerShell
$env:SPOTIPY_CLIENT_ID="your_spotify_client_id"
$env:SPOTIPY_CLIENT_SECRET="your_spotify_client_secret"
$env:SPOTIPY_REDIRECT_URI="http://127.0.0.1:8000/callback/"

# Linux / macOS
export SPOTIPY_CLIENT_ID="your_spotify_client_id"
export SPOTIPY_CLIENT_SECRET="your_spotify_client_secret"
export SPOTIPY_REDIRECT_URI="http://127.0.0.1:8000/callback/"
```

### 4. Run the Application
```bash
# Run database migrations
python manage.py migrate

# Launch local server
python manage.py runserver
```
Navigate to `http://127.0.0.1:8000` to log in and generate your first wrap!

---

## 👥 Credits & Academic Context

- **Course**: CS 2340 (Objects and Design) at the **Georgia Institute of Technology**.
- **Contributors**:
  - **Benjamin Yohros** ([@byohros6](https://github.com/byohros6)) - Full-stack architecture, backend stabilization, views and route orchestration, and final integration.
  - **Jad Bardawil** ([@jmb245](https://github.com/jmb245)) - Spotify API authorization, callback flow, and language localization logic.
  - **Emily Prieto** ([@emilyprietob](https://github.com/emilyprietob)) - UI/UX styling, audio guessing game frontend, and contact page.
  - **Natalie Burstein** ([@natalieburstein08](https://github.com/natalieburstein08)) - User onboarding, home page layouts, and signup views.
  - **Heeyoon Shin** - Design collaboration and feature ideation.

*This repository serves as an academic and engineering portfolio showcase of API integration, OAuth 2.0 security, and full-stack software development.*
