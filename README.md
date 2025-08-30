
# EVT Project

A step-by-step guide to run the EVT Project (Backend + Frontend).

## Project Structure

```
evt-server/
├── evt-backend/
├── frontend/
└── backup.sql
```

## Backend Setup (FastAPI)

Navigate to the backend directory:

```bash
cd evt-server/evt-backend
```

Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Linux/macOS
venv\Scripts\activate   # On Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### PostgreSQL Setup

Default `DATABASE_URL` :

```
postgresql+asyncpg://postgres:root@127.0.0.1:5433/evt_be
```

#### DB Configuration:
- User: postgres  
- Password: root  
- Host: 127.0.0.1  
- Port: 5433  
- Database: evt_be  

#### Steps:

1. Connect to PostgreSQL:
   ```bash
   psql -U postgres -h 127.0.0.1 -p 5433
   # Enter password: root
   ```
2. Create the database:
   ```sql
   CREATE DATABASE evt_be;
   ```
3. Verify the database:
   ```sql
   \l
   ```
4. (Optional) Create a dedicated user:
   ```sql
   CREATE USER myapp_user WITH PASSWORD 'myapp_password';
   GRANT ALL PRIVILEGES ON DATABASE evt_be TO myapp_user;
   ```
5. Exit PostgreSQL:
   ```sql
   \q
   ```

✅ PostgreSQL is ready to connect using your `DATABASE_URL`.

### Apply Database Migrations

From the `evt-backend` directory:

```bash
alembic upgrade head
```

This will create the required tables in your PostgreSQL database as defined in the `versions` folder.

### Run Backend Server

Ensure `.env` contains:

```
DATABASE_URL=postgresql+asyncpg://postgres:root@127.0.0.1:5433/evt_be
```

Run the server:

```bash
python -m uvicorn app.main:app --reload
```

To access the server on the local network:

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

---

## Frontend Setup (Next.js)

1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```
2. Install npm dependencies:
   ```bash
   npm install
   ```
3. Update `.env.local` :
   ```
   NEXT_PUBLIC_API_URL=http://127.0.0.1:8000
   ```
4. Run the frontend server:
   ```bash
   npm run dev
   ```

Make sure npm is installed globally (`npm -v` to verify).

---

## Notes

- Port numbers, database names, or usernames may vary. Adjust `.env` and commands accordingly.  
- Ensure backend is running before starting the frontend.  

✅ Project is ready! Open your browser at [http://localhost:3000](http://localhost:3000) to view the frontend.
