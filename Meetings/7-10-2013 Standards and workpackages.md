# Meeting 7-10-2013

* Present: Rikkert, Martin, Sander, Bart, Kenny
* Point discussed:
	* Field definition
	* Work packages definition
	* Use-case scenarios:
		* Robustness, security
		* Communication
	* Next meeting
	
## Field definition file

We want to provide a challenge definition file to the program so organizers and teams can load a challenge, and with no need to redevelop the software for the next year. In addition we want to propose this as the international standard so other developers and users can benefit from it as well. In the meeting we discussed two proposals, JavaScript and XML definition as definition language. 

### General set-up
In both cases the definition file follows the following setup:
* Define the *observations*. These are the states observed by a referee, for example a chair repaired, a lever turned or number of elements placed. We can define the following types of observations:
	* Boolean: Observations that are either True or False, e.g. a object is touching an area
	* Enums: Observations that can have multiple states, e.g. a list of choices for example the truck is either area A, area B or Area C
	* Integers: Observations that can be counted, e.g. number of pins knocked down.
	* **Note/Discussion**: Can all observations be expressed as enums?
* Next we define *constraints*. These are the limitations that a observation has, for example the maximum number of pins or a value has to be selected.
* Then we define the *functions*. These are combinations of multiple observations (with their constraints) that jointly make up one score. Some of these conditions (for now) are:
	* *and* both conditions have to be true to score
	* *or* one of the conditions has to be true to score
	* *not* a condition has to be false in order to score
	* **Note/Discussion**: Please check and verify if this is correct
* Finally we define a *multiplier* for the various cases of the conditions, this can be used so the number of points can be calculated.

### JavaScript
Using JavaScript more power full functions can be written. This allows more flexibility to construct more complex missions. By combining definition and function, the JavaScript file is easily parsed by the application and can be quickly verified by the code for completeness. However reading the indention file is less clear to the untrained eye. Furthermore it limits the options for other developers to adopt the definition file.

### XML
XML is better human-understandable. It also has wide application range and thus a potentially wider user-base. XML can for example also be used to generate PDF score-forms, and allow for easier translation. However XML provides less (direct) functions to define logic. These logical constructs have to be defined and parsed separately when using XML

### Conclusion
We choose to use the **XML** option mainly because of the 'readability' for the non-technical users. XML makes it also easier for other developers to use the definition file in other applications, thus allows a wider adoption. However the JavaScript file is more useful in the envisioned scoring system. Therefore a pre-loader/render will be used to transform the XML to the JavaScript. Users can load the XML file which the system will then transform into the JavaScript functions that can parsed by the score-sheet controller. 

## Work packages definition

At the moment we define four major applications that are being developed. In declining order of importance: the scoring application, the clock, the overlay and the twitter feed. Work is being done on all these applications, but the main focus is on the scoring application. In all applications various options are built to communicate with each other, i.e. the RabbitMQ central server.

### Scoring application
Within the scoring application we have the following main work-packages that are being developed, brackets indicate the task lead:
* Missions definition (see above) (Rob). To define the various missions, the scores and the calculations. Includes the translation to JavaScript functions
* Interfaces (Bart). We will use various interfaces for the central administration and the client, as well for the various devices. 
* Communication (Sander). How the various devices and application communicate, taking into consideration: configuration ease, robustness (loss of connectivity), no internet access and various use-scenarios.
* Publishing (Martin). Generate the needed output in the system, such as the ranking, PDFs and web page with results. Also includes connections to overlay.
* Team administration. The module that deals with everything that has to do with the data storage, team list, names, but also scores and other relevant data and the related interfaces
* Score sheets controller and configuration. Evaluating the entered spreadsheets and recording the results. Creating options for different competitions setups (finales, elimination, practice rounds etc)

### Clock
The Clock is available and ready to use. The clock can also be used in standalone modus and can be found on the Github. Rikket will continue to work on the performance and appearance. 
**Note/Discussion:** perhaps we should create a separate page for our releases + manuals and support (helpdesk?). 

### Twitter
The twitter application is a often requested application that shows twitter messages pulled in live from the internet. Optionally this twitter feed can be superimposed on live video using chroma keying. The features of the twitter application are:
* Load twitter messages from the internet
* Create the twitter bar as a webpage and not as application
* Add moderation service through webpage

### Overlay
Some functions of the overlay are being rebuild. The major desired functions for the overlay application (superimposing on live video) are:
* Display (and configure) sponsor logo's
* Display (and load) team scores
* Display (and enter) messages, including the award ceremony results
The default option is to keep using Martins' current (Delphi) overlay application and work on this part after the national finales.

## Use cases
For now we envision two major scenario's that will apply to the majority of finales. We have the following scenarios:
* At the very basic level referee use paper score sheets. These are handed to a scorekeeper who enters them directly into a central application. In this scenario there is only 1 device: one laptop (optionality w. printer)
* Score keeping is done on 1 device. In a small final 1 device can be used by all referees, passing for example a tablet around. This tablet contains both the central application and replaces the score sheet.
* Score keeping is done on devices who automatically submit the results to the central application. 
* Hybrid forms are possible, furthermore the central application contains and provides the team-list to the clients. If run on the same devices (central+client) no network synced is needed. B

Notes:
* The system should create regular backups at various devices
* Restore points should be created when modifying crucial information (i.e. deactivate team instead of deleting the row)
* Administration (central application) should be password protect
* Clients should identify themselves (ie. referee login with password)

###Conclusion
As a conclusion we define two applications, that both will run on multiple devices (mobiles, tablets, laptops, pc, and eventually server-side).
* The central application, that contains the definition of the challenges, the team list, the recorded results and scores and generates the outputs. (replacing excels)
* The client application, that is used to enter the scores of the teams (replacing the score-sheet)
In the first scenario, both applications run on the same device. In the later scenario the applications run on (multiple) different devices. Sander will define a plan on how these applications can communicate and ensure the data exchange is robust. A key requirements is the ease of use (configuration) when using the system in both the networked mode and the single device mode. Note that the client application should also be able to be replaced by paper scoresheets in the above scenarios. 

## Next meeting
We will plan a next meeting in 3 weeks (last week of October) to verify the progress and discuss any points. Bart has indicated that he will be less available in the upcoming three week due to thesis writing. Kenny will propose a meeting date. Location will be TU/e.

## Action points
Action points are defined in the various issues on GitHub but include:
* [Rob] XML definition and translation to JavaScript functions
* [Kenny] Invite new (international) volunteer to work a small parts
* [Rikkert] Improve clock
* [Bart] Start implementing administration (central application on laptop) interface
* [Martin] Work on publishing (output) features for central and client application
* [Sander] Define / Design communication interface between applications including sync options
* [Kenny] Workday for testing ATEM video-mixer
* [Kenny] Outsource team administration module
* [Rikkert] Score-sheet controller + competition setup
* [Kenny] Design process for Judge deliberation integration (input and output)
* [Kenny] Write scenarios for various finales as verification for design


