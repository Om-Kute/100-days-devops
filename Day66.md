☸️ Day 66 – Kubernetes ConfigMaps & Secrets
🎯 Objective
Learn how Kubernetes manages application configuration and sensitive information using ConfigMaps and Secrets.
📋 Why ConfigMaps & Secrets?
Applications often need configuration values that should not be hardcoded into application source code.
Application Code
       │
       ├── Configuration
       │       ↓
       │    ConfigMap
       │
       └── Sensitive Data
               ↓
             Secret
This allows the same application image to be configured differently for development, testing, and production.
