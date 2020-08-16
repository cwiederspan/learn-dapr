# Learning Dapr

## Start up the Go Add application

```bash

# Get to the correct directory
cd src/go/

# Get the router that is used by the Go app
go get -u github.com/gorilla/mux

# Build the app
go build -o app app.go

# Run the app with Dapr
dapr run --app-id addapp --app-port 6000 --port 3503 --components-path ../components app

# Check the result through Dapr's CLI interface
dapr invokePost -a addapp -m add -p '{ "operandOne": "6", "operandTwo": "7" }'

# Check the result through a raw HTTP POST
curl -X POST --header "Content-Type: application/json" \
  --data '{"operandOne": "100", "operandTwo": "99"}' \
  http://localhost:3503/v1.0/invoke/addapp/method/add

```

## Start up the C# Subtract application

```bash

# Get to the correct directory
cd src/csharp/

# Setup an ENV variable
export ASPNETCORE_URLS="http://localhost:7000"

# Build the app
dotnet build

# Run the app with Dapr
dapr run --app-id subtractapp --app-port 7000 --port 3504 --components-path ../components dotnet ./bin/Debug/netcoreapp3.1/Subtract.dll

# Check the result through Dapr's CLI interface
dapr invokePost -a subtractapp -m subtract -p '{ "operandOne": "10", "operandTwo": "7" }'

```

## Start up the Node Divide application

```bash

# Get to the correct directory
cd src/node/

# Restore the NPM files
npm install

# Run the app with Dapr
dapr run --app-id divideapp --app-port 4000 --port 3502 --components-path ../components node app.js

# Check the result through Dapr's CLI interface
dapr invokePost -a divideapp -m divide -p '{ "operandOne": "42", "operandTwo": "7" }'

```

## Start up the Python Multiply application

```bash

# Get to the correct directory
cd src/python/

# Restore the packages
pip3 install wheel python-dotenv flask flask_cors

# Setup an ENV variable
export FLASK_RUN_PORT=5000

# Run the app with Dapr
dapr run --app-id multiplyapp --app-port 5000 --port 3501 --components-path ../components flask run

# Check the result through Dapr's CLI interface
dapr invokePost -a multiplyapp -m multiply -p '{ "operandOne": "5", "operandTwo": "7" }'

```

## Start up the Front-end React application

```bash

# Get to the correct directory
cd src/react-calculator/

# Restore the NPM files
npm install

# Build the client app
npm run buildclient

# Run the app with Dapr
dapr run --app-id frontendapp --app-port 8080 --port 3500 --components-path ../components node server.js

```
