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

@en