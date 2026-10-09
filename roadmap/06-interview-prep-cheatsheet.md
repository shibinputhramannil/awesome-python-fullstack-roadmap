# 💼 06. Python Full Stack Interview Cheatsheet

### Q1: What is the difference between synchronous WSGI (Django/Flask) and asynchronous ASGI (FastAPI)?
**Answer:**
- **WSGI (Web Server Gateway Interface):** Handles requests synchronously (one request per thread/process). If a request waits on an I/O query (database, third-party API), the thread is blocked.
- **ASGI (Asynchronous Server Gateway Interface):** Supports asynchronous Python (`async`/`await`). A single thread can handle thousands of concurrent connections (ideal for WebSockets, chat apps, and high-throughput APIs).

---

### Q2: How do you prevent SQL Injection and N+1 query problems in Django / SQLAlchemy?
**Answer:**
- **SQL Injection:** Always use ORM parameterized queries or SQLAlchemy bind parameters. Never format raw strings into SQL queries.
- **N+1 Problem:** Occurs when fetching parent records and then querying child records individually in a loop.
  - In Django: Use `select_related()` (for ForeignKey / OneToOne) and `prefetch_related()` (for ManyToMany).
  - In SQLAlchemy: Use `joinedload()` or `selectinload()`.

---

### Q3: How do you manage database connections in production with FastAPI?
**Answer:**
Use async connection pooling (e.g. `asyncpg` with SQLAlchemy `create_async_engine(..., pool_size=20, max_overflow=10)`) or deploy **PgBouncer** in front of PostgreSQL to prevent running out of database connections under high traffic.
