# Beach 2026 Website - Project Handoff

**Date:** January 19, 2026
**Project:** Beach 2026 Emerald Isle - Retro 90s Style Website
**Owner:** Christian

---

## 🎯 Project Overview

This is a retro 90s-themed beach vacation website with:

- Classic GeoCities/Angelfire aesthetic
- Visitor counter functionality
- Music player with autoplay
- Animated elements (marquees, blinking text, rainbow effects)
- Shopping list for beach trip supplies
- "No swinging allowed" joke section

---

## ✅ What's Been Completed

### 1. **Website Features**

- ✅ Full retro 90s HTML page with inline CSS
- ✅ Background music player (assets/back_music.ogg)
- ✅ Visitor counter using CountAPI.xyz with localStorage fallback
- ✅ Shopping list section (emphasis on deli meat and board games)
- ✅ Beach rules section (humorous "no swinging" notice)
- ✅ Under construction animations
- ✅ Marquee scrolling text
- ✅ Guestbook placeholder

### 2. **Visitor Counter Implementation**

- API: CountAPI.xyz endpoint
- Namespace: `beach2026-christian/emerald-isle`
- Fallback: localStorage counter if API fails
- Format: Spaced digits (e.g., "0 0 1 5")

### 3. **Docker Setup**

- ✅ Created `docker-compose.yml` file
- Service: nginx:alpine
- Port: 8080 (internal 80)
- Volume: Current directory mounted as read-only

---

## 📁 Project Structure

```
beach 2026/
├── index.html              # Main website file
├── docker-compose.yml      # Docker Compose configuration
├── CLAUDE_HANDOFF.md      # This file
├── assets/
│   └── back_music.ogg     # Background music file
└── assets copy/           # Backup folder
```

---

## 🚀 Next Steps - Deployment

### User's Environment

- **OS:** macOS
- **Docker:** Uses Docker Compose
- **Reverse Proxy:** Nginx Proxy Manager with wildcard SSL cert
- **Goal:** Self-host this website for friends to access

### To Complete Deployment

1. **Start Docker Desktop** (if not running)

   ```bash
   open -a Docker
   ```

2. **Move repository to deployment server**
   - Transfer entire `/Users/christian/repos/beach 2026/` directory
   - Ensure `docker-compose.yml` and `index.html` are present

3. **Start the container**

   ```bash
   cd /path/to/beach-2026
   docker compose up -d
   ```

   - This will serve the site on port 8080

4. **Configure Nginx Proxy Manager**
   - URL: Usually `http://server-ip:81`
   - Add new Proxy Host:
     - **Domain:** `beach.yourdomain.com` (or desired subdomain)
     - **Scheme:** `http`
     - **Forward Hostname/IP:** `host.docker.internal` or server IP
     - **Forward Port:** `8080`
     - **SSL Tab:** Select wildcard certificate, enable Force SSL

5. **DNS Configuration**
   - Add A record: `beach.yourdomain.com` → server public IP
   - Ensure ports 80/443 are forwarded to NPM server

6. **Test**
   - Visit `https://beach.yourdomain.com`
   - Check visitor counter increments
   - Verify music plays (may need user interaction)

---

## ⚙️ Technical Details

### Visitor Counter

- **Primary API:** `https://api.countapi.xyz/hit/beach2026-christian/emerald-isle`
- **Fallback:** localStorage (browser-specific)
- **Format Function:** Pads to 4 digits, spaces between each digit
- **Console Logging:** Enabled for debugging

### Music Player

- **File:** `assets/back_music.ogg` (must exist)
- **Autoplay:** Attempts autoplay, shows button if blocked
- **Controls:** HTML5 audio controls visible
- **Loop:** Enabled

### Docker Container

- **Image:** `nginx:alpine` (lightweight)
- **Port Mapping:** Host 8080 → Container 80
- **Volume:** Read-only mount of current directory
- **Restart Policy:** `unless-stopped`
- **Network:** Custom network `beach-network`

---

## 🐛 Known Issues / Notes

1. **Visitor Counter Status:** May show "? ? ? ?" if CountAPI fails
   - Fallback to localStorage works
   - Console logs errors for debugging

2. **Music Autoplay:** Browsers block autoplay by default
   - Button appears if blocked
   - User must click to play

3. **Docker Compose Version:** Warning about obsolete `version` field (can be ignored or removed)

---

## 📝 Content Highlights

### Shopping List Items

- 🥪 Deli meat (LOTS)
- 🧀 Cheese
- 🎲 Board games
- 🃏 Card games
- 🍞 Bread

### Beach Activities

- Swimming, sand castles, ice cream
- Getting tan, collecting seashells
- Watching sunsets

---

## 🔧 Useful Commands

```bash
# Start container
docker compose up -d

# Stop container
docker compose down

# View logs
docker compose logs -f

# Restart after changes
docker compose restart

# Check container status
docker ps | grep beach

# Test locally
curl http://localhost:8080
```

---

## 💡 Future Enhancements (Not Yet Implemented)

- Actual guestbook with CGI scripts / form backend
- Image gallery of beach photos
- Additional pages (about, contact, etc.)
- Self-hosted visitor counter (if CountAPI unreliable)
- Additional retro GIFs and animations

---

## 🎨 Design Philosophy

Maintains authentic 90s web aesthetic:

- Clashing colors (cyan, yellow, magenta, red)
- Comic Sans MS font
- Animated GIFs and blinking text
- Marquee elements
- "Under Construction" notices
- Excessive exclamation marks!!!
- Emoji overload 🏖️🌊☀️

---

**End of Handoff Document**

*Good luck with deployment! The site is ready to go - just needs Docker started and NPM configured. 🏖️*
