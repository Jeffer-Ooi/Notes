# Investment Website: Supporting Projects and Learning Roadmap

## Purpose

Build small services and tools that the investment website can use. Each project develops a different engineering skill while contributing to one connected product.

## Recommended Projects

| Project | Website functionality | Learning focus | Suggested order |
|---|---|---|---|
| Background processing system | Process filings asynchronously and display pending, running, completed or failed status | Job queues, workers, retries, idempotency and concurrency | Next |
| Watchlist and investment journal | Save stocks to follow, research notes and review dates | Database design, migrations, search, pagination and authorisation | After background processing |
| Scheduled alerts | Send review reminders and document-processing notifications | Scheduling, delivery retries, duplicate prevention and user preferences | Later |
| Data import and export | Import holdings from files and export records | File validation, preview flows, duplicate detection and database transactions | Later |
| Service monitoring dashboard | Display service availability, response times and failures | Health checks, metrics, logs, networking and incident investigation | Alongside deployment |

## 1. Background Processing System

This is the recommended next project because downloading, parsing and embedding a filing can take longer than a user should wait on a page.

### Workflow

1. The website requests filing processing.
2. The backend creates a job and returns its identifier.
3. A worker processes the filing separately.
4. The website checks and displays job status.
5. The user can search the filing when processing finishes.

### Implementation Order

- Record job status and processing errors.
- Add retries for recoverable failures.
- Prevent duplicate jobs and duplicate records.
- Limit simultaneous processing jobs.

Idempotency means repeated execution does not create unintended duplicate effects.

## 2. Watchlist and Investment Journal

Build this as part of the investment application to practise conventional application engineering alongside AI work.

### Features

- Add and remove stocks from a watchlist.
- Create, edit and delete investment notes.
- Associate notes with a stock.
- Set review dates.
- Search and paginate saved records.
- Enforce ownership checks when multiple users are supported.

Later, allow a note to reference evidence returned by the SEC RAG service.

## 3. Scheduled Alerts

Introduce alerts when reminders or processing notifications become useful.

### Features

- Research review reminders.
- Filing-processing completion notifications.
- Notification preferences.
- Delivery status and failure reporting.
- Retry failed deliveries without sending duplicate notifications.

## 4. Data Import and Export

Support holdings snapshots and research records without introducing purchase or sale transactions.

### Features

- Upload a supported file format.
- Validate fields and show row-level errors.
- Preview changes before saving.
- Detect duplicate holdings.
- Define whether matching holdings are updated or skipped.
- Export saved records.

## 5. Service Monitoring Dashboard

Build a small view of the application's operational health.

### Features

- Website and RAG service availability.
- Request response times.
- Processing failures.
- Recent job status.
- Last successful health check.

## Repository Organisation

| Work | Recommended location |
|---|---|
| Watchlists, notes and holdings import/export | Investment application repository |
| Filing workers and job management | SEC RAG repository initially |
| Docker, CI/CD, logging and rate limiting | Within the application that needs them |
| Independent monitoring tool | Separate repository if it monitors several services |

A separate repository is not required for every learning topic. Keep closely related functionality together until there is a practical reason to separate it.

## Suggested Learning Order

1. Finish a usable SEC RAG API.
2. Deploy it and connect it to the investment backend.
3. Add background filing processing.
4. Build the watchlist and investment journal.
5. Connect research evidence to saved notes.
6. Add alerts, import/export and monitoring as needed.

## Working Approach

- Build one useful capability at a time.
- Introduce infrastructure when it solves an observed problem.
- Learn both the tool and the responsibility behind it.
- Record important decisions and lessons.
- Finish and maintain working integrations before starting additional projects.

