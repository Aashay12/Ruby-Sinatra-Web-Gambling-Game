# Ruby-Sinatra-Web-Gambling-Game (COEN_278)

This code is a Sinatra application that implements a simple web-based dice betting game with user registration and login functionality. Here's a breakdown of its main features and functionality:

Database Setup: The code uses DataMapper, an Object-Relational Mapping (ORM) library, to set up a connection to a SQLite database. It defines the default database location as mydb.db in the current working directory. 

Environment Configuration: The code includes configurations for both the development and production environments. In the development environment, the default SQLite database is used. In the production environment, the DATABASE_URL environment variable is used to determine the database connection details.

# Routes:

- The root route (get '/') renders an ERB template called "login", which presumably contains a login form.

## The '/signup' route (post '/signup') handles the form submission for user registration.
- It checks if a user with the given username already exists in the database. If not, a new user is created with the provided username, password, and initial values for win, loss, and profit. If the username is already taken, a message is displayed, and the user is redirected back to the signup form.

## The '/login' route (post '/login') handles the form submission for user login. 
- It checks if a user with the given username exists and if the provided password matches the stored password. If the login is successful, the user's name is stored in the session, and they are redirected to '/users'. If the login fails, an error message is displayed, and the user is redirected back to the login form.

## The '/bet' route (post '/bet') handles the form submission for the dice betting game. 
- It receives the user's bet amount and chosen number, generates a random number between 1 and 6 (representing the roll of a dice), and compares it with the chosen number. If they match, the user wins and their session variables for win, profit, totalWin, and totalProfit are updated accordingly. If they don't match, the user loses, and their session variables for loss, profit, totalLoss, and totalProfit are updated. A message is displayed indicating the outcome of the bet, and the user is redirected back to the '/bet' route.

## The '/logout' route (post '/logout') handles user logout. 
- It updates the total win, loss, and profit values for the user in the database, clears the session variables related to login, and redirects the user back to the root route ('/').

## Helper Method: The save_session method is a helper function used to update and save session variables. It takes a parameter name and a money amount. It retrieves the current value of the session variable (or 0 if it doesn't exist), adds the money amount to it, and saves the updated value back to the session.

## Error Handling: The not_found block handles any routes that are not defined in the application and returns the "Page not found" message.

Overall, this code sets up a web application for user registration, login, and a simple dice betting game where users can place bets and see their win/loss statistics.
