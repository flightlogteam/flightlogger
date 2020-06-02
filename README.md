# A better flightlogger
flightlog.org is a great site. This project is a modern implementation of that webpage with a similar data-model, written in golang

# Architecture
Here we use a layered model in order to ensure security. The backend API will basically have two layers

### Frontend
- Angular Cli (coming soon)

### Backend
- Presentation-layer
- Business (UseCase)
- Datalayer

# Project setup

## Dependencies
* golang
* git

Please also set the GOHOME environment variable should be $HOME/go

## Project setup
1. `go get github.com/klyngen/flightlogger`. 
2. Generate certificates 
```bash
openssl genrsa -out fly.rsa 2048
openssl rsa -in app.rsa -pubout > fly.rsa.pub
```
3. Migrate the database...
4. Add configuraion preferrably to $HOME/.flightlogger/flightlog.yaml
```yaml
serverport: "61225"
publicKeyPath: "$HOME/.flightlogger/fly.rsa.pub"
privateKeyPath: "$HOME/.flightlogger/fly.rsa"
# Expiration in seconds
tokenexpiration: 3600

database:
   hostname: "canbeempty"
   password: "dbpassword"
   port: "canbeempty"
   username: "dbuser"
   database: "Flightlog"
```

5. `go run main.go`

# Contributions
All help is appreciated. Send me an email if you wonder how you can contribute or just make a PR. All contributors will be given access to a full JetBrains-software-package and will be given out to anyone who proves themselves by contributing.

## Guidelines
- Ensure that the API is easy to use. Please reed [this guide](https://blog.florimond.dev/restful-api-design-13-best-practices-to-make-your-users-happy)
- **Write tests** the application is layered for a reason....
- Be nice :) 



**Check out our board on [taiga.io](https://tree.taiga.io/project/klyngen-better-flightlog/timeline)**

# Authorization
Flightlogger uses **A**ttribute-**B**ased-**A**ccess-**C**ontrol to control access to resources. Resources are defined in the database.

## Goals for access-control
The main goals is to ensure that we can get a hierarchy of access and allowing users to state if they want their information to be public or not, and the possibility to allow certain users to access a profile; what we have learned to expect from social media. Access-control should also be efficient and casbin rules should be kept to a minimum. 
