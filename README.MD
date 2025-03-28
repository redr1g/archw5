## How to run
Go to `https://openrouter.ai/`, log in, create your API key. Place it to business_logic folder in .env file

Then run the following command being in the same directory where **docker-compose.yaml** is located \

`docker compose up`
 
Check 
- `http://localhost:8000/` - for the business logic entrypoints
- `http://localhost:8001/` - for the database entrypoints
- `http://localhost:8002/` - for the customer service logic

`http://localhost:8002/ask` is the main post request. It asks a question from Deepseek v3-0324.
Your bearer token should be the same in your request as in .env file (**secret_token** for a simpler usage) and have the following json body:

{ \
    "input_text": "What is the capital of Ukraine?" \
}
 
The question is then processed by the client service. If your token is valid, the question is sent to database to check if this question was asked previously. If so, return the answer from cache; send new request (`/process`) to business_logic otherwise. In the end, new question is saved in the db and printed for user (along with the source of answer - cached or business logic).

***Client -> Client Service -> Database -> Business Logic -> Database -> Client***

### Output example for business logic source
![Alt text](business_logic.png?)



### Output example for cached source
![Alt text](cached.png?)
