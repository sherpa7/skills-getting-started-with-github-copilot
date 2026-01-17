# API Examples

This document provides practical examples of how to interact with the Mergington High School Activities API.

## Prerequisites

Make sure the server is running:
```bash
uvicorn src.app:app --reload
```

## Using curl

### Get All Activities

```bash
curl http://localhost:8000/activities
```

**Expected Response:**
```json
{
  "Chess Club": {
    "description": "Learn strategies and compete in chess tournaments",
    "schedule": "Fridays, 3:30 PM - 5:00 PM",
    "max_participants": 12,
    "participants": ["michael@mergington.edu", "daniel@mergington.edu"]
  },
  "Programming Class": {
    "description": "Learn programming fundamentals and build software projects",
    "schedule": "Tuesdays and Thursdays, 3:30 PM - 4:30 PM",
    "max_participants": 20,
    "participants": ["emma@mergington.edu", "sophia@mergington.edu"]
  },
  "Gym Class": {
    "description": "Physical education and sports activities",
    "schedule": "Mondays, Wednesdays, Fridays, 2:00 PM - 3:00 PM",
    "max_participants": 30,
    "participants": ["john@mergington.edu", "olivia@mergington.edu"]
  }
}
```

### Sign Up for an Activity

```bash
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=alice@mergington.edu"
```

**Expected Response:**
```json
{
  "message": "Signed up alice@mergington.edu for Chess Club"
}
```

### Sign Up for Programming Class

```bash
curl -X POST "http://localhost:8000/activities/Programming%20Class/signup?email=bob@mergington.edu"
```

### Try to Sign Up for Non-existent Activity (Error Case)

```bash
curl -X POST "http://localhost:8000/activities/Dance%20Club/signup?email=charlie@mergington.edu"
```

**Expected Response (404):**
```json
{
  "detail": "Activity not found"
}
```

## Using Python Requests

```python
import requests

BASE_URL = "http://localhost:8000"

# Get all activities
response = requests.get(f"{BASE_URL}/activities")
activities = response.json()
print(f"Available activities: {list(activities.keys())}")

# Sign up for an activity
email = "student@mergington.edu"
activity = "Chess Club"
response = requests.post(
    f"{BASE_URL}/activities/{activity}/signup",
    params={"email": email}
)
print(response.json())
```

## Using JavaScript (fetch)

```javascript
// Get all activities
fetch('http://localhost:8000/activities')
  .then(response => response.json())
  .then(data => console.log('Activities:', data))
  .catch(error => console.error('Error:', error));

// Sign up for an activity
const email = 'student@mergington.edu';
const activity = 'Chess Club';

fetch(`http://localhost:8000/activities/${encodeURIComponent(activity)}/signup?email=${email}`, {
  method: 'POST'
})
  .then(response => response.json())
  .then(data => console.log('Signup result:', data))
  .catch(error => console.error('Error:', error));
```

## Interactive API Documentation

The FastAPI framework provides interactive documentation:

- **Swagger UI**: http://localhost:8000/docs
  - Try out endpoints directly in your browser
  - See request/response schemas
  - Test error cases

- **ReDoc**: http://localhost:8000/redoc
  - Alternative documentation view
  - Printable format
  - Detailed schema information

## Testing Scenarios

### Scenario 1: New Student Registration Flow

1. Get list of activities
2. Choose an activity
3. Sign up with student email
4. Verify signup by getting activities again

```bash
# Step 1
curl http://localhost:8000/activities

# Step 2 & 3
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=newstudent@mergington.edu"

# Step 4
curl http://localhost:8000/activities | grep newstudent
```

### Scenario 2: Testing Duplicate Signup (Bug)

Currently, students can sign up multiple times for the same activity. This is a bug!

```bash
# First signup - should succeed
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=duplicate@mergington.edu"

# Second signup - currently succeeds but should fail
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=duplicate@mergington.edu"

# Verify the bug - you'll see the email listed twice
curl http://localhost:8000/activities | grep -A 5 "Chess Club"
```

**Exercise**: Use GitHub Copilot to fix this bug!

### Scenario 3: Edge Cases

Test various edge cases:

```bash
# Empty activity name
curl -X POST "http://localhost:8000/activities/%20/signup?email=test@mergington.edu"

# Special characters in email
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=test+special@mergington.edu"

# Very long email
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=verylongemailaddressthatshouldstillwork@mergington.edu"
```

## Common HTTP Status Codes

- **200 OK**: Successful GET request or signup
- **307 Temporary Redirect**: Root path redirects to static page
- **404 Not Found**: Activity doesn't exist
- **400 Bad Request**: Invalid request (e.g., duplicate signup after fix)
- **422 Unprocessable Entity**: Invalid parameters

## Tips for Testing

1. **Use the interactive docs**: Visit `/docs` for a user-friendly testing interface
2. **Check response headers**: Use `-v` flag with curl to see full response
3. **Pretty print JSON**: Pipe curl output through `jq` for formatted JSON
4. **Save responses**: Use `-o` flag to save responses to files

```bash
# Pretty print with jq
curl http://localhost:8000/activities | jq

# Verbose output
curl -v http://localhost:8000/activities

# Save to file
curl http://localhost:8000/activities -o activities.json
```
