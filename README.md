# KeepAndTrack
KeepAndTrack is a concept for app to help users to locate their stored items. For example where Do I have stored the floor lamp last november?Is it in the basement or loft? The concept is that the user only take one foto of this item, make a brief description of item and location, and give the main location (cellar for instance), when the item is stored. In a graphical frontend the possible storeplaces and the items are displayed in a way a standard house is structured, and it is also planned, that the user can set up the possible store places. For example, some may a have a garage for storing things, others not.  The items are displayed as small foto miniatures. Of course there will be a searchfunction.

## Technical Implementation
The first version of the app will be a "web-App", using the following mark-up and programminglanguages 
- HTML and CSS for the Design
- Pure Javascript for handling the input data on the clientside and for displaying the items using DOM specifications on the frontendside
- PHP and SQL to realize the datamanagement on the backendside / on the sqldatabase

First Version means, that I create this app with the knowledge i already have. There might be other versions with more features, possibly programmed with python.

## Current State
As said before the current version is a Web-App, that means that there is a link: [http://www.littleorange.de/keeptrack/](http://www.littleorange.de/keeptrack/), where you can see the pre-alpha version of the app. I am afraid, that the language is currently in german. To view the code, I will place the php-files also in GitHub. I am actually working on programming and designing the part of input the items and transmitting the pictures for the items. When I am finished with this part, I will start programming the frontendpage, where the stored items are displayed in a structure of a house (with loft, cellar etc.) and are also search able. This is the part for retrieving the data, which has been transmitted on the sql database in the first step of recording the data.

### The Input / Recording Part of the App has the following steps and States
![Programming Steps Implementation Input and transmitting data to database](http://www.littleorange.de/keeptrack/o_bilder/InputDiagramm.jpg)

**Detailed Description of the implementation of recording and transmitting data to the database**
The file __input3,php__ is relevant for the clientside recording and transmitting data process:
- For the layout the css grid-layout is used. For the aligning the form description and the corresponding input field a two column design was assigned. The columns have the same width in dependency of the available width:
```display:grid;grid-template-columns:1fr 1fr```
The rows also have a automatic height. There a 7 Rows defined in the grid, which corresponds to the total of required rows in the layout (Input-rows and headline):
```grid-template-rows:auto auto auto auto auto auto auto```
The Sizes (font and width of the inputboxes are defined with the measurement _em_ with the goal to enable a responsive view. However the responsive view have to be improved.


### The Front End/ Data-Retrieving Part will be coming soon, when finished the first Part
