# Event-Driven-Notification-System

Project Structure

EVENT-DRIVEN-NOTIFICATION-SYSTEM/
├── cmd/
│   └── api/
│       └── main.go
├── internal/
│   ├── handler/
│   │   ├── upload.go
│   │   └── status.go
│   ├── processor/
│   │   ├── worker.go
│   │   └── calculation.go
│   └── repository/
│       └── job.go
├── uploads/
│   ├── raw/
│   └── processed/
├── go.mod
└── README.md

┌─────────────────────────────────────────────────┐
│              HTTP API (Gin Server)               │
│  ┌─────────────────┐  ┌───────────────────┐     │
│  │  /upload (POST) │  │ /status/:id (GET) │     │
│  └─────────────────┘  └───────────────────┘     │
└─────────────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────┐
│              Worker Pool (N workers)             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  Worker 0   │  │  Worker 1   │  │ Worker N│ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
│         Buffered Channel (queue)                  │
└─────────────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────┐
│              Job Repository                      │
│  ┌─────────────────────────────────────┐         │
│  │  In-Memory Job State Cache          │         │
│  └─────────────────────────────────────┘         │
└─────────────────────────────────────────────────┘
