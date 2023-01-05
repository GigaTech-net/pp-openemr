# Project Prometheus - OpenEMR Capabilities
## Overview
This documentation aims to assist on using open-source [OpenEMR](https://www.open-emr.org/) to:
1. Launch SMART on FHIR (SoF) applications
2. CRUD/query FHIR API use for patients

Note: registering and launching your SMART application comes as a prerequisite to FHIR API use.

## Technology Stack
* OpenEMR
* XAMPP
* PHP
* MySQL
* FHIR API
* SMART
* OAuth 2.0

## 0 - Prerequisite
### Installation
Running a local OpenEMR server requires a webserver and database. This guide will expect a basic understanding of PHP and MySQL after installing [XAMPP](https://www.apachefriends.org/download.html), though [alternative installation guides](https://www.open-emr.org/wiki/index.php/OpenEMR_Installation_Guides) exist (i.e. Docker).
* My [personal recommendation](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gksOX3Kd9KPo-O68ncT05o) for learning XAMPP

After installing XAMPP, run the **Apache** and **MySQL** services, install and unzip [OpenEMR](https://sourceforge.net/projects/openemr/files/OpenEMR%20Current/7.0.0.2/openemr-7.0.0.zip/download) and move it to XAMPP's webserver root directory (i.e. C:/xampp/htdocs).

#### Additional Installation Notes
OpenEMR 7.0.0 is the current stable production release version and is compatible with PHP
versions 7.4 - 8.1. Select a XAMPP version that supports a compatible PHP version.
* The **php.ini** file can be found at:
  * Windows: `C:/xampp/php/php.ini`
  * Mac/Linux: `/Applications/XAMPP/xamppfiles/etc/php.ini`
* The Apache configuration file **httpd.conf** can be found at:
  * Windows: `C:/xampp/apache/conf/httpd.conf`
  * Mac/Linux: `/Applications/XAMPP/xamppfiles/apache2/conf/httpd.conf`

### Setting up OpenEMR
Use OpenEMR”s installation instruction guide ([Windows](https://www.open-emr.org/wiki/index.php/OpenEMR_7.0.0_Windows_Installation), [Linux](https://www.open-emr.org/wiki/index.php/OpenEMR_7.0.0_Linux_Installation)) to configure the Web GUI
that will setup your OpenEMR database and admin account
* Note: As long as you have not touched any user accounts in phpMyAdmin, the **Root
  Password** field will be blank
* **Password** and **Initial User Password** are your own custom passwords that you will
   use to login as an administrator to the OpenEMR application

When setup is complete, login to the system with your new admin credentials.

## 1 - OpenEMR SMART Capabilities
First, enable the Standard REST and FHIR API endpoints by navigating to `Admin -> Globals -> Connectors` and toggling:
* _Enable OpenEMR standard REST API_
* _Enable OpenEMR Standard FHIR REST API_

Next, register a new client by navigating to `Admin -> System -> API Clients -> Register New
App` and filling in the following fields:
* **Application Type** - Public
* **Application Context** - Multipurpose Application
* **App Name** - [ up to you ]
* **Contact Email** - [ your email ]
* **App Redirect URI** - http://localhost:4200/
* **App Launch URI** - http://localhost:4200/launch
* **App Logout URI** - [ you can leave blank ]

Then, select the following scopes:
* _**openid**_
* _**fhirUser**_
* _**online_access**_
* _**launch**_
* _**profile**_
* _**patient/Condition.read**_
* _**patient/Encounter.read**_
* _**patient/MedicationRequest.read**_
* _**patient/Observation.rea**_
* _**patient/Patient.read**_

Submit the registration form and copy the **Client APP ID** in a secure location. If you haven't already, run your SMART on FHIR application, and then update its Client ID accordingly.

In order to enable the client for active use, return to `Admin -> System -> API Clients`, edit the client just created, and select **Enable Client**.

Navigate to `Patient -> New/Search` and create a new patient
* For testing purposes, simply inputting **Name**, **DOB**, and **Sex** is enough

At the bottom of the patient dashboard, expand **SMART Enabled Apps** and
click the Launch button for your client app, where you will OpenEMR login with your admin account.

Finally, authorize the application scopes to view the SoF App.

## 2 - OpenEMR FHIR Capabilities
Querying FHIR API endpoints will require you to toggle API endpoints and register a new SoF client by following the steps of **1 - OpenEMR SMART Capabilities** above.

After registering your client, navigate to [Swagger](http://localhost/openemr/swagger/index.html) and click the green **Authorize** button.

IN PROGRESS...

## Resources / Links
* <a href="https://www.apachefriends.org/download.html" target="_blank">XAMPP Download</a>
* <a href="https://www.open-emr.org/wiki/index.php/OpenEMR_Downloads" target="_blank">OpenEMR Download</a>
* <a href="https://www.open-emr.org/demo/" target="_blank">OpenEMR Live Demos</a>
* <a href="https://github.com/openemr/openemr/blob/master/API_README.md" target="_blank">OpenEMR REST API Guide</a>
* <a href="https://github.com/openemr/openemr/blob/master/FHIR_README.md" target="_blank">OpenEMR FHIR API Guide</a>
