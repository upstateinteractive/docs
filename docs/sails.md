# And Sails was Good.

## Intro
Sails is Ruby On Rails for JavaScript.  
  
We use Sails as our rapid API prototyping framework of choice.  
  
In here we have our thoughts, opinions, and findings for Sails.  

## Table of Contents
1. [Sails Setup](#setup)
2. [Generate an API](#generate-an-api)
3. [Helpers](#helpers)
4. [Limitations](#limitations)  

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

### Helpers
```bash
sails generate helper makeFoo
```

#### General
- Helpers replace services and add more structure to the code
- This involves typechecking for values, description settings for function clarification/comments, and a defaultTo value that provides as a fail safe
- Helpers will only work if the coder is proactive in documentation. Because of the need to define every value that enters and exits the function, a poorly thought out helper will result to confusing legacy code and a weakened logging system
-It would be useful to know about [how async functions work](https://www.youtube.com/watch?v=568g8hxJJp4&t=98s)


#### Anatomy of a Helper
A helper starts out with a `module.exports` wrapper that includs a  `friendlyName: ` and `description: ` field. For sake of organization, please name friendlyName as the file name itself. Try a verb and a Noun to clarify what the purpose of the code is. Examples include `friendlyName: fetchArticles` or `friendlyName: queryItunesAPI`. The  `description` field allows for further commmenting.

1. `inputs:` An object that clarifies what function arguments are needed.
  ```
  module.exports = {
    inputs : {
      userId: {
        friendlyName: 'user Id from user model',
        description: 'used to identify user',
        type: 'number'
      },
      productSerialNum: {
        friendlyName: 'wine cooler serial number',
        description: 'identify user product item',
        type: 'string',
        defaultsTo: 'SE934304'
      }
    }
  }
  ```
 This includes fields such as:
  - `friendlyName:` a friendly name
  - `description`: what does this function do
  - `extendedDescription`: any additional details that are not necessary but helpful. Any gotchas?
  - `type`: this field is particularly useful! While sails does not provide a list of types, examples include number and string. This field helps whoever using the helper function identify arguments entering and exiting function
  - `defaultsTo`: another useful field to help automate some of the work. Example: If helper function user does not provide the amount of articles needed, automatically defaultTo ten articles
2. `Exits:` An object that clarifies what exits the function. General defining a successful exit with `success` would suffice and should be the practice for all helper functions. The interesting part is the branching of errors. A good way to track errors would lead to less debugging headaches in the future! Example:
  ```
  exits: {
    success : {
      outputFriendlyName: 'Product information',
      outputDescription: 'Information including distribution, availability, created year',
      type: 'object'
    },

    missingInput : {
      outputFriendlyName: 'missing argument',
      outputDescription: 'Must provide user Id and product serial number'
    },

    retrievalError : {
      outputFriendlyName: 'database error',
      outputDescription: 'Error querying model User or Product'
  }
  ```

3. `fn`: The meat of the helper function, this is replaced with the async await syntax. The function definition requires two arguments: `inputs` and `exits`. Inputs/exits are what are defined earlier. In order to access input property, simply follow `inputs.foo`. The same goes with `exits.success(result)`
```
  async function doEverything(input, exits) {
    //async func A
    //async func B
    //async func C
    if(//something failed!) {
      throw 'retrievalError'
    }
    return exits.success()
  }
```

#### Calling the Helper function
1. Passing no arguments: `sails.helpers.exampleHelper` would rely on default settings
2. Passing multiple arguments: `sails.helpers.exampleHelper(1, 'productSerial')` would separate arguments with comma
3. Chaining: using a 'with' keyword, pass in an object that identifies the value and argument; This is the best practice because it translates to clearer code. Chaining also involves error handling. This includes adding a `.intercept()` or `.tolerate()`. Because of the well defined exit errors, you can then further tailor actions to it.
  ```
    sails.helpers.example-helper.with({
      userId: 1,
      productSerial: 'SE29282'
    }).intercept('missingInput', () => {
      sails.log('Missing input field! Please ensure all inputs are entered or include defaultTo value')
    })
  ```

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

