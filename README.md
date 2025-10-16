# RDJR SOYHUCE — Environnement Docker complet

Projet complet **Laravel + React + MySQL**, orchestré avec **Docker Compose**.  
Ce dépôt regroupe :
- `rdjr-back` → backend Laravel (API + Filament)
- `rdjr-front-test` → frontend React/Vite/TypeScript
- `docker-compose.yml` → configuration Docker (3 services : back, front, DB)

---

## INSTALLATION COMPLÈTE 

```bash
# 1️⃣ Cloner le dépôt AVEC les sous-modules (back + front)
git clone --recurse-submodules https://github.com/Frederic-Leforestier/rdjr-soyhuce.git
cd rdjr-soyhuce

# 2️⃣ Construire et lancer les conteneurs
docker compose up --build -d

# 3️⃣ Vérifier que tout tourne bien
docker ps

# 4️⃣ Accéder au terminal du backend
docker compose exec backend bash

# 5️⃣ (DANS LE CONTENEUR BACKEND) :
php artisan migrate              # créer les tables
php artisan db:seed --class=RealDataSeeder   # insérer les données réelles
php artisan storage:link         # corriger les images
exit                             # sortir du conteneur

# 6️⃣ Vérifier dans le navigateur :
# - Frontend → http://localhost:5173
# - Backend API → http://localhost:8000
# - Filament Admin → http://localhost:8000/admin



# 🚀 Lancer tout le projet
docker compose up --build

# 🛑 Stopper le projet
docker compose down

# 🧹 Stopper + supprimer les volumes et images
docker compose down -v --rmi all

# 🐳 Voir les logs des conteneurs en direct
docker compose logs -f

# 🪄 Entrer dans le conteneur backend
docker compose exec backend bash

# ⚙️ Artisan (dans le conteneur backend)
php artisan migrate:fresh --seed      # reset complet de la BDD
php artisan make:filament-user        # créer un admin Filament
php artisan storage:link              # activer les images
php artisan tinker                    # console interactive Laravel

# 🧩 Mettre à jour les sous-modules (front et back)
git submodule update --remote --merge
git add rdjr-back rdjr-front-test
git commit -m "Update submodules"
git push

# 📦 Initialiser les sous-modules si clone sans recurse
git submodule update --init --recursive
