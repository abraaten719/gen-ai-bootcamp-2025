# Backend Server Technical Specs

## Business Goal: 
A language learning school wants to build a prototype of learning portal which will act as three things:
- Inventory of possible vocabulary that can be learned
- Act as a  Learning record store (LRS), providing correct and wrong score on practice vocabulary
- A unified launchpad to launch different learning apps

## Technical Requirements

- The backend will be built using Go
- The database will be SQLite3
- The API will be built using Gin
- The API will always return JSON
- There will be no authentication or authorization
- Everything will be treated as a single user

## Database Schema

Our database will be a single sqlite database called `words.db` that will be in the root of the project folder of `backend_go`

We have the following tables:
- words - stored vocabulary words
    - id interger
    - japanese word string
    - ramaji string
    - english string
    - parts json

- words_groups - join table for words and groups (many-to-many)
    - id integer
    - word_id integer 
    - group_id integer 
    
- groups - thematic groups of words
    - id integer 
    - name string

- study_sessions - records of study sessions grouping word_review_items
    - id integer 
    - group_id integer
    - study_activitiy_id integer
    - created_at datetime

- study_activities - a specific study activity, linking a study session to group
    - id integer 
    - study_session_id integer 
    - group_id integer 
    - created_at datetime

- word_review_items - a record of word practice, determining if the word was correct or not
    - study_session_id integer 
    - word_id integer 
    - correct boolean
    - created_at datetime

## API Endpoints

### GET /api/dashboard/last_study_session

**Response:**
```json
{
  "id": 1,
  "activity_name": "Vocabulary Practice",
  "created_at": "2025-03-01T12:00:00Z",
  "study_activity_id": 789,
  "group_id": 456,
    "group_name": "Basic Greetings"
}
```

### GET /api/dashboard/study_progress

**Response:**
```json
{
  "total_words_studied": 3,
  "total_available_words": 124,
}
```

### GET /api/dashboard/quick-stats

**Response:**
```json
{
  "success_rate": "80%",
  "total_study_sessions": 4,
  "total_active_groups": 3,
  "study_streak": "4 days"
}
```

### POST /api/study_activities

**Request:**
```json
{
  "group_id": 1,
  "study_activity_id": 234
}
```
**Response:**
```json
{
  "id": 1,
  "group_id": 234,
}
```
    - required params: group_id, study_activity_id
### GET /api/study_activities/:id

**Response:**
```json
{
  "id": 1,
  "name": "Vocabulary Practice",
  "thumbnail": "url_to_thumbnail",
  "description": "Practice vocabulary words",
  "created_at": "2025-03-02T12:00:00Z"
}
```

### GET /api/study_activities/:id/study_sessions

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "activity_name": "Vocabulary Practice",
      "group_name": "Beginner",
      "start_time": "2025-03-01T12:00:00Z",
      "end_time": "2025-03-01T12:30:00Z",
      "number_of_review_items": 12
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 5,
    "total_items": 100,
    "items_per_page": 20
  }
}
```

### GET /api/words
    - pagination with 100 items per page

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "japanese": "こんにちは",
      "romaji": "konnichiwa",
      "english": "hello",
      "correct_count": 5,
      "wrong_count": 1
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 10,
    "total_items": 500,
    "items_per_page": 100
  }
}
```

### GET /api/words/:id

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "japanese": "こんにちは",
      "romaji": "konnichiwa",
      "english": "hello",
      "correct_count": 5,
      "wrong_count": 1
    }
  ],
  "groups": [
    {
        "id": 1,
        "name": "Basic Greetings"
    }
  ]
}
```

### GET /api/groups
    - pagination with 100 items per page

**Response:**
```json
{
  "groups": [
    {
      "id": 1,
      "name": "Beginner",
      "word_count": 50
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 1,
    "total_items": 50,
    "items_per_page": 100
  }
}
```

### GET /api/groups/:id

**Response:**
```json
{
  "id": 1,
  "name": "Beginner",
  "total_words": 50
}
```

### GET /api/groups/:id/words

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "japanese": "こんにちは",
      "romaji": "konnichiwa",
      "english": "hello",
      "correct_count": 5,
      "wrong_count": 1
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 1,
    "total_items": 5,
    "items_per_page": 100
  }
}
```

### GET /api/groups/:id/study_sessions

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "activity_name": "Vocabulary Practice",
      "group_name": "Beginner",
      "start_time": "2025-03-01T12:00:00Z",
      "end_time": "2025-03-01T12:30:00Z",
      "number_of_review_items": 12
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 1,
    "total_items": 5,
    "items_per_page": 100
  }
}
```

### GET /api/study_sessions
    - pagination with 100 items per page

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "activity_name": "Vocabulary Practice",
      "group_name": "Beginner",
      "start_time": "2025-03-01T12:00:00Z",
      "end_time": "2025-03-01T12:30:00Z",
      "number_of_review_items": 12
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 1,
    "total_items": 5,
    "items_per_page": 100
  }
}
```

### GET /api/study_sessions/:id

**Response:**
```json
{
  "id": 1,
  "activity_name": "Vocabulary Practice",
  "group_name": "Beginner",
  "start_time": "2025-03-01T12:00:00Z",
  "end_time": "2025-03-01T12:30:00Z",
  "number_of_review_items": 12
}
```

### GET /api/study_sessions/:id/words

**Response:**
```json
{
  "items": [
    {
      "id": 1,
      "japanese": "こんにちは",
      "romaji": "konnichiwa",
      "english": "hello",
      "correct": true,
      "reviewed_at": "2025-03-01T12:15:00Z"
    }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 1,
    "total_items": 5,
    "items_per_page": 100
  }
}
```

### POST /api/reset_history

**Response:**
```json
{
  "status": "success",
  "message": "History reset successfully"
}
```

### POST /api/full_reset

**Response:**
```json
{
  "status": "success",
  "message": "Full reset successfully"
}
```

### POST /api/study_sessions/:id/word_id/review
    - required params: correct

**Request:**
```json
{
  "correct": true
}
```
**Response:**
```json
{
  "success": true,
  "word_id": 1,
  "study_session_id": 123,
  "correct": true,
  "created_at": "2025-03-02T12:00:00Z"
}
```

## Mage (Tasks)

Mage is a task runner for Go. 
Lets list out possible tasks we need for our lang portal.

### Initialize Database
This task will initialize the sqlite database called `words.db`

### Migrate Database
This task will run a series of migrations sql files on the database

Migrations will live in the `migrations` folder.
The migration files will be run in order of their file name.
The file names should look like this:

```sql
0001_init.sql
0002_create_words_table.sql
```

### Seed Data
This task will import json files and transform them into target data for our database

All seed files live in the `seeds` folder.

In our task we should have DSL to specific each seed file and its expected group word name.

[
  {
    "id": 1,
    "japanese": "こんにちは",
    "romaji": "konnichiwa",
    "english": "hello",
    "parts": {
      "part_of_speech": "greeting"
    }
  },
  {
    "id": 2,
    "japanese": "ありがとう",
    "romaji": "arigatou",
    "english": "thank you",
    "parts": {
      "part_of_speech": "expression"
    }
  }
]

