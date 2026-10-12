import os
import psycopg2
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    db_url = os.environ.get("DATABASE_URL")
    if not db_url:
        return {"status": "error", "message": "DATABASE_URL is not set"}

    try:
        conn = psycopg2.connect(db_url)
        cur = conn.cursor()
        cur.execute("SELECT version();")
        db_version = cur.fetchone()[0]
        cur.close()
        conn.close()
        return {
            "status": "connected",
            "message": "Neon database connected successfully!",
            "postgres_version": db_version
        }
    except Exception as e:
        return {"status": "error", "message": str(e)}
