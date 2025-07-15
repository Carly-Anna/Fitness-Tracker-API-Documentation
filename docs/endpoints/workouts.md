# Workouts

## POST /workouts

Create a new workout entry.

**Request**

```http
POST /workouts
Authorization: Bearer {token}
Content-Type: application/json
```

{
  "user_id": "123",
  "type": "cardio",
  "duration_minutes": 30,
  "calories_burned": 250,
  "notes": "Morning run"
}
{
  "id": "789",
  "user_id": "123",
  "type": "cardio",
  "duration_minutes": 30,
  "calories_burned": 250,
  "created_at": "2025-07-15T08:00:00Z"
}
---
## Get /workouts?user_id=123
Retrieve a list of workouts for a specific user
[
  {
    "id": "789",
    "type": "cardio",
    "duration_minutes": 30,
    "calories_burned": 250,
    "created_at": "2025-07-15T08:00:00Z"
  }
]


---

### 🔹 `docs/endpoints/progress.md`

```markdown
# Progress

## GET /progress/weight

Fetch weight history for a user.

**Request**

```http
GET /progress/weight?user_id=123
Authorization: Bearer {token}
```

[
  {"date": "2025-07-01", "weight": 140},
  {"date": "2025-07-08", "weight": 137.5},
  {"date": "2025-07-15", "weight": 135}
]

---

### 🔹 `docs/endpoints/goals.md`

```markdown
# Goals

## POST /goals

Set a new fitness goal.

```json
{
  "user_id": "123",
  "goal_type": "weight_loss",
  "target_weight": 125,
  "deadline": "2025-08-31"
}
```

## GET /goals?user_id=123
{
  "goal_type": "weight_loss",
  "target_weight": 125,
  "current_weight": 135,
  "progress": "80%",
  "deadline": "2025-08-31"
}

---

### 🔹 `docs/errors.md`

```markdown
# Error Handling

The API uses standard HTTP status codes. Error responses include a message field.

**Example**

```json
{
  "error": "Unauthorized",
  "message": "Token is missing or invalid"
}
```


---

### 🔹 `examples/curl-requests.md`

```markdown
# Example cURL Requests

## Log a Workout

```bash
curl -X POST https://api.fittrackapp.com/v1/workouts \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "123",
    "type": "strength",
    "duration_minutes": 45,
    "calories_burned": 300
  }'
```

## Get Progress
curl https://api.fittrackapp.com/v1/progress/weight?user_id=123 \
  -H "Authorization: Bearer YOUR_TOKEN"


---

### 🔹 `examples/python-client.md`

```python
import requests

BASE_URL = "https://api.fittrackapp.com/v1"
TOKEN = "YOUR_API_TOKEN"

headers = {
    "Authorization": f"Bearer {TOKEN}",
    "Content-Type": "application/json"
}

def get_weight_progress(user_id):
    r = requests.get(f"{BASE_URL}/progress/weight", headers=headers, params={"user_id": user_id})
    return r.json()

print(get_weight_progress("123"))

