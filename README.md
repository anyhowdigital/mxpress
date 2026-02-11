mxpress | High-Speed IMAP Relocation Engine 

mxpress is a high-performance, server-to-server IMAP synchronization tool. Born out of necessity during our days as a digital agency (Anyhow), it was built to solve a single, frustrating problem: moving massive mailboxes without the tool crashing.

While most migration tools use slow web-wrappers that "choke" on special characters or timeout during 100GB+ transfers, mxpress uses a Hybrid-Core architecture to bridge the gap between a user-friendly interface and raw server-side power.

Why mxpress?
Standard migration tools fail for three reasons:
The "Dumb Splitter" Problem: They misinterpret special characters (!, &, $) in passwords, leading to "supplementary argument" errors.
Middleware Latency: They download data to a third-party server before uploading it to the destination.
Memory Leaks: They run inside bloated web environments that crash during long-running tasks.
mxpress bypasses the shell entirely, injecting credentials directly into the native Linux core via memory-injection.

Key Features
Server-to-Server Speed: Direct socket-streaming between IMAP providers.
Hybrid-Core Technology: The reliability of a native Linux binary with a responsive web-terminal interface.
100% Character Support: Handles complex passwords that break other tools.
Resume-Safe: Interrupted sync? Run it again. mxpress uses UID-based deduplication to skip already-migrated mail.
Folder Mapping: Automatically maps Sent, Drafts, Trash, and Archives across different providers (Gmail, Outlook, Private IMAP).
Internal Date Preservation: Keeps the original "Date Received" metadata intact.

Technical Architecture
mxpress operates on a Zero-Buffer Logic:
Web Layer: A Go-based terminal emulator (Gotty) provides a secure, encrypted UI.
Security Shield: A Caddy reverse-proxy handles automatic SSL (Let's Encrypt).
Execution Core: A custom-patched Perl engine that bypasses standard Docker wrappers to communicate directly with server kernels.

Quick Start (Docker)
Ensure you have Docker and Docker Compose installed.

Clone the repository:

Bash
git clone https://github.com/your-repo/mxpress.git
cd mxpress
Configure your domain: Edit the Caddyfile to point to your subdomain (e.g., mxpresscore.anyhow.gr).

Launch the engine:

Bash
docker-compose up -d --build
Access: Navigate to https://your-domain.com and start your migration.

Deployment Strategy
Code snippet
graph LR
    A[User Browser] -- HTTPS --> B[Caddy SSL Shield]
    B -- WebSocket --> C[mxpress Hybrid-Core]
    C -- Raw Socket --> D[Source IMAP Server]
    C -- Raw Socket --> E[Destination IMAP Server]

Beta Disclaimer
Interface: The current application interface is in English.

Cost: During the Beta period, mxpress is 100% Free to use.

Support: This tool is provided "as is," born from internal agency needs. Use the "Dry Run" feature before committing to a live migration.
