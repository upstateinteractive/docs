# And Sails was Good.

## Intro
Sails is Ruby On Rails for JavaScript.  
  
We use Sails as our rapid API prototyping framework of choice.  
  
In here we have our thoughts, opinions, and findings for Sails.  

## Table of Contents
1. [Limitations](#limitations)  

### Limitations
#### No Foreign Key Contraints 
Waterline - the default ORM that ships with Sails - does not build Foreign Key Constraints on tables when you're writing one-to-many relationships. Our untested but promising solution would be to, when the time is right, use [sails-hook-sequelize](https://www.npmjs.com/package/sails-hook-sequelize) to swap out Waterline for Sequelize.

