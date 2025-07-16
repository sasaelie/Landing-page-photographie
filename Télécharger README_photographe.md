
# 📸 Site Photographe Mariage — Backend & Frontend

Un projet complet pour une landing page photographe de mariage, avec un backend Node.js (Express + SQLite) et un frontend React (Vite + TailwindCSS), prêt à déployer sur Netlify + Railway, ou localement avec Docker.

---

## 🧱 Structure du projet

```
├── backend/
│   ├── main.js
│   ├── routes/
│   ├── controllers/
│   ├── models/
│   ├── config/
│   ├── tests/
│   └── .env
│
├── frontend/
│   ├── src/
│   ├── public/images/
│   ├── index.html
│   └── vite.config.js
```

---

## 🚀 Lancer le projet avec Docker (recommandé)

### 1. Installer Docker

➡️ https://www.docker.com/products/docker-desktop

### 2. Créer les fichiers suivants à la racine :

#### 📄 `Dockerfile`

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN cd backend && npm install
RUN cd frontend && npm install && npm run build
CMD ["node", "backend/main.js"]
```

#### 🐳 `docker-compose.yml`

```yaml
version: "3.8"
services:
  backend:
    build: .
    ports:
      - "4000:4000"
    volumes:
      - ./backend:/app/backend
    environment:
      - PORT=4000
    command: node backend/main.js

  frontend:
    image: node:18
    working_dir: /app/frontend
    volumes:
      - ./frontend:/app/frontend
    ports:
      - "5173:5173"
    command: sh -c "npm install && npm run dev"
```

---

## 🌐 Déploiement séparé

### Frontend (Netlify)
1. Dépose `/frontend` sur Netlify
2. Configure `vite.config.js` pour le bon `base` si nécessaire

### Backend (Railway)
1. Crée un projet Railway
2. Uploade `/backend`
3. Ajoute une base SQLite ou PostgreSQL si besoin
4. Configure l’URL de l’API pour le frontend

---

## 📩 Contact API

- URL : `POST /api/contact`
- Body :
```json
{
  "name": "Nom",
  "email": "exemple@mail.com",
  "date": "2025-08-12",
  "message": "Votre message"
}
```

---

## 🧪 Tests

Dans `backend/tests/`, lance les tests avec :

```bash
npm install
npm run test
```

---

## 💾 Base de données (SQLite)

- Stockée dans `/backend/data/database.sqlite`
- Modèle : `reservations(id, name, email, date, message, created_at)`

---

## ✨ Tech stack

- **Frontend** : React, Vite, TailwindCSS, i18n
- **Backend** : Express.js, better-sqlite3, dotenv
- **Tests** : Jest, Supertest
- **Hébergement** : Netlify (frontend), Railway (backend)

---

## 🙌 Merci à Eli pour la direction artistique et technique de ce projet.
