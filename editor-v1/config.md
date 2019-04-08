# Config
Write your configuration file
  
The configuration file is where the user will add the charts of the dashboard, the form for data collection, add validations, add applets to use and edit them as desired. To access the configuration section the user must click on the 'config" tab on the menu

![](../.gitbook/assets/editor-image76.png)

The user will then presented with a structured view of the config. In this context structured view means that the configuration file is divided into the sections shown on the left \(Spatial Hierarchy, Map Focus, Meta, Monitor, Plan, Record \(point\), Tasker, Form, Aggregations, Decorators, Validations\). By selecting one of the sections you get to edit code that concerns only the selected section.

![](../.gitbook/assets/editor-image120.png)

When a section is selected it will turn blue and it will be displayed on the top of right column in bold black text

![](../.gitbook/assets/editor-image93.png)

The structured config editor makes editing easier because; aside from structuring the whole config file into sections it allows you to insert blank or empty json objects. The user can click on the "insert blank" button as shown below

![](../.gitbook/assets/editor-image52.png)

Clicking the "insert new blank" will create the minimum needed code for that applet. It puts in some random text so the user has to change to show what is desired on the app.

![](../.gitbook/assets/editor-image11.png)

The user can switch to the raw view to type everything from scratch by clicking the switch at the top that has the label "structured" on the right and the label "raw" on the right

![](../.gitbook/assets/editor-image123.png)

If the user goes straight to the raw view of the config after logging in they will be presented with a screen that will have only the instance ID object.

![](../.gitbook/assets/editor-image75.png)

The Structured view can work as a guide telling the user what code to add to the config file to complete it step by step. All the user needs to do is add some jason, click on "save" and then click on "check if valid"

![](../.gitbook/assets/editor-image112.png)

If the user is not sure how to start, clicking on check if valid will print a message on the right to tell you what is missing.

![](../.gitbook/assets/editor-image33.png)

The message above say the missing property is \_id, instance ID is there but the system expects it to be called \_id and not instance\_id. So the use must change it to \_id and click on the save button and then on the "check if valid" one.

![](../.gitbook/assets/editor-image54.png)

This presents a new validation message

![](../.gitbook/assets/editor-image13.png)

To solve it the user needs to create a property called applets as shown below:

![](../.gitbook/assets/editor-image14.png)

The next error is shown above on the right in the image. It requires that we add another property: \_id. After adding something always click the save button and the "check if valid button". The image shown below has the \_id property added and the error message displayed after clicking save and check if valid.

![](../.gitbook/assets/editor-image104.png)

The error message above states that Data applets requires a property called meta. So we insert that save and check if our json is valid and fix the error message:

![](../.gitbook/assets/editor-image32.png)

The next property to add is a property of the data.spatial\_heirachy and its called data\_version. So this means the config editor needs to have spatial\_heirachy and then have the data version. The image below shows the insertion of both properties and then the results of saving and checking the JSON is valid:

> Note: The version should match the one you have defined in your geodata file.

![](../.gitbook/assets/editor-image41.png)

The next thing to add is in the same place as the previous step, spatial\_heirarchy and it is the levels property. In the image below it is shown that the expected property of levels is an array but the square brackets. Note: The value comes from the levels that you have on your geodata file.

![](../.gitbook/assets/editor-image101.png)

The next property to add according the validation message is markers under spatial\_heirarchy. The image below shows the addition of the of the markers property. Note: Sometimes we have to add commas to at the end of the property lines to keep the rules of writing in JSON. It is for that reason that commas after the data version and levels were put.

![](../.gitbook/assets/editor-image15.png)

The next property to add are the denominator fields under spatial\_heirarchy inside markers, Note that these values come from your geodata file too:

![](../.gitbook/assets/editor-image47.png)

The validation messages requests for the addition of planning\_level\_name inside markers too. Note that a comma was added at the end of denominator\_fields to keep the config file valid JSON:

![](../.gitbook/assets/editor-image28.png)

The next required property is record\_location\_selection\_level\_name. The image below shows the addition of record\_location\_selection\_level\_name property and the next validation message

![](../.gitbook/assets/editor-image59.png)

Since the image is not clear below the image shows how to add the record\_location\_selection\_level\_name

![](../.gitbook/assets/editor-image58.png)

And the validation message is shown in the image below: ![](../.gitbook/assets/editor-image124.png)

Which means the next to add is to add values for the properties listed above. The validation messages states that we need to first include the geodata\_summary summary array inside spatial\_heirarchy

second; add value for `record\_location\_selection\_level\_name` property which is called locality, and

third add inside the denominator field a field from the geodata that will be used as a denominator for calculating spray coverage. Which means it should the number of structures inside each area. In the geodata used in this example the file is called NumStrct field locality inside markers, and inside denominator\_fields. Forth and last; We had to also add the property of "name" with "locality" inside the levels array as it is shown in the image below:

![](../.gitbook/assets/editor-image24.png)

The validation message requires that we add a property called "display\_field\_name" under the "spatial\_heirarchy" property inside the "levels" array. The image below was taken after adding the "display\_field\_name" property, clicking save and clicking check if valid:

> Note: that the value OBJECTID comes from the geodata file._

Remember to add commas to the existing property above when adding another property in the same level below it.

![](../.gitbook/assets/editor-image88.png)

In the same place, the "field\_name" property is required, the image below was taken after adding it and checking if config is valid:

![](../.gitbook/assets/editor-image56.png)

The next property required is the geodata\_summaries. It is the array "geodata\_summaries" : \[\], and it is not recognised because we are missing the id of the geodata. The geodata is uploaded on the next section \(Section 4\) of this document. The geodata is shown on this screen of the geodata section:

![](../.gitbook/assets/editor-image20.png)

![](../.gitbook/assets/editor-image30.png)
2. The next step is adding the modules that you want your application to show to your users. In this step you add all of them, you will allow permissions for after creating them. The modules should be placed in the aplets level of the config file. The list of modules that can be added are: Monitor, Planner, and data collector \(record\). In this example the modules added first are the monitor and planner:

![](../.gitbook/assets/editor-image35.png)

The validation message requires the addition of the charts propoerty inside irs\_monitor which we added above. In the image below charts is added and the next validation message is shown. Note that charts is an array:

![](../.gitbook/assets/editor-image70.png)

And the validation message shows that we need to add the property of "map" inside irs\_monitor. The image below shows the validation message after the addition of the "map" property

![](../.gitbook/assets/editor-image83.png)

The next thing to add is the aggregation\_names property inside the "map property which we just added in the step before". This is are the names that will be shown below the map for the user to choose which layers they want to display on the map.Note that it is an array.

![](../.gitbook/assets/editor-image99.png)

The next property to add is "bin\_by" which is used to differentiating records points from each other when they are shown the map \(stated by the value location.selection.id\).

![](../.gitbook/assets/editor-image26.png)

The validation message shown in the image above requires the addition of a property called property\_layers inside 'map'. We add it in the image below and check for if json is valid, note that it is an array:

![](../.gitbook/assets/editor-image12.png)

With the "property\_layers" array added, the next thing required is the response\_point\_fieldswhich are also inside the "map" property. This is shown on the monitor when you click on a response point so you can choose any piece of data from the data collection form for its value \(the value is the one after the ":" and for this example the value is "recorded\_on"\) and it does not have to be only one field.

![](../.gitbook/assets/editor-image27.png)

The validation message requires the addition of season\_start\_dates. Values do not have to be added here but if the user's spraying project requires them they can add as many as they want. The application requires start dates only, the application will set the finishing date to be the day before the next season start date. This should added inside the "irs\_monitor" property and four dates are added as the image shows below:

![](../.gitbook/assets/editor-image49.png)

The next requirement is of the "table" also inside "irs\_monitor". In the image below the "table" is added and we check the validation message to see what is required next.

![](../.gitbook/assets/editor-image79.png)

The "aggregation\_names" property should be added next and that is what the image below shows. The validation message requires that we add the property inside the "table" property that we just added in the previous step and that is because the aggregation\_names will be the headers of the table shown on the monitor.

For this example the structures spayed and structures sprayed % will be the ones shown in the table. They are all added in the image show below marked out with a red rectangle:

![](../.gitbook/assets/editor-image17.png)

The next required property is the "bin\_by" on the "table" to do some filtering of the records when they are collected so that spray percentage can be calculated. The image below shows the addition of "bin\_by" and the next validation message after the addition:

![](../.gitbook/assets/editor-image9.png)

Inside the same place \("table"\) the property "propoerty\_layers" is the next thing to be added. The layers to be added is a property for the geodata to show you areas and the label that will show on the table and they are all added at the same time in the image below;

![](../.gitbook/assets/editor-image62.png)

The next required property is "table\_ output". This property as stated in the validation message goes in the "irs\_plan". In the image below the property is added and the next error message is shown.

![](../.gitbook/assets/editor-image74.png)

To solve the bottom two validation messages which are concerned with aggregation the aggregations must be defined. Aggregations are the calculations we do or numbers we collect to get a total e.g \(total number of structures sprayed, percentage of sprayed structures\). They should be defined end of the "markers" propers as shown in the image below. There are four aggregations defined in our example and they are; structures sprayed, structures sprayed %, bed nets in use and count.

![](../.gitbook/assets/editor-image108.png)

The two errors that are left are requiring the addition of the form that is used in data collection because the data is being referred to but the system does not know when and how this data enters the pplication. The form can be genarated easily on a service called surveyjs. Surveyjs, can be accessed here \[[https://surveyjs.io/Survey/Builder](https://surveyjs.io/Survey/Builder), provides a drag and drop interface for the user to create survey forms. While the user creates the form it generates the json of whatever the user has designed so that it can be copied and pasted elsewhere. In this example the json for the form has already been developed using the survey js and will be pasted at the end of the "markers" applet, the image below demonstrates:

![](../.gitbook/assets/editor-image94.png)

Another image showing the other end of the form:

![](../.gitbook/assets/editor-image57.png)

And the complete code of just the form is shown below:

```text
{
  "form": {
    "pages": [
      {
        "name": "page1",
        "elements": [
          {
            "type": "text",
            "name": "sprayed_count",
            "title": "Number structures sprayed with DDT",
            "isRequired": true,
            "validators": [
              {
                "type": "numeric",
                "text": "Must be more than zero",
                "minValue": 0
              }
            ],
            "inputType": "number"
          },
          {
            "type": "text",
            "name": "bednets_count",
            "title": "Number bednets in use",
            "isRequired": true,
            "validators": [
              {
                "type": "numeric",
                "text": "Must be more than zero",
                "minValue": 0
              }
            ],
            "inputType": "number"
          }
        ]
      }
    ]
  }
}
```

And once there is a validation message that says there are no problems. The configuration file is still incomplete though because there are still more options that can be added to the disarm application. The table on "irs\_plan" applet does not have any items to display. The image below adds the headers for the table and adds the source fields.

![](../.gitbook/assets/editor-image8.png)

When the "No probs" validation error shows up it may help to check the whole configure file for some missing values like empty braces. The charts are still an empty array and the next step will be adding a chart. In the image below the chart is given an ID and its dimensions then the validation message will guide on what to add next:

![](../.gitbook/assets/editor-image36.png)

The validation messages states that the next required fproperty of the chart is "options". In the image below options is added and the next validation message is shown. The options property comes with the first property, "layouts" in the image. The other options are added in other images:

![](../.gitbook/assets/editor-image100.png)

The next required property according to the validation message is the "title" which is supposed to be inside the "layout" property which we just added. The title refers to the titles of the chart that are included in the legend. That means the x-axis label, y- label and the main title of the chart. In this step all three titles are added:

![](../.gitbook/assets/editor-image73.png)

The next step is to set to be visible on the screen. This is done by adding a "showlegend" property and giving the value true inside the "layout".

![](../.gitbook/assets/editor-image86.png)

The validation message shows there are no problems, but the chart is not complete. The image below shows the addition of the chart type and the one in this example is a line. It could be a bar or pie chart:

![](../.gitbook/assets/editor-image98.png)

In the image below the "time\_series" is set to true to plot the line chart against a stipulated time period:

![](../.gitbook/assets/editor-image25.png)

To show the records on this chart \(line graph\) we will need to state a value to group them with, and since it is a line that is based on the dates when records are collected the field to be used is "recorded\_on". This field is automatically generated as time stamp and saved when the record is collected. In the image below we add the "bin\_by" property just below the "time\_series"

![](../.gitbook/assets/editor-image107.png)

The next thing we add just below the "bin\_by" property is the "geographic\_level\_refactor\_this\_key\_name" property and its value is "location.selection.id".

![](../.gitbook/assets/editor-image51.png)

The next property to add is the "multi\_series" and changes the legend on line graph at the bottom.

![](../.gitbook/assets/editor-image105.png)

There is nothing more required but the map property does not seem like it is complete as it missing some values of the properties. There is a couple of empty arrays that need to be filled in. in this example the "aggregation\_names" array is filled in first and the values added as shown in the image below are \"structures sprayed %\", \"structures sprayed\":

![](../.gitbook/assets/editor-image114.png)

The "property\_layers" property also has an empty array, so we put values that will be used to paint the map with the layers that the user prefers. In this example the values that will be added will be the risk and layer, and the number of structures layer. They are added as shown in the image below:

![](../.gitbook/assets/editor-image118.png)

The "response\_point\_field" property has an array that is still empty. In the image below we add only one value in that value called \"recorded\_on\" to show the date when the record was collected when it is clicked:

![](../.gitbook/assets/editor-image46.png)

The map that is in the monitor is of type chart and therefore we must state is its property as shown in the image below:

![](../.gitbook/assets/editor-image19.png)

The same applies to the table on the dashboard/monitor. It is also of type chart in the code of the application and therefore it should be identified so by adding the "chart\_type" property inside table{} as shown below:

![](../.gitbook/assets/editor-image63.png)

The planner module is also missing a tittle which should be added just before the closing brace of "irs\_plan" as shown in the image below. The title can be any word you want as long as you will remember that it refers to the planning module.

![](../.gitbook/assets/editor-image2.png)

The application will also need the "irs\_record\_point" property just below the "title" property that we just added. The image below demonstrates the addition and the validation message shows what more is required

![](../.gitbook/assets/editor-image61.png)

As required in the validation message in the image above, the next thing that is added is the metadata property.

![](../.gitbook/assets/editor-image38.png)

"Optional\_fields" is the next required property. It is going to be added in the "metadata" brace that was made in the previous step. The "optional\_fields" will be an array that will have fields that the users do not have to fill in when collecting data.

![](../.gitbook/assets/editor-image64.png)

The validation message requires the addition of a property called "show" inside metadata. The image below shows how to add that property and it is given the value of true:

![](../.gitbook/assets/editor-image111.png)

Before moving to deal with the validation message shown above we will insert a field inside the optional\_fielda array just below the "show" property that we just added. The optional field will be "team\_name"

![](../.gitbook/assets/editor-image71.png)

The validation messages shown above require the location selection areas. The user will have to list all of them in an array. They should all be listed in the geodata. For this example in each area the ID, name and category will be listed in the array. First the array will be added in the image below:

![](../.gitbook/assets/editor-image110.png)

Next thing to add is the list of areas in the "locality" array added above. As stated in the previous step, each area will have an ID, name and category \(which is a region in which the area is\).

![](../.gitbook/assets/editor-image68.png)

At the end of the array it should like it looks in the image below:

![](../.gitbook/assets/editor-image97.png)

The next thing to add the debug module. This is a part of the application that can be used for advanced debugging function e.g. automatically generating random records, editing form validations, clearing app data and etc

![](../.gitbook/assets/editor-image37.png)

The next property to add is the map focus. This will set the application to focus on your supplied geodata instead of the whole map or a wrong country when the application monitor/dashboard is opened. In the image below it is added without any properties inside, the validation message will state what is required:

![](../.gitbook/assets/editor-image23.png)

The validation message requires a property called "center" and it requires two values of latitudes and longitude to show the center of your geodata for the application to focus on. The image below demonstrates the addition of that property and its two values:

![](../.gitbook/assets/editor-image92.png)

The validation message then requires the addition of the "zoom" property after adding the center. The zoom property should be added right after the closing brace of the "center" property:

![](../.gitbook/assets/editor-image122.png)

Even though the validation messages do not show, but the instance will probably need a title so the users know what they are using on their devices. This title can be named anything the administrator desires. For this example it is named the Y-Land Demo. In the image below the instance property is added and inside it the title of the instance is designed:

![](../.gitbook/assets/editor-image31.png)

In the absence of problems in the validation messages the next property to be added will be the "location\_name" and the "slug", both inside the instance property. The location of this name is fictional, the administrator user should put the name of the country or area they will be working in.

![](../.gitbook/assets/editor-image43.png)

The next property to add is the "fake\_form". This is added at the end of the configuration file. The "fake\_form" is used in the debug part of the application for generating the random records. It will be an array of values filling in the data that needs to be filled in when collecting a record.

![](../.gitbook/assets/editor-image116.png)

Inside the array the user can add as many form values as they want to alternate when generating random data. The user only has to define the data that will be filled in on the form while collecting the data. The application will come up with time stamps and location coordinates for each record point that is collected. In this example three different sets of data are added.

![](../.gitbook/assets/editor-image78.png)

The next to add is an array of validations. This array will hold the validation of the form should there be any extra that the user wants to add. It is best to add all of them while generating the form and have them embedded in the form. The validation array added below will then be left empty as shown below:

![](../.gitbook/assets/editor-image84.png)

After the validations array, a "presenters" property is added. It will have inside it some properties that will be shown when a response point is clicked on the map in the monitor module. These properties will be inside another property called "pop\_up" description as shown below:

![](../.gitbook/assets/editor-image77.png)

Inside the "popup\_description" the fields that will be shown when the response point is clicked will be defined as shown in the image below:

![](../.gitbook/assets/editor-image50.png)

wergwerg![](../.gitbook/assets/editor-image48.png)

The last property to add on the configuration file will be the decorators. They are used to show different colors on the response point on the map. In this example the application will use the default color so the decorators property is left empty. The default color is gray:

![](../.gitbook/assets/editor-image60.png)

