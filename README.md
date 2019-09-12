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

The file __input3.php__ is relevant for the clientside recording and transmitting data process:
- For the layout the css grid-layout is used. For the aligning the form description and the corresponding input field a two column design was assigned. The columns have the same width in dependency of the available width:
``` display:grid;grid-template-columns:1fr 1fr ```
The rows also have a automatic height. There a 7 Rows defined in the grid, which corresponds to the total of required rows in the layout (Input-rows and headline):
``` grid-template-rows:auto auto auto auto auto auto auto ```
The Sizes (font and width of the inputboxes are defined with the measurement _em_ with the goal to enable a responsive view. However the responsive view have to be improved.
- The values of the inputfields are accessed by ```NameOfForm.inpfieldname.value ``` . These values are assigned to the corresponding properties of a new Javascript object _importTextItem_, which contains all relevant text-data of the recorded dataset.
Defining the empty object:```let importTextItem={};```
Assigning the formvalues of the form (name: _curForm_) to the corresponding property of _importTextItem_:

```importTextItem.iTitel=curForm.inp_title.value;
importTextItem.iArea=curForm.inp_area.value;
importTextItem.iDesc=curForm.inp_desc_detail.val
importTextItem.iDest=curForm.inp_dest_detail.value;
```  
- After all values are assigned to the temporary object importTextI
tem, this object is transformed to a JSON-file for transfering it to the sql-database.

```    importJSON=JSON.stringify(importTextItem);```

- The object is transfered to the PHP-File _transferdata.php_ by using an **XMLHTTPREQUEST** in Javascript. The transfermethod is "Post".
``` var transfer=new XMLHttpRequest();
transfer.open("POST","transferdata.php",true);
transfer.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
transfer.send('newItem='+importJSON);
transfer.onerror=function(){console.log("Übermittlungsfehler");}
transfer.onreadystatechange=function(){
console.log("Status:"+transfer.readyState+"\n Übermittlung erfolgreich:"
+transfer.status+"\n Inhalt:"+transfer.responseText);} 
```

In the targetfile __transferdata.php__ the object is fetched with the variable _impObj_:
```$impObj=$_POST["newItem"];```

The JSON is imported and it's properties are written in the array _jsonImpObj_ by usin the __json_decode__ command, with the second parameter setted to true. The splitting up to an array helps to import this values in an later step to in certain Columns of an table of a sql-database:
```$jsonImpObj=json_decode($impObj,true);```

To work with the database in PHP in any possible manner, a databaseconnection is required at first.

```$db=mysqli_connect("Host","User","PW","DB-Name");```

The following parameter are needed, that PHP and the SQL-Data are formatting the incoming text-information in UTF-8. So also all special characters are displayed correctly.

```mb_internal_encoding('UTF-8');
mysqli_set_charset($db,"utf8");
```
There is one value, which cannot be collected from the recorded data in the inputform: for a correct matching with the img-data later on, and also to make the dataset unique in any case, an Id is required. In the table _KuT_Id_ is only one value: The Id of the dataset before. This value summed up with 1 is the Id of the current dataset. The new Id also needs to be updated in the Table _KuT_Id_.

```$quer1="SELECT * FROM KuT_Id";
$quer1_result=mysqli_query($db,$quer1);
$getId=mysqli_fetch_object($quer1_result);
$valGetId=$getId->Id;
$newId=$valGetId+1;
$updQuery="Update KuT_Id Set Id=".$newId." Where Id_Name='curId'";
$quer2_updateId=mysqli_query($db,$updQuery);
```
As seen above, the queries are defined in a string as input for the relevant PHP-SQL-command. Since the whole table _KuT_Id_ is selected, the __mysqli_fetch_object__ command is used to write all data in an object(although there is only one dataset of the last Id in this case). There are also some commands to check, wether the dql query worked, which have no high relevance for the concept as a whole, so that the description is not necessary at this point.

With fetching the old Id and generate the new, the text-data for the database is complete. The values can by written (inserted) in the table _KuT_Items_: 

### The Front End/ Data-Retrieving Part will be coming soon, when finished the first Part
  
