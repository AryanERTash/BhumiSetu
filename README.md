# Bhoomi Setu

Bhoomi Setu is a responsive national land acquisition monitoring prototype. It includes a React dashboard, Express REST API, and a local SQLite database. The seeded records make the dashboard useful immediately, and proposal, project update, document upload, audit history, and CSV report actions persist to SQLite.

## Run locally

Requires Node.js 20 or newer (developed with Node.js 22.22.2).

```sh
npm install
npm run dev
```

Open http://localhost:5173. Vite proxies `/api` requests to Express on port 3001. For a production build, run `npm run build && npm start`, then open http://localhost:3001.

SQLite data and uploaded documents live under `server/data` by default. Set `DATA_DIR` to move them.

## Deploy to Render

Create a Render Web Service from this repository. The included `render.yaml` selects Docker, checks `/api/health`, and mounts a persistent disk at `/data`. The container stores the SQLite database and uploaded files on that disk. The service uses the `PORT` supplied by Render.

## API

- `GET /api/health`, `GET /api/summary`
- `GET /api/projects` (supports `state`, `status`, `sector`, `q` filters)
- `POST /api/projects`, `PATCH /api/projects/:id`
- `GET /api/documents`, `POST /api/documents` (multipart field `file`, 20 MB limit), `GET /api/documents/:id/download`
- `GET /api/audit`, `GET /api/reports.csv`

## Notes

This is a demonstration platform with seeded sample figures and a schematic India map. Production deployment should connect authoritative land record/GIS services, government identity and access management, notification gateways, and approved security controls before real records are used.
