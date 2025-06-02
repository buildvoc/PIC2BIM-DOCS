---
title: Egnss4cap 
description: Enabling the digitalisation of agri-government controls through Galileo & EGNOS
---
#### Introduction
Mobile Application that digitises procedures for farmers in the European to satisfy their reporting requirements under the current and post-2020 Common Agricultural Policy (CAP) reform. New rules adopted by the European Commission for the current and upcoming CAP allow a range of modern satellite-based technologies to be used when administering and controlling area-based payments. 

For example, automatic monitoring procedures employing data and signals from both the Copernicus and Galileo programmes can be used to reduce the number of On The Spot Checks (OTSC). 
The use of these technologies is a part of the European Commission's ongoing commitment to modernise and simplify the Integrated Administration and Control System (IACS) processes within CAP.

The tool is Open Source, available for free and is able to be integrated by any Android or iOS developer. 

The EGNSS4CAP application will use Galileo differentiators to enable farmers to provide geo-tagged photos that both support and complement a Copernicus Sentinel-based monitoring approach for CAP. 

Mass market devices such as smartphones and tablets will be able to run the application and use GNSS to provide location and timing of the photo ensuring required accuracy and authentication for reporting to the paying agencies.

#### Application Key Features:
* Map view: The Picture Map view provides various features on the screen such as a connect/disconnect button to access the GNSS raw data, and a search button, photo button and send button to perform the necessary steps to take a photo.
* Photo taking with high accuracy position: Photos can be taken with correction or without correction depending on t he farmer's choice.
* Tilt control in photo mode: When in t he camera view, the app displays a tilt bar to show heading and tilt information and an error message when the phone is tilted too far.
* Angle view of photos on the map: After taking a photo, the farmer can see in which direction the photo was taken on the picture map.
* Tracking mode: This mode is used for higher Land Parcel ldentification
System (LPIS) proposes, considering the high accuracy calulated position on the map.
* GNSS Information: The app provides various details that are retrieved from the GNSS module and are divided into several sections that display:
    * The number of sate llites in use, in view and EGNOS fix use
    * Geolocation information (Latitude, Longitude and Altitude)
    * North/Sout h, East/West and fix quality
    * Quality parameters

#### Web Console Key Features for Farmers
* Photo list: Photos that are currently stored in the database are displayed on the left side of the console and are divided in columns with relevant information: Photo ID, latitude, longitude,timestamp, and details of Exit photo metadata.
* Map overview: Photo are represented by a pin that shows its geolocation, and an arc that shows the angular field of view and the direction in which the camera lens was pointing. Photos are coloured green for valid photos, red instead for invalid
photos.

#### Web Console Key Features for Paying Agencies
* Assigned farmers list: Photo lists from all assigned farmers are available.
* Photo list check details can be checked, including:
    * Camera field of view value (tilt angle and camera heading)
    * altitude; location and timestamp
    * universally unique identifier (UUID) of the device that took the photo; and the network cell id and Wi-Fi.

#### Project Outcomes
The EGNSS4CAP project reviewed and assessed the state-of-art and positioning of Galileo including high accuracy and authentication, in order to define the parameters and requirements for a geotagged photo application. 

Building on those requirements, a standalone open source Android and iOS application has been developed for use in CAP-oriented products. The outputs or this development include the software, supporting documentation and the source code of both the application and libraries.

* Android & iOS mobile application
* Web console
* User manual
* Source code published on Github
* Authentication library
* High-accuracy library
* Quick start guide

[[Web-Console]]