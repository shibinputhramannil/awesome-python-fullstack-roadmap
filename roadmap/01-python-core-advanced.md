# 🐍 01. Core & Advanced Python Guide

## 1. Type Hinting & Pydantic V2
In modern Python full-stack engineering, strict typing is mandatory for API safety and clean architecture:

```python
from pydantic import BaseModel, EmailStr, Field

class UserCreate(BaseModel):
    username: str = Field(..., min_length=3, max_length=50)
    email: EmailStr
    is_active: bool = True
```

## 2. Asynchronous Programming (`asyncio`)
Understand the event loop, coroutines, and concurrent execution:

```python
import asyncio

async def fetch_user_data(user_id: int):
    await asyncio.sleep(0.5)  # Simulate I/O bound database query
    return {"id": user_id, "name": "Shibin"}

async def main():
    users = await asyncio.gather(*(fetch_user_data(i) for i in range(5)))
    print(users)

asyncio.run(main())
```

## 3. Decorators & Context Managers
Custom decorators are heavily used in authentication, timing, and caching:

```python
import time
from functools import wraps

def timeit(func):
    @wraps(func)
    async def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = await func(*args, **kwargs)
        duration = time.perf_counter() - start
        print(f"{func.__name__} took {duration:.4f}s")
        return result
    return wrapper
```
