---
title: TypeScript PHP
description: Web Console it’s possible to connect and check the data uploaded from the smartphone (Android and iOS).
---
### Hosting and installing the web console

#### Hosting requirements

* Php7 engine
* Composer v2
* Postgres
* Apache2 webserver
* Node v20.17.0

#### Server resources requirements

* min 8GB RAM
* min 2 core cpu
* min 10GB disk space

#### Installation Database

* Install pgsql database 
* Create a Database named "egnss4all"
* Import postgres dump file to init database

#### Installation steps for the webconsole and webservices


copy the web console files into the selected webroot directory create VirtualHost section in the Apache2 configuration and point it to selected directory
make sure that there is set a directive DirectoryIndex index.php

Execute the following commands in the selected directory

Create environment file
```
cp .env.example .env
```

Generate application key
```
php artisan key:generate
```

write the database name, database user and the corresponding password into the web console configuration file .env

```
DB_CONNECTION=pgsql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=egnss4all
DB_USERNAME=username
DB_PASSWORD=password
```

Migrate Database


```
php artisan migrate
```

Install Laravel dependencies
```
composer install
```

Install front end packages
```
npm install
```

For development
```
npm run dev
```

For production build
```
npm run build
```

run [<u>http://your * domain.tld</u>](<http://your> * domain.tld/)

### Developer Documentation

#### Technologies

* Laravel 11
* Inertia
* React
* Typescript
* HTML, CSS, Javascript
  * Tailwind
* Google maps API
* MPDF framework for generating PDF
* html2canvas.js plugin

#### Classes description

* Index
  * managing farmers
  * loading farmer list and tasks
* login
  * login user
  * logout user
  * verifying users
* task
  * adding tasks
  * loading task info and photos
  * accepting, declining and deleting tasks
  * changing task status
  * loading photos and photos metadata
  * loading shapes
  * assign unassigned photos to task
  * generating PDF
* user
  * managing users and roles
  * loading the unassigned photos and tasks of users
  * managing photo rotation

#### Structure

* Tailwind
  * Styles for web pages
* app
  * Model, Controllers and Middleware
* FONTS
  * fonts for web pages
* IMG
  * images for web
* JS
  * javascript files for web and map
* PHOTOS
  * photos downloaded from phones
* Typescript
  * Types for the language
* VENDOR
  * dependencies
* RESOURCES
  * front end views
* Directories
  	* app
      * Auth
      * Http
      * Mail
      * Models
      * Providers
      * Rules
    * bootstrap
      * cache
      * ssr
    * config
    * database
      * factories
      * migrations
      * seeders
    * node_modules
    * public
      * build
      * storage
    * resources
      * css
      * js
        * Components
        * Layouts
        * Pages
        * types
      * views
    * routes
      * emails
      * vendor
    * storage
      * app
      * framework
      * logs
    * tests
      * Feature
      * Unit
    * vendor  
* Components
	* Alert
	  * Alert.tsx
	* Button
    * CloseButton.tsx
    * DeleteButton.tsx
    * LoadingButton.tsx
	* FilterBar
	  * FilterBar.tsx
	* Form
    * CheckboxInput.tsx
    * FieldGroup.tsx
    * FileInput.tsx
    * SelectInput.tsx
    * TextInput.tsx
	* Messages
    * FlashMessages.tsx
    * TrashedMessage.tsx
	* Pagination
	  * Pagination.tsx
	* Table
	  * Table.tsx
	* ApplicationLogo.tsx
	* Checkbox.tsx
	* DangerButton.tsx
	* Dropdown.tsx
	* InputError.tsx
	* InputLabel.tsx
	* Modal.tsx
	* NavLink.tsx
	* PrimaryButton.tsx
	* ResponsiveNavLink.tsx
	* SecondaryButton.tsx


### Web Services and Database

Below is a technical overview of the implemented web services for the PIC2BIM application and their features.


#### check user by login and pswd

[<u>https://pic2bim.co.uk/comm_login</u>](https://pic2bim.co.uk/comm_login)

* input
  * HTTPS, POST
  * parameters
    * login – string(255)
    * pswd  *  string(255)
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * user – number – user ID for login, if exists
    * token - string - Bearer token to access APIs

#### sends geometry shapes for rectangle

[<u>https://pic2bim.co.uk/comm_shapes</u>](https://pic2bim.co.uk/comm_shapes)

* input
  * HTTPS, POST
  * parameters
    * max_lat – float
    * min_lat – float
    * max_lng – float
    * min_lng – float
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * shapes – array
    * identificator – string – shape identificator
    * wgs_geometry – json – geometry of shape

#### sends photos for task or user

[<u>https://pic2bim.co.uk/comm_task_photos</u>](https://pic2bim.co.uk/comm_task_photos)

* input
  * HTTPS, POST
  * parameters
    * task_id – number – task identificator
    * user_id – number – user identificator
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * photos – array
      * altitude – float – altitude of photo
      * vertical_view_angle – float – vertical view angle of photo
      * accuracy – float – accuracy of photo
      * distance – float – Distance of photo
      * nmea_distance – string – GNSS distance of photo
      * device_manufacture – string – Device manufacturer
      * device_model – string – Device model
      * device_platform – string – Device platform
      * device_version – string – Device version
      * efkLatGpsL1 – float – Kef metadata field efkLatGpsL1
      * efkLngGpsL1 – float – Kef metadata field efkLngGpsL1
      * efkAltGpsL1 – float – Kef metadata field efkAltGpsL1
      * efkTimeGpsL1 – datetime – Kef metadata field efkTimeGpsL1
      * efkLatGpsL5 – float – Kef metadata field efkLatGpsL5
      * efkLngGpsL5 – float – Kef metadata field efkLngGpsL5
      * efkAltGpsL5 – float – Kef metadata field efkAltGpsL5
      * efkTimeGpsL5 – datetime – Kef metadata field efkTimeGpsL5
      * efkLatGpsIf – float – Kef metadata field efkLatGpsIf
      * efkLngGpsIf – float – Kef metadata field efkLngGpsIf
      * efkAltGpsIf – float – Kef metadata field efkAltGpsIf
      * efkTimeGpsIf – datetime – Kef metadata field efkTimeGpsIf
      * efkLatGalE1 – float – Kef metadata field efkLatGalE1
      * efkLngGalE1 – float – Kef metadata field efkLngGalE1
      * efkAltGalE1 – float – Kef metadata field efkAltGalE1
      * efkTimeGalE1 – datetime – Kef metadata field efkTimeGalE1
      * efkLatGalE5 – float – Kef metadata field efkLatGalE5
      * efkLngGalE5 – float – Kef metadata field efkLngGalE5
      * efkAltGalE5 – float – Kef metadata field efkAltGalE5
      * efkTimeGalE5 – datetime – Kef metadata field efkTimeGalE5
      * efkLatGalIf – float – Kef metadata field efkLatGalIf
      * efkLngGalIf – float – Kef metadata field efkLngGalIf
      * efkAltGalIf – float – Kef metadata field efkAltGalIf
      * efkTimeGalIf – datetime – Kef metadata field efkTimeGalIf
      * timestamp – datetime – Kef metadata field efkLngGalIf
      * note – string – user note
      * lat – float – latitude of photo
      * lng – float – longitute of photo
      * photo_heading – number – photo azimuth
      * created – datetime – date and time of photo creation
      * link – string – photo link
      * digest – string – hash of photo

#### sends tasks for user

[<u>https://pic2bim.co.uk/comm_tasks</u>](https://pic2bim.co.uk/comm_tasks)

* input
  * HTTPS, POST
  * parameters
    * user_id – number – user identificator
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * tasks – array
      * id – number – task identificator
      * status – string – task status
      * name – string – task name
      * text – string – description of task
      * text_returned – string – description why is returned
      * date_created – datetime – date of create task
      * task_due_date – datetime – task due date
      * note – string – task note
      * number_of_photos – number – number of photos for task
      * flag_valid – string – task is accepted
      * flag_invalid – string – task is declined
      * reopen_reason – string – description why task is reopened
      * purpose – string – task purpose
      * photos_ids – array of numbers – IDs of task photos

#### receive task data from phone

[<u>https://pic2bim.co.uk/comm_update</u>](https://pic2bim.co.uk/comm_update)

* input
  * HTTPS, POST
  * parameters
  * task_id – number – task identificator
  * user_id – number – user identificator
  * status – string – task statuses
  * note – string – task note
  * photos – array
    * note – string – photo note
    * lat – float – photo latitude
    * lng – float – photo longitude
    * altitude
    * bearing
    * magnetic_azimuth
    * photo_heading
    * pitch
    * roll
    * photo_angle
    * orientation
    * horizontalViewAngle
    * verticalViewAngle
    * accuracy
    * deviceManufacture
    * deviceModel
    * devicePlatform
    * deviceVersion
    * satsInfo
    * extraSatCount
    * NMEAMessage
    * networkInfo
    * created – datetime – date of photo creation
    * digest – string – photo hash
    * efkLatGpsL1
    * efkLngGpsL1
    * efkAltGpsL1
    * efkTimeGpsL1
    * efkLatGpsL5
    * efkLngGpsL5
    * efkAltGpsL5
    * efkTimeGpsL5
    * efkLatGpsIf
    * efkLngGpsIf
    * efkAltGpsIf
    * efkTimeGpsIf
    * efkLatGalE1
    * efkLngGalE1
    * efkAltGalE1
    * efkTimeGalE1
    * efkLatGalE5
    * efkLng GalE5
    * efkAlt GalE5
    * efkTimeGalE5
    * efkLatGalIf
    * efkLngGalIf
    * efkAltGalIf
    * efkTimeGalIf
    * photo – string – base64 encoded photo
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs

#### sends paths for user

[<u>https://pic2bim.co.uk/comm_get_paths</u>](https://pic2bim.co.uk/comm_get_paths)

* input
  * HTTPS, POST
  * parameters
    * user_id – number – user identificator
* output
  * JSON
  * status – string  *  ok/error
  * error_msg – string – error message if an error occurs
  * paths – array
  * id – number – identificator
  * name  *  string
  * start – datetime – start of tracking datetime
  * end – datetime – end of tracking datetime
  * area – float – path area in m2
  * device_manufacture  *  string
  * device_model  *  string
  * device_platform  *  string
  * device_version  *  string
  * points – array
    * id – number – identificator
    * lat  *  float
    * lng  *  float
    * altitude  *  float
    * accuracy  *  float
    * created  *  datetime

#### sends photo by ID

[<u>https://pic2bim.co.uk/comm_get_photo</u>](https://pic2bim.co.uk/comm_get_photo)

* input
  * HTTPS, POST
  * parameters
    * photo_id – number – photo identificator
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * photo – object
      * altitude – float – altitude of photo
      * vertical_view_angle – float – vertical view angle of photo
      * accuracy – float – accuracy of photo
      * distance – float – Distance of photo
      * nmea_distance – string – GNSS distance of photo
      * device_manufacture – string – Device manufacturer
      * device_model – string – Device model
      * device_platform – string – Device platform
      * device_version – string – Device version
      * efkLatGpsL1 – float – Kef metadata field efkLatGpsL1
      * efkLngGpsL1 – float – Kef metadata field efkLngGpsL1
      * efkAltGpsL1 – float – Kef metadata field efkAltGpsL1
      * efkTimeGpsL1 – datetime – Kef metadata field efkTimeGpsL1
      * efkLatGpsL5 – float – Kef metadata field efkLatGpsL5
      * efkLngGpsL5 – float – Kef metadata field efkLngGpsL5
      * efkAltGpsL5 – float – Kef metadata field efkAltGpsL5
      * efkTimeGpsL5 – datetime – Kef metadata field efkTimeGpsL5
      * efkLatGpsIf – float – Kef metadata field efkLatGpsIf
      * efkLngGpsIf – float – Kef metadata field efkLngGpsIf
      * efkAltGpsIf – float – Kef metadata field efkAltGpsIf
      * efkTimeGpsIf – datetime – Kef metadata field efkTimeGpsIf
      * efkLatGalE1 – float – Kef metadata field efkLatGalE1
      * efkLngGalE1 – float – Kef metadata field efkLngGalE1
      * efkAltGalE1 – float – Kef metadata field efkAltGalE1
      * efkTimeGalE1 – datetime – Kef metadata field efkTimeGalE1
      * efkLatGalE5 – float – Kef metadata field efkLatGalE5
      * efkLngGalE5 – float – Kef metadata field efkLngGalE5
      * efkAltGalE5 – float – Kef metadata field efkAltGalE5
      * efkTimeGalE5 – datetime – Kef metadata field efkTimeGalE5
      * efkLatGalIf – float – Kef metadata field efkLatGalIf
      * efkLngGalIf – float – Kef metadata field efkLngGalIf
      * efkAltGalIf – float – Kef metadata field efkAltGalIf
      * efkTimeGalIf – datetime – Kef metadata field efkTimeGalIf
      * timestamp – datetime – Kef metadata field efkLngGalIf
      * note – string – photo note
      * lat – float – photo lattitude
      * lng – float – photo longitude
      * alt – float – photo altitude
      * photo_heading – number – heading in degrees
      * created – datetime
      * link – string – photo link
      * digest – string – photo hash

#### receive path from phone

[<u>https://pic2bim.co.uk/comm_path</u>](https://pic2bim.co.uk/comm_path)

* input
  * HTTPS, POST
  * parameters
    * user_id – number – user identificator
    * name  *  string
    * start – datetime – start of tracking datetime
    * end – datetime – end of tracking datetime
    * area – float – path area in m2
    * device_manufacture  *  string
    * device_model  *  string
    * device_platform  *  string
    * device_version  *  string
    * points – array
      * lat  *  float
      * lng  *  float
      * altitude  *  float
      * accuracy  *  float
      * created  *  datetime
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * path_id – number – ID of received path

#### receive photo data from phone

[<u>https://pic2bim.co.uk/comm_photo</u>](https://pic2bim.co.uk/comm_photo)

* input
  * HTTPS, POST
  * parameters
    * task_id – number – task identificator
    * user_id – number – user identificator
    * photos – array
      * note – string – photo note
      * lat – float – photo latitude
      * lng – float – photo longitude
      * centroidLat
      * centroidLng
      * altitude
      * bearing
      * magnetic_azimuth
      * photo_heading
      * pitch
      * roll
      * photo_angle
      * orientation
      * horizontalViewAngle
      * verticalViewAngle
      * accuracy
      * deviceManufacture
      * deviceModel
      * devicePlatform
      * deviceVersion
      * satsInfo
      * extraSatCount
      * NMEAMessage
      * networkInfo
      * created – datetime – date of photo creation
      * digest – string – photo hash
      * efkLatGpsL1
      * efkLngGpsL1
      * efkAltGpsL1
      * efkTimeGpsL1
      * efkLatGpsL5
      * efkLngGpsL5
      * efkAltGpsL5
      * efkTimeGpsL5
      * efkLatGpsIf
      * efkLngGpsIf
      * efkAltGpsIf
      * efkTimeGpsIf
      * efkLatGalE1
      * efkLngGalE1
      * efkAltGalE1
      * efkTimeGalE1
      * efkLatGalE5
      * efkLng GalE5
      * efkAlt GalE5
      * efkTimeGalE5
      * efkLatGalIf
      * efkLngGalIf
      * efkAltGalIf
      * efkTimeGalIf
      * photo – string – base64 encoded photo
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * photo_id – number – ID of received photo

#### receive task data from phone

[<u>https://pic2bim.co.uk/comm_status</u>](https://pic2bim.co.uk/comm_status)

* input
  * HTTPS, POST
  * parameters
    * task_id – number – task identificator
    * status – string – task statuses
    * note – string – task note
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs

#### sends IDs of unassigned photos for user

[<u>https://pic2bim.co.uk/comm_unassigned</u>](https://pic2bim.co.uk/comm_unassigned)

* input
  * HTTPS, POST
  * parameters
    * user_id – number – user identificator
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * photos_ids – array of numbers – IDs of unassigned photos

#### Save LPIS Data

[<u>https://pic2bim.co.uk/comm_lpis</u>](https://pic2bim.co.uk/comm_lpis)

* input
  * HTTPS, POST
  * parameters
    * identificator – string – identificator
    * pa_description – text – Description
    * wkt – text – wkt data
    * wgs_geometry – json – wgs coordinates 
    * wgs_max_lat – float – max latitude
    * wgs_min_lat – float – min latitude
    * wgs_max_lng – float – max longitude
    * wgs_min_lng – float – min longitude
* output
  * JSON
    * status – string  *  ok/error
    * error_msg – string – error message if an error occurs
    * lpis_id – integer – IDs of created record

#### Get LPIS Data

[<u>https://pic2bim.co.uk/comm_get_lpis</u>](https://pic2bim.co.uk/comm_get_lpis)

* input
  * HTTPS, POST
  * parameters
    * bbox – string – bbox coordinates
    * numberOfRecords – integer – Number of records
* output
  * JSON

### Database Tables
#### Page Paying Agency (PA)
```
-- Struttura della tabella `pa`
--

CREATE TABLE `pa` (
  `id` bigint NOT NULL,
  `name` varchar(255) NOT NULL,
  `timestamp` datetime NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
```

```
-- Dump dei dati per la tabella `page`

INSERT INTO `page` (`id`, `name`, `timestamp`) VALUES
(1, 'login', '2021-04-27 14:52:07'),
(2, 'list farmářů', '2021-04-27 14:52:07'),
(3, 'seznam úkolů', '2021-04-27 14:52:07'),
(4, 'popup mapy', '2021-04-27 14:52:07'),
(5, 'detail úkolu', '2021-04-27 14:52:07'),
(6, 'base šablona', '2021-04-27 14:52:07'),
(7, 'galerie neprirazenych fotek', '2021-04-27 14:53:31'),
(8, 'cesty', '2021-04-27 14:53:31'),
(9, 'správa agentur', '2021-04-27 14:53:31'),
(10, 'správa PA officer', '2021-04-27 14:53:31'), 
(11, 'release notes', '2021-04-27 14:53:31'),
(91, 'PHOTO_PDF_EXPORT', '2021-04-27 14:53:31');
```


[[Web-Console]]

### Updates to Photo response
* Currently APIs are returning the photo as the base64string, going forward a photo link will be sent in the response so wherever we are using the photo as base64string, we need to replace it with the link.
* A new attribute will be added in the response named as "link" which will contain the link to photo
* "photo" attribute will be removed from the APIs response going forward to optimize the APIs.

### Migration of Typescript code with next.js to Laravel
#### Step by step instructions

Migrating a Next.js application to a Laravel Inertia.js application with React involves several steps. This guide is based on the APIs developed in Laravel

* Authentication
  * Authentication system is already implemented so we don't need to migrate that part into Laravel. Just call the Laravel APIs after authentication and Sanctum will take care of the APIs authentication using the cookies in the requests generated by our SPA.
* Layouts
  * Authentication Layout
    * This is intended for use after authentication.
    * This layout file is located at resources/js/Layouts/AuthenticatedLayout.tsx.
  * Guest Layout
    * This is intended for use before authentication.
    * This layout file is located at resources/js/Layouts/GuestLayout.tsx.
  * If you wish to use your own layout file, you can created a new file under resources/js/Layouts and use that accordingly in your components.
* Set Up Routing in Laravel Inertia
  * Translate your Next.js page routes into Laravel routing system using Inertia, Laravel web routes are located inside a file named routes/web.php.
  * For each page in Next.js, create a corresponding Inertia route and React component in your Laravel application.
  * Example
    * Create a route in routes/web.php
    ```
      use App\Http\Controllers\TestController;

      Route::get('/test', [TestController::class, 'index'])->name('test.index');
    ```
    * Create a new controller by running the following command in the terminal
    ```
      php artisan make:controller TestController
    ```
    * Create an index function in test controller to render the react component
    ```
      use Inertia\Inertia;
      use Illuminate\Http\Request;

      public function edit(Request $request)
      {
          $status = "This is my test react page";
          return Inertia::render('Test/index', [
              'status' => $status,
          ]);
      }
    ```
    * Create a react component naed index.tsx at resources/js/Pages/Test. You can use the status variable in your react component as follows
    ```
      import { usePage } from '@inertiajs/react';
      const { status } = usePage<{
        status : string
      }>().props;
    ```
* Move Components
  * Copy over the Next.js components into your existing Laravel Inertia application’s resources/js/Pages directory.
  * Adjust the imports and ensure each component works within the Laravel environment.
* Handle API Calls
  * Since your Next.js app makes API calls, ensure that the API calls in your components continue to work within the Laravel setup. You can reuse your existing APIs or refactor them if necessary.
	* Use Axios (or the same library you are using) in your React components to make these calls, similar to how they were made in Next.js.
* Migrate Global State Management (if applicable)
	* If your Next.js application uses global state management (such as React Context or Redux), move this to your Inertia application.
	* Ensure any global state is accessible across your components in the Inertia setup.
* Define Enivronment variables
  * In Laravel Inertia.js application with React, environment variables are typically defined in the .env file. However, for them to be available in React (client-side), you need to ensure they are prefixed with REACT_APP_.
  ```
    REACT_APP_API_URL=https://api.example.com
    REACT_APP_KEY=your_key_here
  ```
  * In your React components, you can access environment variables using process.env.REACT_APP_variable_name (for example, process.env.REACT_APP_API_URL).
  ```
    const apiUrl = process.env.REACT_APP_API_URL;

    const fetchData = async () => {
        const response = await fetch(`${apiUrl}/data`);
        const data = await response.json();
        console.log(data);
    };

    useEffect(() => {
        fetchData();
    }, []);
  ```
  * If you add or modify environment variables, you will need to restart your React development server for the changes to take effect.
  ```
    npm run dev
  ```
* Deployment
  * Push the code in the repository
  * Take the pull on server
  * Run npm run build in terminal on server.


### Guide to use APIs
Swagger documentation for APIs is available at https://pic2bim.co.uk/api-docs. All APIs except /comm_login are protected by Sanctum authentication. You must authorize with a Bearer token to use the protected APIs.

* How to get a Bearer token
	* Execute the /comm_login API with valid credentials.
	* In the response of /comm_login, you will receive the Bearer token in an attribute named "token".
* How to authorize with a Bearer token in Swagger
	* Click on the "Authorize" button in the top right of Swagger UI. A popup will appear, asking for the Bearer token.
	* Paste the token received from /comm_login there, and you will be authorized to use all the protected APIs.
* How to pass the Bearer token when consuming the APIs
	* The token received from /comm_login must be passed as a header "Authorization" with the value "Bearer {your token}"


### Farmer Registration and Assignment by Officers

* Farmers can register at https://pic2bim.co.uk/register.
* After registration, they receive an email for verification. Once their email is verified, they gain access to the platform.
* Farmers who register through https://pic2bim.co.uk/register initially appear as "Unassigned Farmers" in the officer's dashboard under the "Unassigned Farmers" tab.
* Officers can assign any unassigned farmer to their agency on the "Unassigned Farmers" page by selecting the "+" icon next to the farmer's name.
* Once assigned, the farmer will appear in the officer's user management list.


# Running PIC2BIM on Apache NetBeans (Windows)

## Prerequisites

### Software Requirements
1. Install [Apache NetBeans](https://netbeans.apache.org/).
2. Install [PHP 8+](https://www.php.net/downloads).
3. Install [Node.js and npm](https://nodejs.org/).
4. Install [Composer](https://getcomposer.org/download/).

### Project Setup
1. Verify that the following tools are installed globally:
   - PHP: `php -v`
   - Node.js: `node -v`
   - npm: `npm -v`
   - Composer: `composer -v`

---

## Steps to Run the App

### 1. Clone or Copy the Laravel Project
- Copy or clone your Laravel project into your development folder.
  ```bash
  git clone <repository-url>
  cd <project-folder>
### 2. Install Laravel Dependencies
- Open a terminal in the project root folder and run:
  ```bash
  composer install
### 3. Install Javascript Dependencies
- Install npm dependencies required for React and TypeScript:
  ```bash
  npm install
### 4. Configure environment variables
- Duplicate the .env.example file and rename it to .env:
  ```bash
  cp .env.example .env
- Update the .env file:
  - Set APP_URL to http://127.0.0.1:8000 or your local server URL.
  - Configure your database settings (DB_HOST, DB_PORT, DB_DATABASE, DB_USERNAME, DB_PASSWORD).
### 5. Import Database file into pgsql server

### 6. Run Database Migrations
- Run the migrations to set up the database schema:
  ```bash
    php artisan migrate
### 7. Configure Netbeans
  - Open Apache NetBeans.
  -	Go to File > Open Project and select your Laravel project folder.
  -	Right-click the project in the Projects panel and select Properties.
  -	Under the Run Configuration section:
    -	Set the PHP Interpreter to the path of your php.exe file (e.g., C:\php\php.exe).
    - Set the Project URL to http://localhost/<your-project-folder>.
### 8. Configure Node.js in NetBeans
  - Go to Tools > Options > JavaScript.
	-	Under the Node.js tab:
	  -	Set the Node Path to the location of your Node.js executable (e.g., C:\Program Files\nodejs\node.exe).
### 9. Start Laravel Development Server
  ```
    php artisan serve
  ```
  - This will start the backend server at http://127.0.0.1:8000.

### 10. Run Frontend Development Server
  ```
    npm run dev
  ```
  - This will compile React and TypeScript assets.

## Debugging
### For PHP 	
  - Use the built-in debugger in NetBeans:
  - Right-click your project and choose Debug.
### For Frontend 	
  - Use browser developer tools to debug React and TypeScript components.

## Notes
- Run npm run build for production builds.
- Ensure all required ports are open and not blocked by a firewall.
- For troubleshooting:
  - Verify .env configuration.
  - Ensure php artisan serve and npm run dev are running.
	- Check for errors in the browser console or terminal.
