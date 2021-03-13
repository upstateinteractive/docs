# Nexus Guide
- has roles, events, artifacts, and rules that bind them
- for more than one Scrum Team using the shared Product Backlog
- concept of Integrated Increment

## Dependencies that arise between the work of multiple teams
1. Requirements
2. Domain Knowledge
3. Software and test artifacts

## Roles
- a nexus has 1 Nexus Integration Team and 3-9 scrum teams

### Nexus Integration Team 
- consists of The Product Owner, A Scrum Master, Nexus Integration Team Members. Coordinates, coaches, and supervises. 
- often integration team members are on scrum teams
- their work priority is to the integration team first, scrum team second
- composition of team changes over time
- activities:  coaching, consulting, and highlighting, awareness of dependencies. might also perform work from Product Backlog
- they resolve constraints that may impede a Nexus' ability to delivery a constantly Integrated increment

#### Product Owner in Nexus Integration Team
- There is a single Product Owner in the Nexus
- same as in scrum, singularly responsible for Product Backlog

#### Scrum Master
- the scrum master may also be in one or more scrum teams
- has overall responsibility for ensuring Nexus is understood and enacted

#### Nexus Integration Team Members
- professionals who are generally skilled in systems engineering
- ensure teams have tools to identify dependencies and tools needed to integrate all artifacts according to definition of "done"
- responsibile for coaching and guiding team members to use the integration tools
- also maintains architectural standards, infrastructural standards, required by organization to ensure the development of quality integrated Increments
- if their primary duty is satisfied they may work in one or more Scrum Teams

## Artifacts
Product Backlog
- all scrum teams manage the product backlog
- granularity to 'thinly sliced' functionality
- a PB item is Ready when a Scrum Team can select it with no or minimal dependencies with other Scrum Teams

Nexus Sprint Backlog
- all scrum teams maintain their individual Sprint Backlogs
- this one exists to assist with transparency during the sprint

Integrated Increment
- sum of all integrated work done by a Nexus
- must meet definition of "Done"
- inspected at Nexus Sprint Review

## Events
- Sprint Review is replaced by Nexus Sprint Review 
- Other events are appended to or placed around regular scrum events to augment them

### Refinement
### Nexus Sprint Planning
- best to have all members of all scrum teams
- its completed when every scrum team has completed their individual sprint planning event

### Nexus Sprint Goal
- the sum of all work and sprint goals
- goal should be met by nexus sprint review

### Nexus Daily Scrum
- includes representatives from each team
- used to inspect integrated increment progress
- asks three questions

### Nexus Sprint Review
- result is a revised product backlog
- provide feedback on Integrated Increment
- replaces individual Sprint Reviews

### Nexus Sprint Retrospective
- occurs after Nexus Sprint Review and after Nexus Sprint Planning
- three parts:
  1. make shared issues transparent across all Scrum Teams
  2. each scrum team holding their own Sprint Retrospective
  3. all scrum teams meet again and agree how to visualize and track the identified actions. For the whole Nexus to Adapt. 
- three subjects:
  1. Was any work left undone? Did the Nexus generate technical debt?
  2. Were all artifacts, particularly code, frequently (as often as every day) successfully integrated?
  3. Was the software successfully built, tested, and deployed often enough to prevent the overwhelming accumulation of unresolved dependencies?
- three follow up questions for each subject:
  1. Why did this happen?
  2. How can technical debt be undone?
  3. How can the recurrence be prevented?

## Process Flow
### Refine Product Backlog
- Product Backlog needs to be decomposed so Dependencies are identified and minimized 

### Nexus Sprint Planning
- representatives from each Scrum Team meet to discuss and review the refined PB. Outcome is a set of Sprint Goals that align with an overarching Nexus Sprint Goal

### Development Work
- all teams integrate into a common environment

### Nexus Daily Scrum
- each Scrum Team sends a representative. They identify any integration issues. They report back to each Scrum Team's Daily Scrum

### Nexus Sprint Review
- all individual Scrum Teams meet with stakeholders to review Integrated Increment

### Nexus Sprint Retrospective
- representatives from each Scrum Team meet to identify shared challenges. Then each individual Scrum Team meets to hold individual Retrospectives. Representatives from each team meet again to share bottom-up intelligence.

## Artifact Transparency
### DoD
- an integrated increment is releasable by a Product Owner
- an individual team can be more stringent in their DoD but not less stringent than the Nexus DoD

## End Note
> Nexus is free and offered in this Guide. As with the Scrum framework, the Nexus roles, artifacts, events, and rules are immutable. Although implementing only parts of Nexus is possible, the result is not Nexus.