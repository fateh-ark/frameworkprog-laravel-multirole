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
  * [Database](#database)
  * [Interfaces](#external-interfaces)

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

This project contains two entities/models, which as below. You can also click on the hyperlinks to see the code a closer look.

- [**User**](/blog/app/Models/User.php)<br>
This entity contains datas relating to authentication such as name, email, and password. This entity also has role attribute which used to differentiate role between users for different permissions.

- [**Product**](/blog/app/Models/Product.php)<br>
This entity contains the name and detail of a product that interchangeable. Not much else goes here.

### Controllers

Overall this project contains four controllers, which are all an extension of [**Controller**](/blog/app/Http/Controllers/Controller.php), an extension of the BaseController with additional Middlewares such as `AuthorizeRequests` and `ValidateRequests`. The controllers are as follows:

- [**HomeController**](/blog/app/Models/User.php)<br>
This controller functions to check wether the user has been authenticated/logged using the `\App\Http\Middleware\Authenticate` middleware whenever a user try to access the Homepage, providing access to all autheticated users.

- [**ProductController**](/blog/app/Models/User.php)<br>
This controller handles actions relating to the manipulation of the data of a **Product** entity such as the **creation, storing, showing, editing, updating, and deletion** of it from a given request. This controller also contains the use of a couple of `\Spatie\Permission\Middlewares\PermissionMiddleware` middlewares that checks the user's permissions on what action they are allowed to do in the product page.

- [**RoleController**](/blog/app/Models/User.php)<br>
This controller handles actions relating to the manipulation of the data of a **Role** such as the **creation, storing, showing, editing, updating, and deletion** of a role from a given request. Like the previous, this controller also contains the use of a couple of `\Spatie\Permission\Middlewares\PermissionMiddleware` middlewares that checks the user's permissions on what action they are allowed to do in the role manager page.

- [**UserController**](/blog/app/Models/User.php)<br>
Similar to the previous two controllers, this controller handles actions relating to the manipulation of the data of a **User** entity such as the **creation, storing, showing, editing, updating, and deletion** of it from a given request. This controller also contains the use of a couple of `\Spatie\Permission\Middlewares\PermissionMiddleware` middlewares that checks the user's permissions on what action they are allowed to do in the user page.

### Middlewares

Though there are a lot of middlewares that are used in this project, the three main ones are as follows:

```php
...
protected $middlewareAliases = [
    ...
    'role' => \Spatie\Permission\Middlewares\RoleMiddleware::class,
    'permission' => \Spatie\Permission\Middlewares\PermissionMiddleware::class,
    'role_or_permission' => \Spatie\Permission\Middlewares\RoleOrPermissionMiddleware::class,
];
...
```

- **role**
- **permission**
- **role_or_permission**

these middlewares handle the multirole and permision management capability of the project.

### Database

Overall the main database used in this project consist of 7 tables. The tables Are as follows:

#### 1. users

The users table stores the attributes of the **User** entity. Contains 8 attributes.

| Name              | Type         | Description                    |
| ----------------- | ------------ | ------------------------------ |
| id                | bigint(20)   | The user's id number           |
| name              | varchar(255) | The user's username            |
| email             | varchar(255) | The user's email address       |
| email_verified_at | timestamp    | When was the email verified    |
| password          | varchar(255) | The user's password            |
| remember_token    | varchar(100) | The user's remember token      |
| created_at        | timestamp    | When was the user created      |
| updated_at        | timestamp    | When was the user last updated |

#### 2. roles

The roles table store the attributes for the different types of **roles**. Contains 5 attributes.

| Name       | Type         | Description                    |
| ---------- | ------------ | ------------------------------ |
| id         | bigint(20)   | The role id number             |
| name       | varchar(255) | The role name                  |
| guard_name | varchar(255) | The role user-agent            |
| created_at | timestamp    | When was the role created      |
| updated_at | timestamp    | When was the role last updated |

#### 3. products

The products table stores the attributes of the **Product** entity. Contains 5 attributes.

| Name       | Type         | Description                       |
| ---------- | ------------ | --------------------------------- |
| id         | bigint(20)   | The product's id number           |
| name       | varchar(255) | The product's name                |
| detail     | text         | The product details               |
| created_at | timestamp    | When was the product created      |
| updated_at | timestamp    | When was the user product updated |

#### 4. permissions

The permissions table store the attributes for the different types of **permissions**. Contains 5 attributes.

| Name       | Type         | Description                          |
| ---------- | ------------ | ------------------------------------ |
| id         | bigint(20)   | The permission id number             |
| name       | varchar(255) | The permission name                  |
| guard_name | varchar(255) | The permission user-agent            |
| created_at | timestamp    | When was the permission created      |
| updated_at | timestamp    | When was the permission last updated |

#### 5. roles_has_permissions

The permissions table is an intermediary between the **permissions table** and **role table**, to define what role has what permissions. Contains 2 attributes.

| Name          | Type       | Description              |
| ------------- | ---------- | ------------------------ |
| permission_id | bigint(20) | The permission id number |
| role_id       | bigint(20) | The role's id number     |

### 6. models_has_roles

The permissions table is an intermediary between the **users table** and **role table**, to define what users has what roles. Contains 3 attributes.

| Name       | Type         | Description          |
| ---------- | ------------ | -------------------- |
| role_id    | bigint(20)   | The role's id number |
| model_type | varchar(255) | The model type       |
| model_id   | bigint(20)   | The user's id number |

#### 7. models_has_permissions

The permissions table is an intermediary between the **users table** and **permissions table**, to define what users has what permissions. Contains 3 attributes.

| Name          | Type         | Description              |
| ------------- | ------------ | ------------------------ |
| permission_id | bigint(20)   | The permission id number |
| model_type    | varchar(255) | The model type           |
| model_id      | bigint(20)   | The user's id number     |

### External Interfaces
