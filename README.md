## phase 4 week 1 code challenge##
This is a simple project of an API for tracking heroes and their superpowers. This README will guide you through the setup, models, validations, and routes needed to complete the challenge successfully.
Setup

## To get started, follow these steps to set up your development environment: ##

    Clone this repository to your local machine.

    Install the required dependencies for the frontend and backend:

    sh

pipenv install
npm install --prefix client

There is starter code in the app/seed.py file that you can use to create initial data for testing your application.

Run the Flask API on localhost:5555:

sh

python app.py

Run the React app on localhost:4000:

sh

npm start --prefix client

You can also run the included tests to check your work:

sh

    pytest -x

You have multiple options to check your progress:

    Run the tests using pytest -x and see if your code passes.
    Interact with the API via the React frontend.
    Use Postman to make requests to the Flask server.

**he frontend code is available to help you test your API in a realistic setting.**
Models

You need to create the following relationships in your database:

    A Hero has many Powers through HeroPower.
    A Power has many Heros through HeroPower.
    A HeroPower belongs to both a Hero and a Power.

  ## Follow these steps to get started ##

    Create the necessary models and migrations for the database tables as shown in the provided domain diagram (domain.png).

    Add any code required in the model files to establish the relationships.

    Run the migrations and seed the database with initial data:

    sh

    flask db upgrade
    python app/seed.py

If you encounter issues with the provided seed file, you can generate your own seed data to test the application.
Validations

add the following validations to the models to ensure data integrity
HeroPower Model:

    strength must be one of the following values: 'Strong', 'Weak', 'Average'.

Power Model:

    description must be present and at least 20 characters long.

Make sure to implement these validations to maintain data consistency in your application.
Routes

Set up the following routes in your Flask application. Ensure that each route returns JSON data in the specified format along with the appropriate HTTP verb.
GET /heroes

Return JSON data in the following format:

json

[
  { "id": 1, "name": "Kamala Khan", "super_name": "Ms. Marvel" },
  { "id": 2, "name": "Doreen Green", "super_name": "Squirrel Girl" },
  { "id": 3, "name": "Gwen Stacy", "super_name": "Spider-Gwen" }
]

GET /heroes/:id

If the Hero with the specified ID exists, return JSON data in the format below:

json

{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}

If the Hero does not exist, return the following JSON data along with the appropriate HTTP status code:

json

{
  "error": "Hero not found"
}

GET /powers

Return JSON data in the format below:

json

[
  {
    "id": 1,
    "name": "super strength",
    "description": "gives the wielder super-human strengths"
  },
  {
    "id": 2,
    "name": "flight",
    "description": "gives the wielder the ability to fly through the skies at supersonic speed"
  }
]

GET /powers/:id

If the Power with the specified ID exists, return JSON data in the format below:

json

{
  "id": 1,
  "name": "super strength",
  "description": "gives the wielder super-human strengths"
}

If the Power does not exist, return the following JSON data along with the appropriate HTTP status code:

json

{
  "error": "Power not found"
}

PATCH /powers/:id

This route should update an existing Power. It should accept an object with the following properties in the body of the request:

json

{
  "description": "Updated description"
}

If the Power exists and is updated successfully (passes validations), update its description and return JSON data in the format below:

json

{
  "id": 1,
  "name": "super strength",
  "description": "Updated description"
}

If the Power does not exist, return the following JSON data along with the appropriate HTTP status code:

json

{
  "error": "Power not found"
}

If the Power is not updated successfully (does not pass validations), return the following JSON data along with the appropriate HTTP status code:

json

{
  "errors": ["validation errors"]
}

POST /hero_powers

This route should create a new HeroPower associated with an existing Power and Hero. It should accept an object with the following properties in the body of the request:

json

{
  "strength": "Average",
  "power_id": 1,
  "hero_id": 3
}

If the HeroPower is created successfully, send back a response with the data related to the Hero:

json

{
  "id": 1,
  "name": "Kamala Khan",
  "super_name": "Ms. Marvel",
  "powers": [
    {
      "id": 1,
      "name": "super strength",
      "description": "gives the wielder super-human strengths"
    },
    {
      "id": 2,
      "name": "flight",
      "description": "gives the wielder the ability to fly through the skies at supersonic speed"
    }
  ]
}

If the HeroPower is not created successfully, return the following JSON data along with the appropriate HTTP status code:

json

{
  "errors": ["validation errors"]
}


