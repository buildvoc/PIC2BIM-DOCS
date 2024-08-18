---
title: Getting started
description: PIC2BIM (EGNSS4ALL) is a geotagging photo mobile phone application
---
Interactive Graph Links ---

[[web-console]]

[[ios]]

[[android]]

[[building-attributes]] 

### Introduction
PIC2BIM (EGNSS4ALL) is a geotagging photo mobile phone application, which is Open-Source for IOS and Android.

Initially developed by EU Space Programme see [<u>http://egnss4cap.eu/</u>](http://egnss4cap.eu/) for more information, now being maintained and developed by PIC2BIM.</p>
</p>It takes advantage of GNSS raw measurements, European Global Navigation Satellite System (EGNSS) differentiators 

* Open Service – Navigation Message Authentication – OS-NMA) <b>for trustworthy and accurate geotagging.</b>
* European Geostationary Navigation Overlay Service (EGNOS)
* Dual frequency capabilities 

#### Features
Inside the App, the user can perform several different tasks:

* Taking photos, storing the position data (PVT) and representing them on the map
* Path recording
* Assisted-NMA architecture providing <b>authenticated positioning</b>
* Retrieving raw data about a specific point on the map through GNSS Raw Data
* Having access to GNSS SkyMap, showing the location of the satellites of the four global constellations (GPS, GALILEO, GLONASS, BeiDou) allowing for Two-Line Element (TLA) cross-check

PIC2BIM unique functionalities improve the performance and trustworthiness of smartphone photo geotagging, mapping and tracing, serving multiple domains including urban planning, logistics and insurance.

To check if the device that you are using can indeed use all the EGNSS differentiators, the following traffic lights are given as confirmation on your smartphone capabilities:

* Location service check: *green light* if this device has enabled location service and application has permission to use it
* Galileo capacity check: *green light* if this device is capable to use Galileo satellites
* Compass and Gyroscope: *green light* if this device is capable to use Compass and Gyroscope (Android)
* EGNOS signal check: *green light* if this device is capable to use ENOS (Android)
* Galileo Nav Message Signal check: *green light* if this device is capable to use OS-NMA (Android)

### Building Information Modelling (BIM)
Future development

### <b>Getting started</b>

This  Quick  Start  Guide  provides  a  brief  overview  of  the  main  functionalities  of  the  PIC2BIM application.  Detailed  information  on  the  functionalities  of  the  application  can  be  found  in  the following sections:

* Mobile Application - iOS
* Mobile Application - Android
* Web Console

The Pic2Bim / Egnss4all application is available at Google Play Store and Apple App Store:

[<img src="/media/media_google-play.png" width="229" height="73" />](https://play.google.com/store/apps/details?id=com.erasmicoin.euspa.gsa.egnss4all&hl=en)
[<img src="/media/media_app-store.png" width="229" height="71" />](https://apps.apple.com/ai/app/egnss4all/id1628843978)

#### Login

Click the *Sign In* button to complete the login.

<img src="/media/media_47a80ccdb00dfa6c.png" width="189" height="334" />

Fig. 20 <b>Login screen</b>

Through the "Select Server" button, it will be possible to set the URL of a custom server  that will be used instead of the app's default server.
<p>Enter "https://pic2bim.co.uk/" and click save.</p>

<img src="/media/media_8a6887262f599c06.png" width="189" height="334" />

Fig. 21 <b>Select Server</b>


* Make sure to grant permissions to access the device’s location.
For the first login, request a  user  and  password  combination  at  [<u>https://pic2bim.co.uk/</u>](https://pic2bim.co.uk/)  or  use  demo
(username) and demo (password).

* After the first login, the credentials will be stored in the device.

#### How to Make a Photo
Go to Unassigned Photos/Photos Menu (Fig. 1, for Android devices or Fig. 2 for iOS Devices)

<img src="/media/media_unassigned-photos-android.png" width="189" height="334" />
<p>Fig. 1 <b>Unassigned Photos</b> (Android)</p>

<img src="/media/media_photos-menu.png" width="189" height="334" />
<p>Fig.2 <b>Photos Menu</b> (iOS)</p>

Click on “TAKE PHOTO” and the camera turns on. After a few seconds, the snap
photo button appears on the screen (Android). 

<img src="/media/media_take-a-photo-android.png" width="189" height="334" /> 
<p>Fig.3 <b>Take a Photo</b> (Android)</p>

<img src="/media/media_camera-android.png" width="189" height="334" />
<p>Fig.4 <b>Camera</b> (Android)</p>

Click on “New” and the camera
turns on. After
a few seconds, the snap
photo button appears on the screen (iOS).

<img src="/media/media_new-photo-ios.png" width="189" height="334" /> 
<p>Fig.5 <b>New Photo</b> (iOS)</p> 
<img src="/media/media_camera-ios.png" width="189" height="334" />
<p>Fig.6 <b>Camera</b> (iOS)</p>

#### How to see your Photos
Click on “MAP” and the pictures will be displayed in their location on a map (Android).

<img src="/media/media_map-android.png" width="189" height="334" /> 
<p>Fig.7 Map (Android)</p> 
<img src="/media/media_photo-location-android.png" width="189" height="334" />
<p>Fig.8 <b>Photo Location</b> (Android)</p>

Click on “MAP” and the pictures will be displayed in their location on a map (iOS).

<img src="/media/media_map-ios.png" width="189" height="334" /> 
<p>Fig.9 <b>Map</b> (iOS)</p> 
<img src="/media/media_photo-location-ios.png" width="189" height="334" />
<p>Fig.10 <b>Photo Location</b> (iOS)</p>

#### How to SEND or SAVE to PDF your geotagged photos
Click on “SEND” and the pictures will be uploaded to the server (Android and iOS).

<img src="/media/media_send-photo-android-1.png" width="189" height="334" /> 
<p>Fig.11 <b>Send Photo</b> (Android)</p> 
<img src="/media/media_send-photo-ios-1.png" width="189" height="334" />
<p>Fig.12 <b>Send Photo</b> (iOS)</p>

#### How to TRACK a path or MAKE a polygon
Click on “Path Tracking” and then choose between record a new path or browse the paths already recoded and upload them or export to a KML file (Android).

<img src="/media/media_send-photo-android-2.png" width="189" height="334" /> 
<p>Fig.13 <b>Send Photo</b> (Android)</p> 
<img src="/media/media_send-photo-ios-2.png" width="189" height="334" />
<p>Fig.14 <b>Send Photo</b> (iOS)</p>

Click on “Map Menu” and then choose between record a new path or browse the paths already recoded and upload them or export to a KML file (iOS).

<img src="/media/media_map-ios.png" width="189" height="334" /> 
<p>Fig.15 <b>Map</b> (iOS)</p> 
<img src="/media/media_send-photo-ios-3.png" width="189" height="334" />
<p>Fig.16 <b>Send Photo</b> (iOS)</p>

#### How to USE the web console
Using the same credentials than the ones available for the application (demo/demo by default), it’s possible to connect and check the data uploaded from the smartphone (Android and iOS).
The URL is [<u>https://www.pic2bim.co.uk/</u>](https://www.pic2bim.co.uk/) there is the possibility to check the unassigned photos or the paths.
Scroll-up to see all the options, in case that you are not able to see the displayed buttons.

<img src="/media/media_web-console-01.png" width="363" height="35" />
<p>Fig. 17 <b>Web console</b></p> 
<img src="/media/media_web-console-available-photos.png" width="363" height="35" />
<p>Fig. 18 <b>Available photos</b></p>
<img src="/media/media_web-console-available-paths.png" width="363" height="35" />
<p>Fig. 19 <b>Available paths</b></p>
