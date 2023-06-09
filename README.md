# Framework Programming - Laravel Multirole

Muhammad Fatih Akbar <br>
5025201117

Framework Programming IUP

Based on [Laravel 8 User Roles and Permissions Tutorial](https://www.itsolutionstuff.com/post/laravel-8-user-roles-and-permissions-tutorialexample.html).

----

## Table of contents

- [Table of contents](#table-of-contents)
- [Installation and Startup](#installation-and-startup)
- [Usage](#usage)
- [Breakdown](#breakdown)
  * [Entities](#entities)
  * [Controllers](#controllers)
  * [Middlewares](#middlewares)
  * [Other Libraries](#other-libraries)
  * [Database](#database)
  * [Interfaces](#interfaces)

## Installation and Startup

Clone the repo, then in the app directory run the command below in a new terimal window.

```sh
npm install && npm run dev
```

Secondly, open up a second terminal and to install all of the needed dependencies, make sure you have Composerly installed and run the following command

```sh
composer install
```

Then create an `.env` file by creating manually, then copy the contents of `.env.example`.

Run you database server, as an example the MySQL server in XAMPP, then migrate and seed the database by running the following commands

```sh
php artisan migrate
```

To start and run the app, run the following command

```sh
php artisan serve
```

## Usage

## Breakdown

### Entities

This project contains two entities/models, which as follows:

- [**User**](/blog/app/Models/User.php)<br>
This entity contains datas relating to authentication such as name, email, and password. This entity also has role attribute which used to differentiate role between users for different permissions.

- [**Product**](/blog/app/Models/Product.php)<br>
This entity contains the name and detail of a product.

### Controllers

### Middlewares

### Other Libraries

### Database

### Interfaces
