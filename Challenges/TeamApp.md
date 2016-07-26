# Overview
A team application should be the digital equivalent of the information package / tournament booklet combined with team specific information. Optionally this can include live updates from the other modules like scoring, schedueling. The target audience is maily the teams, couches and parents, but also an information channel to general visitors. An example is the US FIRST Championship app. http://www.firstchampionship.org/event-app

The initial implementation could be a mobile website served from a local host, available during the event itself. But in the future this could be packaged and deployed on a webserver so the information is also available before and after the event. 

# Team App elements


# Functions

## Information
The majority of the informatino would be added by the tournament organizer before the event. This 'static' information contains general information about the events that won't change (much) during the event. I.e. all information that is normally printed and handed out to teams. 

### General information
An organizer should be able to enter the information for an event; and should be able to use rich text, hyperlinks and include images and upload PDFs. In addition to preset categories, organizers might create some additional pages specific for their event. The 'standard' information could include (in random order):

* _What is the FIRST LEGO League_: could potentially be pre-filed with standard text from marketing.
  * _Game rules_: judging and robot game for this season
  * _Awards_: what awards will be handed out at this event, what criteria
* _Event information_: information related to this event
  * _General Schedule_: the global schedule of the event
  * _Layout/maps_: Maps of the venue and pit area
  * _Contact information_: for general help, for emergencies
* _Side events_: what else is there to do at the event, where
* _Frequently asked questions_: for teams, for public, for volunteers
* _Sponsors_: show the sponsors of the event (potentially in different categories: gold, silver, bronze)
* _Volunteers_: recongition of volunteers at the event
* _Social media channels_: Links to twitter account/hashtags, facebook page etc

### Team info:
In addition to the general information, there is some information specific to the team. For this information has to added about the teams, or -in time-  can be pulled from other modules. In any case, the user will need to select which team they want the information for. 

* _team list_: What teams are attending and where are they located
* _My team info_: Pit area number/location, team number, team name, contact details. Include link to pit admin if incorrect.
* _Team scheduele_: the specific time table for the team, potentialy with notifications about upcoming events. 
* _Practive table_: Link to practice reservation system

### Dynamic info:
In addition to the static information; there  is information that will be updated  during the event. This information can be added by the organizer to the app, or being pulled from other modules. This information includes for example:

* _Notifications_: event specific updates, for example about the start of ceremonies (applies to all users)
* _Scores / rubrics / results_: the scores for the specific teams, and optionally award results (from scoring and judging module)

### Interactions
Besides information, the appplication can also enable teams and users to actively connect and engage. For example through social media.

* _Share content_: (results, personal schedule etc) to social media.
* _Engage_: with other teams, for example through team information.

# Interface
The entered information would be accessable by teams on a variety of devices, including mobile phones and tablets. One solution would be to use a repsonsive design for a mobile website. There will be three main users: the event organizer (putting in information), the the general users looking for event information, and the teams looking also for their own information

## Admin
* Show / hide certain sections if not used at the event
* Add additional pages to the general information
* Add notifications during the event to be send to all users

## General user
* Open mobile website
* Navigate on different mobile devices
* Bookmar site

## Teams / coach
* Select their own team from a list
* If selected different landing page (for example own schedule)

# Other requirements
* Local/Multi-language support
* Own branding (logo), colors
* Easy to access (clear landing page)

# API

## Get information:
* Obtain team information from the team adminstration
* Link to schedule module to obtain latest schedule information
* Link to practice table reservation system with own team number
* Receive notification from display system?

## Send information/Triggers
* 

#TODOS
* Discuss how to make the mobile site available to a large number of users, either using local services /network or a cloud solution. 
* Make the app/mobile site available before and after the event (related to previous point)
