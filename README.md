## uml: sequence diagram

### Add User (Mentee)

```plantuml
@startuml
Participant Client
Participant Lambda
Participant "DynamoDB (User)"
Participant "DynamoDB (MentorProfile)"
Participant "DynamoDB (Recommendations)"


' Participant OpenAI
' Participant Secrets
' Participant Pinecone
' Participant EventBridge

Client -> Lambda: Add user
Note left of Lambda: User data in JSON
Lambda -> "DynamoDB (User)": Add user data to DB

"DynamoDB (User)" -> Lambda: Confirmation (User added)

Lambda -> "DynamoDB (MentorProfile)": fetch mentors
"DynamoDB (MentorProfile)" -> Lambda : mentors' profiles

Lambda -> "DynamoDB (Recommendations)": Assign mentors to added user
@enduml
```

### Get User (Mentee)

```plantuml
@startuml
Participant Client
Participant Lambda
Participant "DynamoDB (User)"
' Participant "DynamoDB (MentorProfile)"
Participant "DynamoDB (Recommendations)"


' Participant OpenAI
' Participant Secrets
' Participant Pinecone
' Participant EventBridge

Client -> Lambda: Get user
Note left of Lambda: userId
Lambda -> "DynamoDB (User)": mentee's userId

"DynamoDB (User)" -> Lambda: mentee's profile

' Lambda -> "DynamoDB (MentorProfile)": fetch mentors
' "DynamoDB (MentorProfile)" -> Lambda : mentors' profiles

Lambda -> "DynamoDB (Recommendations)": mentee's userId
"DynamoDB (Recommendations)" -> Lambda : mentee's recommended mentors

@enduml
```

### Add User (Mentor)

```plantuml
@startuml
Participant Client
Participant Lambda
Participant "DynamoDB (User)"
Participant "DynamoDB (MentorProfile)"
Participant "DynamoDB (Recommendations)"




Client -> Lambda: Add user
Note left of Lambda: User data in JSON
Lambda -> "DynamoDB (User)": Add user data to DB

"DynamoDB (User)" -> Lambda: Confirmation (User added)

Lambda -> "DynamoDB (MentorProfile)": fetch mentors
"DynamoDB (MentorProfile)" -> Lambda : mentors' profiles

Lambda -> "DynamoDB (Recommendations)": Assign mentors to all user
@enduml
```

### Get User (Mentor)

```plantuml
@startuml
Participant Client
Participant Lambda
Participant "DynamoDB (User)"
Participant "DynamoDB (MentorProfile)"
Participant "DynamoDB (Recommendations)"


Client -> Lambda: Get user
Note left of Lambda: userId
Lambda -> "DynamoDB (User)": mentor's userId

"DynamoDB (User)" -> Lambda: mentee's profile
@enduml
```


### Weekly Trigger

```plantuml
@startuml
Participant EventBridge
Participant Lambda
Participant "DynamoDB (User)"
Participant "DynamoDB (MentorProfile)"
Participant "DynamoDB (Recommendations)"




EventBridge -> Lambda: Trigger
' Lambda -> "DynamoDB (User)": Add user data to DB

' "DynamoDB (User)" -> Lambda: Confirmation (User added)

Lambda -> "DynamoDB (User)": fetch users
"DynamoDB (MentorProfile)" -> Lambda : mentee' profiles

Lambda -> "DynamoDB (MentorProfile)": fetch mentors
"DynamoDB (MentorProfile)" -> Lambda : mentors' profiles

Lambda -> "DynamoDB (Recommendations)": Assign mentors to all user
@enduml
```


<!-- ```
' Participant OpenAI
' Participant Secrets
' Participant Pinecone
' Participant EventBridge
' Lambda -> OpenAI: Send text for embedding
' OpenAI -> Lambda: Return embeddings
' Lambda -> Secrets: Retrieve API keys or credentials
' Secrets -> Lambda: Provide API keys or credentials
' Lambda -> Pinecone: Store/retrieve embeddings
' Pinecone -> Lambda: Return embeddings based on userid
' Lambda -> EventBridge: Trigger events
```
  


```plantuml
@startuml
Participant Client
Participant Lambda
Participant DynamoDB
' Participant OpenAI
' Participant Secrets
' Participant Pinecone
' Participant EventBridge

Client -> Lambda: Add user
Lambda -> DynamoDB: Add user data to DB
' Lambda -> OpenAI: Send text for embedding
' OpenAI -> Lambda: Return embeddings
' Lambda -> Secrets: Retrieve API keys or credentials
' Secrets -> Lambda: Provide API keys or credentials
' Lambda -> Pinecone: Store/retrieve embeddings
' Pinecone -> Lambda: Return embeddings based on userid
' Lambda -> EventBridge: Trigger events
@enduml
``` -->


