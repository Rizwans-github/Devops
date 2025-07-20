# 🐳 Docker Basics

## ✅ What is Docker?
- Docker lets you **package apps and their environment** into a single unit called a **container**.
- It runs the same way **on any system**, no setup drama.

## 🎮 Analogy: Console + Game CD
- Docker Image = 🎮 Game CD (app + everything it needs)
- Docker Container = 💻 Game running on the console
- Docker Engine = 🕹️ Gaming console (runs all CDs/containers)

So...  
> "Build your game once (image), and play it anywhere (container on any console)"

## 🚀 Why Use Docker?
- No more **"it works on my machine"**.
- Fast, portable, and reliable app deployment.
- Saves setup/configuration time.

## 🧱 Core Concepts

| Docker Term    | Meaning                                   | Analogy                          |
|----------------|-------------------------------------------|----------------------------------|
| **Image**      | Packaged app with its environment         | 🎮 Game CD                       |
| **Container**  | Running instance of that app              | 🕹️ Game being played             |
| **Dockerfile** | Steps to build the image                  | 📜 Game installation guide       |
| **Docker Engine** | Platform that runs everything          | 🖥️ Game Console (like PS5/Xbox)  |

## 🔧 Most Used Docker Commands

```bash
docker build -t myapp .         # Build image from Dockerfile
docker run -p 5000:5000 myapp   # Start container from image
docker ps                       # Show running containers
docker stop <container_id>      # Stop container
