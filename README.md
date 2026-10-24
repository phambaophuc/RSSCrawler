# RSSCrawler 🚀


This project is a powerful RSS feed aggregator and summarizer built with NestJS and TypeScript. It fetches articles from various RSS feeds, cleans and extracts their content, and can optionally summarize them using the Google Gemini API. The project also manages publishers and feeds, storing articles in a PostgreSQL database.

## Badges 🏅

| Badge | Description |
|---|---|
| ![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white) | Written in TypeScript |
| ![NestJS](https://img.shields.io/badge/nestjs-339933?style=for-the-badge&logo=nestjs&logoColor=white) | Built with NestJS framework |
| ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) | Uses PostgreSQL for data storage |
| ![Google Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?style=for-the-badge&logo=google&logoColor=white) | Integrates with Google Gemini for summarization |
| ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) | Docker support (not explicitly configured but feasible) |

---

## Table of Contents 📚

- [Project Title & Badges](#rsscrawler-🚀)
- [Description](#description)
- [Table of Contents](#table-of-contents-📚)
- [Features](#features-✨)
- [Tech Stack](#tech-stack-🛠️)
- [Installation](#installation-⚙️)
- [Usage](#usage-💡)
- [How to Use](#how-to-use-👉)
- [API Reference](#api-reference-📚)
- [License](#license-📜)
- [Footer](#footer-❤️)

---

## Features ✨

*   **RSS Feed Aggregation:** Fetches and parses articles from multiple RSS feeds.
*   **Content Extraction:** Extracts clean article content from web pages using `@mozilla/readability` and `jsdom`.
*   **Content Summarization:** Leverages the Google Gemini API to summarize extracted article content.
*   **Database Persistence:** Stores publishers, feeds, and articles using TypeORM with PostgreSQL.
*   **Scheduled Fetching:** Automatically fetches RSS feeds at regular intervals (e.g., every 2 hours).
*   **API Endpoints:** Provides RESTful API endpoints for managing publishers, feeds, and articles, as well as for direct RSS scraping and content extraction/summarization.
*   **Swagger Documentation:** Integrated Swagger UI for API documentation.
*   **Input Validation:** Utilizes `class-validator` and `class-transformer` for robust API input validation.
*   **Error Handling:** Implements basic error handling and logging.

---

## Tech Stack 🛠️

*   **Language:** TypeScript
*   **Framework:** NestJS
*   **Database:** PostgreSQL (with TypeORM)
*   **API Documentation:** Swagger
*   **Content Extraction:** `@mozilla/readability`, `jsdom`, `cheerio`
*   **Summarization:** `@google/generative-ai` (Google Gemini)
*   **Scheduling:** `@nestjs/schedule`
*   **Utilities:** `rss-parser`, `cross-fetch`, `sanitize-html`, `slugify`
*   **Development Tools:** Node.js, npm/yarn, ESLint, Prettier, Jest, SWC

---

## Installation ⚙️

### Prerequisites

*   **Node.js:** Version 18.0.0 or higher.
*   **npm or yarn:** Package manager.
*   **PostgreSQL:** A running PostgreSQL database instance.

### Steps

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/phambaophuc/RSSCrawler.git
    cd RSSCrawler
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    # or
    yarn install
    ```

3.  **Configure environment variables:**
    Create a `.env` file in the root directory and populate it with your database and Gemini API credentials. Example:

    ```env
    # Database Configuration
    DB_URL=postgres://<user>:<password>@<host>:<port>/<database>
    DB_SYNCHRONIZE=false # Set to true for development if needed, but false is recommended for production

    # Gemini API Configuration
    GEMINI_KEY=<your_gemini_api_key>
    GEMINI_MODEL=<gemini_model_name> # e.g., gemini-pro

    # Application Port
    APP_PORT=3000
    ```

4.  **Run database migrations (if applicable) or ensure schema is set up.**
    *Note: The `synchronize: false` in `typeorm.config.ts` indicates that schema management should be handled via migrations. If you are in a development environment and prefer automatic schema synchronization, you can set `DB_SYNCHRONIZE=true` in your `.env` file, or manually manage migrations.*

5.  **Build the project:**
    ```bash
    npm run build
    ```

6.  **Start the application:**
    ```bash
    npm run start
    ```
    For development with watch mode:
    ```bash
    npm run start:dev
    ```

---

## Usage 💡

This project serves as a backend API for aggregating, processing, and summarizing RSS feed content. It can be used to build applications that:

*   **Automate content curation:** Collect articles from specified RSS feeds.
*   **Generate newsletters:** Summarize content and compile it into newsletters.
*   **Provide content analysis:** Extract and process information from various web sources.

---

## How to Use 👉

### 1. Managing Publishers and Feeds

**Create a Publisher:**
```bash
POST /api/publishers
Body: {
  "name": "Example Publisher",
  "homepage": "https://example.com"
}
```

**Create a Feed for a Publisher:**
```bash
POST /api/feeds
Body: {
  "name": "Example Feed",
  "url": "https://example.com/rss"
}
```
*(Note: The publisher ID is implicitly handled by the backend, likely through association in the service layer or by requiring a publisher association during feed creation if the API were more complex.)*

### 2. Fetching and Summarizing Content

**Manually Trigger RSS Scraping (for a single feed URL):**
This endpoint is primarily for testing or manual initiation.
```bash
POST /api/rss
Body: {
  "feedUrl": "https://example.com/rss"
}
```

**Extract Content from a URL:**
```bash
GET /api/extract?url=https://example.com/article-url
```

**Summarize Content from a URL:**
This endpoint uses the Gemini API to provide a summary.
```bash
GET /api/extract/summarize?url=https://example.com/article-url
```

### 3. Accessing Articles

**Get Paginated Articles (with optional filters):**
```bash
GET /api/articles?page=1&limit=10&feedId=<feed_id>&publisherId=<publisher_id>
```

### 4. Accessing Feeds

**Get all Feeds:**
```bash
GET /api/feeds
```

### 5. Accessing Publishers

**Get all Publishers:**
```bash
GET /api/publishers
```

**Get Publisher by Slug:**
```bash
GET /api/publishers/<publisher_slug>
```

## API Reference 📚

This project uses Swagger for API documentation. After starting the application, you can access the interactive API documentation at:

*   **Swagger UI:** `http://localhost:<APP_PORT>/swagger`

*(Replace `<APP_PORT>` with your configured application port, default is 3000)*

## License 📜

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Footer ❤️

This project is maintained by [phambaophuc](https://github.com/phambaophuc).

*   [Repository](https://github.com/phambaophuc/RSSCrawler)
*   [Star ⭐](https://github.com/phambaophuc/RSSCrawler/stargazers)
*   [Fork 🍴](https://github.com/phambaophuc/RSSCrawler/fork)
*   [Issues 🐞](https://github.com/phambaophuc/RSSCrawler/issues)
