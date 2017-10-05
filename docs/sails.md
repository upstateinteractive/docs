# And Sails was Good.

## Intro
Sails is Ruby On Rails for JavaScript.  
  
We use Sails as our rapid API prototyping framework of choice.  
  
In here we have our thoughts, opinions, and findings for Sails.  

## Table of Contents
1. [Sails Setup](#setup)
2. [Generate an API](#generate-an-api)
3. [Limitations](#limitations)  

### Setup
#### Install Sails
If you've never used Sails, you first need to install it
```bash
npm install sails -g
``` 

#### Create Your App
`cd` into your directory to generate a new app
```bash
sails new test-project
```  

View the app
```bash
cd test-project
sails lift
```

### Generate an API
```bash
sails generate api your-api
``` 
This will create two files: a model and contoller

### Configure Settings
#### Database
Go to the `config/connections.js` to set database connection. 
To use default local database:
```bash
localDiskDb: {
  adapter: 'sails-disk'
}
```

#### Models
Go to the `config/models.js` file to set model configurations. 
```bash
module.exports.models = {
  connection: 'localDiskDb',
  migrate: 'alter'
};
``` 

### Limitations
#### No Foreign Key Contraints 
Waterline - the default ORM that ships with Sails - does not build Foreign Key Constraints on tables when you're writing one-to-many relationships. Our untested but promising solution would be to, when the time is right, use [sails-hook-sequelize](https://www.npmjs.com/package/sails-hook-sequelize) to swap out Waterline for Sequelize.

