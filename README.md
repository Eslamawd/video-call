# 🎤 Social App - Voice & Video Rooms

> Real-time voice and video calling platform using **LiveKit**, built with **Next.js**, **NestJS**, and **Docker**.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Stars](https://img.shields.io/github/stars/Eslamawd/social-app?style=social)](https://github.com/Eslamawd/social-app)
[![Next.js](https://img.shields.io/badge/Next.js-16+-black?logo=next.js)](https://nextjs.org)
[![NestJS](https://img.shields.io/badge/NestJS-10+-E0234E?logo=nestjs)](https://nestjs.com)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker)](https://www.docker.com)

---

## 📋 Overview

**Social App** is a production-ready web application that enables real-time voice and video communication. Users can create rooms, invite others, and start instant peer-to-peer video/audio conversations.

### ✨ Key Features

- 🎥 **Real-time Video & Audio** - Powered by LiveKit
- 🚀 **Scalable Architecture** - Frontend, Backend, and Media server
- 🐳 **Docker-Ready** - Full stack in Docker Compose
- 🌍 **LAN & WAN Support** - Works on local networks and across the internet
- 🔐 **Secure Token Generation** - JWT-based access control
- 📱 **Mobile Friendly** - Works on phones and tablets
- ⚡ **WebRTC Optimized** - Auto-handling of ICE candidates and network conditions

---

## 🏗️ Architecture

```
┌─────────────┐
│   Browser   │
└──────┬──────┘
       │ HTTP/WS
       ▼
┌─────────────────────────────────┐
│      Next.js Frontend           │
│   (Port 3011, React + TS)       │
└──────┬──────────────────────────┘
       │
       │ API Call
       ▼
┌──────────────────────────────┐
│  NestJS Backend API          │
│  (Port 3001, Token Gen)      │
└──────┬───────────────────────┘
       │
       │ LiveKit API Key/Secret
       ▼
┌──────────────────────────────┐
│   LiveKit Server             │
│   (Port 7880 WS, WebRTC)     │
└──────────────────────────────┘
```

---

## 🔌 How It Works

### Join Flow

1. User enters room name → Frontend triggers join
2. Frontend requests token: `POST /api/rooms/join`
3. Backend generates signed JWT using LiveKit credentials
4. Frontend receives `token` + `livekitUrl`
5. LiveKit client connects, WebRTC session starts
6. Audio/video streams are shared in real-time

### Technology Stack

| Component        | Tech                           | Port      |
| ---------------- | ------------------------------ | --------- |
| **Frontend**     | Next.js 16+, TypeScript, React | 3011      |
| **Backend API**  | NestJS, TypeScript             | 3001      |
| **Media Server** | LiveKit Server                 | 7880 (WS) |
| **Container**    | Docker Compose                 | -         |

---

## 🚀 Quick Start (Docker)

### Prerequisites

- Docker Desktop
- Docker Compose (included with Docker Desktop)
- Git

### Setup (2 minutes)

```bash
# Clone the repo
git clone https://github.com/Eslamawd/video-call
cd video-call

# Create env file
echo 'HOST_IP=192.168.8.42' > .env
# Edit .env and set HOST_IP to your machine's local IP

# Build and start all services
docker compose up -d --build

# Verify services are running
docker compose ps
```

### Access the App

- **Frontend**: http://localhost:3011 (or http://<YOUR_HOST_IP>:3011)
- **Backend API**: http://localhost:3001
- **LiveKit**: ws://localhost:7880

---

## 🔧 Environment Variables

### Backend (`back-end/.env`)

```env
PORT=3001
LIVEKIT_API_KEY=devkey
LIVEKIT_API_SECRET=devsecret_1234567890_1234567890_1234
LIVEKIT_URL=ws://localhost:7880
FRONTEND_ORIGIN=http://localhost:3011
```

### Frontend (`frontend/.env.local`)

```env
NEXT_PUBLIC_API_BASE_URL=/api
BACKEND_API_BASE_URL=http://backend:3001
NEXT_PUBLIC_LIVEKIT_URL=ws://localhost:7880
```

### Root (`.env`)

```env
HOST_IP=192.168.8.42  # Your machine's local IP
```

---

## 📦 Project Structure

```
social-app/
├── back-end/                    # NestJS Backend
│   ├── src/
│   │   ├── app.module.ts
│   │   ├── rooms/
│   │   │   ├── rooms.controller.ts
│   │   │   ├── rooms.service.ts
│   │   │   └── dto/
│   │   └── main.ts
│   ├── Dockerfile
│   └── package.json
├── frontend/                    # Next.js Frontend
│   ├── app/
│   │   ├── page.tsx
│   │   ├── layout.tsx
│   │   └── api/
│   │       └── rooms/join/route.ts
│   ├── components/
│   │   └── voice-video-room.tsx
│   ├── hooks/
│   │   └── use-livekit-room.ts
│   ├── Dockerfile
│   └── package.json
├── docker-compose.yml           # Orchestration
├── livekit.yaml                 # LiveKit config
├── .env                         # Root env
└── README.md
```

---

## 🛠️ Available Commands

```bash
# Start all services
docker compose up -d --build

# View running services
docker compose ps

# View logs
docker compose logs -f livekit      # LiveKit logs
docker compose logs -f backend      # Backend logs
docker compose logs -f frontend     # Frontend logs

# Stop all services
docker compose down

# Rebuild images
docker compose build --no-cache
```

---

## 🌍 Deployment to VPS (Staging)

For a complete step-by-step deployment guide, see [DEPLOYMENT.md](./DEPLOYMENT.md).

### Quick Checklist

- [ ] Ubuntu 22.04+ VPS with Docker
- [ ] Domain/Subdomain configured
- [ ] Firewall ports opened (22, 80, 443, 7880-7881)
- [ ] LiveKit credentials set
- [ ] SSL certificate via Let's Encrypt
- [ ] Reverse proxy (Nginx/Caddy) configured

---

## 🔍 Troubleshooting

### "Invalid Token" Error

**Cause**: Mismatch between backend and LiveKit API keys.

**Solution**:

- Verify `LIVEKIT_API_KEY` and `LIVEKIT_API_SECRET` are identical
- Restart backend: `docker compose restart backend`

### WebRTC Connection Fails

**Cause**: Firewall blocking or wrong HOST_IP.

**Solution**:

- Check firewall allows 7881/tcp, 7881/udp, and UDP range (53000-53100)
- Verify `HOST_IP` in `.env` matches your local IP
- Use `ipconfig` (Windows) or `ifconfig` (Linux) to find your IP

### Audio/Video Not Working on Mobile

**Cause**: Mobile device using localhost or wrong domain.

**Solution**:

- Access app via IP: `http://<HOST_IP>:3011` instead of localhost
- Ensure mobile is on same WiFi network
- Check CORS settings in backend

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

- Report bugs via GitHub Issues
- Submit pull requests with improvements
- Share ideas in Discussions

---

## 📄 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [LiveKit](https://livekit.io) - Open-source WebRTC framework
- [Next.js](https://nextjs.org) - React framework
- [NestJS](https://nestjs.com) - Node.js framework
- [Docker](https://www.docker.com) - Containerization

---

## 📞 Support

For questions or support:

- 📧 Email: contact@example.com
- 💬 GitHub Discussions: [Link to discussions]
- 🐛 Report Issues: [GitHub Issues](https://github.com/Eslamawd/social-app/issues)

---

**Made with ❤️ by Eslamawd**

⭐ If you find this useful, please star the repo! 🌟
