# Frontend Technical Specs

## Pages

### Dashboard '/dashboard'

#### Purpose
The purpose fo this page is to provide a summary of learning 
and act as the default page when a user visits the web-app

#### Components
    - Last Study Session
        - shows last activity used
        - shows when last activity used
        - summarizes wrong vs correct from last activity
        - has a link to the group

    - Study Progress
        - total words studied eg. 3/124
            - across all study session show the total words studied out of all possible words in our database
        - display a mastery progress eg. 0%

    - Quick Stats
        - success rate eg. 80%
        - total study sessions eg. 4
        - total active groups eg. 3
        - study streak eg. 4 days

    - Start Studying Button
        - goes to study activities page

#### Needed API endpoints
- GET /api/dashboard/last_study_session
- GET /api/dashboard/study_progress
- GET /api/dashboard/quick-stats

### Study Activities '/study_activities'

#### Purpose
The purpose of this page is to show a collection
of study activities with a thumbnail and its name, to either launch
or view the study activity. 

#### Components
- Study Activity Card
    - show a thumbnail of the study activity
    - the name of the study activity
    - a launch button to take us to the launch page 
    - the view page to view more information about past study
    sessions for this study activity

#### Needed API endpoints
- GET /api/study_activities
    
### Study Activity show '/study_activities/:id'

#### Purpose
The purpose of this page is to show the details of a study
activity and its past study sessions.

#### Components
    - Name of study activity
    - Thumbnail of study activity
    - Description of study activity
    - Launch button
    - Study Activities Paginated List
        - id
        - activity name
        - group name
        - start time
        - end time (inferred by the last word_review_item submitted)
        - number of review items

#### Needed API endpoints
- GET /api/study_activities/:id
- GET /api/study_activities/:id/study_sessions

### Study Activities '/study_activities/:id/launch'

#### Purpose
The purpose of this page is to launch a study activity.

#### Components
    - Name of study activity
    - Launch form
        - select field for group
        - launch now button

## Behaviour
After the form is submited a new tab opens with the 
study activity based on its url provided in the database.

Also the after form is submitted the page will redirect to the study session show page

#### Needed API endpoints
- POST /api/study_activities/

### Words Index '/words'

#### Purpose
The purpose of this page is to show all words in our database.

#### Components
- Paginated Word List
    - Columns
        - Japanese
        - Romaji
        - English
        - Correct Count
        - Wrong Count
    - Pagination with 100 items per page
    - Clicking the Japanese word will take us to the word show page

#### Needed API endpoints
- GET /api/words

### Word Show Page '/words/:id'

#### Purpose
The purpose of this page is to show information about a specific word.

#### Components
    - Japanese
    - Romaji
    - English
    - Study Statistics
        - Correct Count
        - Wrong Count
    - Word Groups 
        - show in a series of pills eg. tags 
        - when group name is clicked it will take us to the group show page

#### Needed API endpoints
- GET /api/words/:id

### Word Groups Index '/groups'

#### Purpose
The purpse of this page is to show a list of groups in our database. 

#### Components
- Paginated Group List
    - Columns
        - Group Name
        - Word Count
    - Clicking the group name will take us to the group show page


#### Needed API endpoints
- GET /api/groups

### Group Show Page '/groups/:id'

#### Purpose
The purpose of this page is to show detailed information about a specific group and its associated words.

#### Components
- Group Name
- Group Statistics
    - Total Words
- Words in Group
    - Paginated list of words in the group
    - (Should use the same component as the words index page)
    - Columns
        - Japanese
        - Romaji
        - English
        - Correct Count
        - Wrong Count
    - Clicking the Japanese word will take us to the word show page

- Study Sessions (Paginated List of Study Sessions)
    - Should use the same component as the study sessions index page


#### Needed API endpoints
- GET /api/groups/:id (the name and groups stats)
- GET /api/groups/:id/words
- GET /api/groups/:id/study_sessions

### Study Sessions Index '/study_sessions'

#### Purpose
The purpose of this page is to show a list of study sessions in our database.

#### Components
- Paginated Study Session List
    - Columns
        - Id
        - Activity Name
        - Group Name
        - Start Time
        - End Time
        - Number of Review Items
    - Pagination with 100 items per page
    - Clicking the study session id will take us to the study session show page

#### Needed API endpoints
- GET /api/study_sessions

### Study Session Show '/study_sessions/:id'

#### Purpose
The purpose of this page is to show detailed information about a specific study session.

#### Components
- Study Session Details
-   Activity Name
-   Group Name
-   Start Time
-   End Time
-   Number of Review Items

- Words Reviewed Items (Paginated List of Words)
    - Japanese
    - Romaji
    - English
    - Correct Count
    - Wrong Count

#### Needed API endpoints
- GET /api/study_sessions/:id
- GET /api/study_sessions/:id/words

### Settings Page '/settings'

#### Purpose
The purpose of this page is to allow users to reset history. 

#### Components
- Theme Selection eg. Light, Dark, System Default
- Reset History Button
    - This will delete all study sessions and word review items
- Reload Seed Data
    - This will drop all tables and re-create with seed data

#### Needed API endpoints
- POST /api/reset_history
- POST /api/full_reset

#### Purpose
#### Components
#### Needed API endpoints





----
### Study Activities '/study-activities'

#### Purpose
#### Components
#### Needed API endpoints
