# aftercredits.

A personal anime archive for tracking what you have watched, what you are watching, and what you want to watch next. This project combines a lightweight static frontend with a FastAPI backend to give the user a clean, responsive anime library with authentication, collection management, and AniList-powered search.

## Overview

`aftercredits.` is designed as a personal anime tracker focused on speed, clarity, and a calm interface. Instead of a heavy app shell, it keeps the UI lightweight and uses a small server for account storage, collection persistence, and secure session management. The app helps users:

- keep an archive of watched, watching, and planned titles;
- add personal notes, dates, and ratings;
- search anime metadata from AniList;
- manage a profile with avatar and email;
- keep everything synced through a single API-backed account.

The project is built for local development and can also be adapted for deployment with a separate frontend host and production database.

## Main features

- Account registration and login with server-side storage.
- Session-based authentication using bearer tokens.
- Profile editing with username, avatar, and optional email.
- Add, update, and remove anime entries from the personal collection.
- Track statuses such as Watched, Watching, and Planned.
- Add a personal rating, date, and note for each title.
- Search AniList titles and pull metadata like cover, year, format, episodes, and score.
- Filter entries by status and search through saved titles.
- Switch the interface language between English, Ukrainian, and Russian.
- Responsive layout optimized for desktop and mobile screens.
- Built-in rate limiting and CORS protections on the backend.

## Functional overview

### Authentication

The app supports account creation, sign-in, sign-out, and profile updates. Authentication is handled in the backend and stored through secure session tokens. The frontend keeps the active token in session storage for the current browser tab.

### Collection management

Users can add anime titles to their collection, update their status and metadata, and remove items when needed. The collection API serves all saved entries for the signed-in account and supports import from locally stored browser data.

### Search and metadata

The search flow is powered by AniList. Users can type a title, explore results, and save the selected entry to their collection with metadata automatically attached.

### Profile and account experience

The account page includes user profile details, avatar support, email information, and account state. The design is intentionally minimal but polished, with strong visual emphasis on the user list and collection flow.

## Screenshots

<div align="center">
  <a href=""><img src="" alt="Collection view" width="220" /></a>
  <a href=""><img src="" alt="Account page" width="220" /></a>
  <a href=""><img src="" alt="Login screen" width="220" /></a>
  <a href=""><img src="" alt="Register screen" width="220" /></a>
  <a href=""><img src="" alt="Anime details" width="220" /></a>
  <a href=""><img src="" alt="Search view" width="220" /></a>
</div>

## Project structure

```text
.
├── assets/
│   └── favicon/                 # browser icons and manifest
├── backend/
│   ├── app/
│   │   ├── api/routes/
│   │   │   ├── auth.py          # login, register, logout, profile
│   │   │   └── collection.py    # collection CRUD and import flow
│   │   ├── core/
│   │   │   ├── database.py      # database engine and session setup
│   │   │   ├── security.py      # password hashing and token generation
│   │   │   └── rate_limit.py    # request limits and temporary blocking
│   │   ├── main.py              # FastAPI app, startup hooks, and CORS
│   │   ├── models.py            # database models
│   │   ├── schemas.py           # validation schemas
│   │   └── __init__.py
│   ├── data/                    # local SQLite database folder
│   ├── requirements.txt
│   └── .venv/                   # local virtual environment
├── css/
│   ├── auth.css                 # authentication layout and forms
│   ├── collection.css           # list, cards, stats, filters
│   ├── dialogs.css              # modals, notes, FAQ, calendar
│   ├── main.css                 # entry stylesheet and module order
│   ├── motion.css               # transitions and motion states
│   ├── playful.css              # decorative UI styling
│   ├── profile.css              # profile layout and avatar actions
│   ├── responsive.css           # responsive behavior
│   ├── search.css               # anime search overlay and results
│   ├── shell.css                # sidebar, layout shell, top bar
│   ├── tokens.css               # design tokens, variables, colors
│   └── ...
├── src/js/
│   ├── api.js                   # fetch wrapper and token handling
│   ├── anime-api.js             # AniList integration and mapping
│   ├── app.js                   # app bootstrap and UI coordination
│   ├── auth.js                 # auth UI actions and migration logic
│   ├── collection.js            # collection logic and statistics
│   ├── config.js                # API base URL configuration
│   ├── i18n.js                  # translations and UI texts
│   ├── storage.js               # browser storage helpers
│   ├── view.js                  # DOM rendering logic
│   └── ...
├── assets/
│   └── banners/                 # artwork used in the app UI
├── index.html                  # main application shell
├── LICENSE
├── README.md
└── todo
```

## Technologies used

- HTML5
- CSS3 with custom design tokens and responsive layout rules
- Vanilla JavaScript
- FastAPI (Python)
- SQLAlchemy ORM
- SQLite for local development
- AniList GraphQL API for search and metadata
- Argon2 password hashing
- CORS middleware and request rate limiting
- Session storage in browser for active auth token

## API summary

| Method | Endpoint                 | Purpose                               |
| ------ | ------------------------ | ------------------------------------- |
| POST   | `/api/auth/register`     | Create a new account                  |
| POST   | `/api/auth/login`        | Sign in and start a session           |
| POST   | `/api/auth/logout`       | End the active session                |
| GET    | `/api/auth/me`           | Get current user profile              |
| PATCH  | `/api/auth/profile`      | Update profile data                   |
| GET    | `/api/collection`        | Fetch collection items                |
| POST   | `/api/collection`        | Add a new anime entry                 |
| PATCH  | `/api/collection/{id}`   | Update an entry                       |
| DELETE | `/api/collection/{id}`   | Delete an entry                       |
| POST   | `/api/collection/import` | Import previously stored browser data |

## Notes about the project

This project intentionally keeps the frontend simple and static while moving the actual user data and auth logic to the backend. That approach makes the app easier to reason about, keeps credentials away from the browser, and makes future deployment smoother.

The codebase is organized around a clear separation:

- frontend: interface, interaction, rendering, language, browser state;
- backend: auth, sessions, data storage, validation, rate limiting;
- external API: AniList metadata provider.

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).
