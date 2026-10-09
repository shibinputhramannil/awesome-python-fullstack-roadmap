# ⚡ 02. Modern Backend Frameworks (FastAPI & Django)

## FastAPI Production Patterns
FastAPI has become the standard for asynchronous microservices and API gateways:

### Dependency Injection Pattern
```python
from fastapi import Depends, FastAPI, HTTPException, status
from fastapi.security import OAuth2PasswordBearer

app = FastAPI(title="Production Service")
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

async def get_current_user(token: str = Depends(oauth2_scheme)):
    # Validate JWT token and extract user
    if token != "secret-token":
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid authentication credentials"
        )
    return {"username": "shibin", "role": "admin"}

@app.get("/api/v1/profile")
async def read_profile(current_user: dict = Depends(get_current_user)):
    return {"message": "Authenticated", "user": current_user}
```

---

## Django & Celery Integration
For long-running background tasks (PDF generation, batch emails, heavy machine learning inference):

```python
# tasks.py
from celery import shared_task
import time

@shared_task
def send_welcome_email(user_email: str):
    time.sleep(2)  # Simulate email SMTP network call
    print(f"Sent welcome email to {user_email}")
    return True
```
