# App manual \(v2\)

The DiSARM application is a prototype web-app designed to support the planning, implementation and monitoring of indoor residual spray (IRS) campaigns.

## Introduction

This document has been prepared for the end user of the DiSARM application once it has been set up and ready to use. It covers the general information of the application including how to download it, what to do if it is not working well and how to use the data collection, planner, and dashboard sections of the DiSARM application.

### General

#### What is DiSARM?

The Disease Surveillance and Risk Monitoring platform \(DiSARM\) is a spatial intelligence tool, built to enable disease control programs to deliver more effective field campaigns. The platform combines an interface used to pull together, collect and visualize data with a powerful back-end analytics engine to convert raw data into actionable information. The DiSARM platform consists of four modules: data collector, planner, dashboard and administration. The platform can be used for any activity that involves spatial data/heat maps, data collection and data analysing and reformatting into charts and graphs. While the internet is needed to sync your data with the online tools, data input can continue to occur while offline.

The platform is currently being used by malaria programs in four countries in southern Africa to help plan, execute and monitor indoor residual spraying campaigns.

More information on the DiSARM platform can be found at [www.disarm.io](http://www.disarm.io).

#### How to download DiSARM

To access the DiSARM application your application administrator should give you a web address \(URL\) where your application can be accessed. DiSARM is most compatible with Google Chrome browser

![](.gitbook/assets/app-image73.png)

## Automatic pop-up
The application will pop up a message; "offline ready" once it is finished loading. At the bottom there will also be a message: "ADD TO HOME SCREEN". To download the application to your mobile phone click the message.

![](../.gitbook/assets/app-image49.png)

A confirmation message will pop up and you should click "ADD" to download the application, or cancel if you want to keep using the Google Chrome whenever you are using DiSARM.

![](../.gitbook/assets/app-image103.png)

When the application has been added to your homescreen, you will receive a notification saying "DiSARM added on home screen". You may get a different name, depending on what name your application administrator gave the application when they deployed it for your organisation.

![](../.gitbook/assets/app-image47.png)

## Manual method
If you do not get the pop "ADD TO HOMESCREEN", you can add the application to your home screen manually by selecting the "Options" button on the top right of your browser.

![](../.gitbook/assets/app-image50.png)

Click "Add to Homescreen" to download the DiSARM application and follow the step number 3.

![](../.gitbook/assets/app-image45.png)

After clicking "Add," the system will start downloading the DiSARM application to your device. When the download is complete, you will receive a notification on your browser and on the notifications bar at the top of your device.

![](../.gitbook/assets/app-image94.png)

A DiSARM icon will show on your device among the other application icons as shown in the image below:

![](../.gitbook/assets/app-image22.png)

> Note: If you are on a desktop, the downloaded application is saved in your browser automatically. DiSARM can now run offline on your browser after it has been downloaded.

### **System requirements**

The system requirements listed below are fully supported by the DiSARM application.

#### Mobile Phones

Operating System must be Android or IOS

Browser must be Google Chrome from version 40 upwards

#### Computers

Operating System must be Windows or Mac

Browser must be Google Chrome from version from version 40 upwards

> Note: Although other browsers my work, we recommend using google chrome as Chrome is fully supported. Other functions may not work well on other browsers.

#### **Memory usage**

A mobile phone must have at least 20 MB of storage free to open and download the application on the browser.


### **Reset offline**

In the unlikely event that the application stops working, please reload the application. If it is still not working there is a function to reset it by selecting the "Reset Offline" option under the DiSARM logo.

![](../.gitbook/assets/app-image55.png)

> Note: Although you will be resetting the application offline, the application will not delete any data that you have already collected and saved to your device.

You will be presented with a screen informing you "you will not lose any data, click the button labeled "reset offline mode"

![](../.gitbook/assets/app-image35.png)

The page shown above can also be reached by editing the URL in the address bar. You have to change it to URL-given-to-access-disarm/reset.html

In other words you add /reset.html. The first character there is a forward slash\(/\). In our public demo application it would be [\[https://demo-app.disarm.io/reset.html\]{.underline}](https://demo-app.disarm.io/reset.html)

You see a message saying stating "offline mode was reset successfully". Click "Restart Application" button to start using the application.

![](../.gitbook/assets/app-image9.png)

> Note: The "restart application" button will bring you back to the Login page.

Resetting the application will log you out. Make sure to do it if you are not using the application offline \(if you have network\) to log back in as it is not possible to log in if you do not have network.

### **Updating**

When the DISARM application is connected to the internet, it will automatically check to see if a new version is available. If a new version is available, it will download automatically and update in the background. You can continue to use the application during the download. Your data will not be affected by the update. When an update is being downloaded, a message stating "Update Downloading" will show at the top right corner of the toolbar.

You can dismiss the message by clicking it.

![](../.gitbook/assets/app-image27.png)

> Note: Updates may not be successful due to slow internet connection. If the update is unsuccessful or your browser freezes during the download, try a "forced reload" by pressing Ctrl+Shift+R on Windows \(Cmd+Shift+R on Mac\). on a mobile phone touch the screen at the top and drag to the bottom. The application will automatically attempt to download the update again. Your data will not be removed as a result of the forced reload. However, **any unsaved forms \(incomplete data collection in the record point module\) may be deleted.**

### **User Page**

The first page you will see after clicking the "login"After logging button is the User Page. It lists the sections of the application you are allowed to access pre-selected by your application administrator. These sections are sometimes referred to as modules and a user who has full access will have:

* IRS Monitor
* IRS Plan
* IRS Record
* Debug
* Geodata

> Note: Some application modules will have customized names and a higher or smaller number of modules based on the configurations of your application administrator.

Below the list of modules the text text shows your the version number of your application. When clicked it displays the version number of your configuration and some more device information that includes your browser name, version, operating system and your device name.

![](../.gitbook/assets/app-image114.jpg)

### **Sidebar**

After logging into the DiSARM application, you can view your modules in the sidebar. These modules are the same as those listed on the User Page and are pre-selected by your application administrator. To open the Sidebar, click the sandwich icon \(three small horizontal lines icon\) on the top left corner of the screen.

![](../.gitbook/assets/app-image46.png)

The Side Bar will display the following information:

* Title given to you DiSARM application
* Version of the DiSARM application being used
* Instance ID \(also referred to as testing ID is set during log in so that testing data and settings are not saved with real data\) _not always there_
* Modules made available by your application administrator
* User Page navigation option
* Help option
* Logout option

![](../.gitbook/assets/app-image110.png)

Close the Sidebar by clicking anywhere outside of the Side

![](../.gitbook/assets/app-image102.png)

### **Geographic Data**

After logging in you will be presented with a page titled geodata. It will have name/s of the uploaded geodata with buttons towards the right of them labeled retrieved. 

![](../.gitbook/assets/geodata.png)

The user will have to retrieve the geodata by clicking on retrieve otherwise the button labeled “launch” will not be activated. When the user clicks on “retrieve”a loading bar will appear and once the geodata have been retrieved a green tick icon will be shown. Then the user can click on launch to launch the application. 

![](../.gitbook/assets/retrieved.png)

Other users may have permissions to see the geodata page where they can even download the geodata to their devices. 
On the user page or on the sidebar select geodata option and you will be brought to the page shown below:

![](../.gitbook/assets/app-image1.png)

The button labeled "RETRIEVE" when clicked will load the new geodata into your application so that it will show all the areas on the dashboard, planner and data collector modules.

A red progress bar will be shown to show that it is loading something, wait till it is finished and then you can continue using the application:

![](../.gitbook/assets/app-image60.png)

The loading bar is shown below with the red rectangle:

![](../.gitbook/assets/app-image75.png)

If the user wants to save the geodata onto their device in their downloads folder, the "DOWNLOAD" button is another option. By clicking the same geodata file that the application administration uploaded on the server will be downloaded to your computer. When clicked it instantly downloads it and you will find it in your downloads folder.

![](../.gitbook/assets/app-image71.png)

### **Known limitations**

It is not possible to make a plan, on the planner module, while using a mobile device. The panel type is not used in the app which makes it not possible to touch areas on the mobile cell phone's screen in order to include them in the plan.

