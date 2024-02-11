# Building an ecommerce store using Nuxt and Medusa

## Introduction

[Nuxt]() is a meta-framework built on top of [Vue.js](), a JavaScript library. It features SSR, SSG, SEO, File-System routing, Caching etc. It can be used to build ecommerce storefronts.

[Medusa]() is a toolkit for developers to create digital commerce applications. It uses a Node.js backend with the core API, plugins, and modules installed through npm.

In this project, you will learn how an ecommerce store can be built using Nuxt for the frontend and Medusa for the backend. To do that, first, you will create a Nuxt project and set a few components, pages and layouts. Then, you will link the Nuxt project with a Medusa server to get the store products and display them on the home page including a product's page, and a product detail page.

## Prerequisites

To follow along with the tutorial you need to have some knowledge of the following:
- Basic understanding of HTML, CSS, and JavaScript
- Basic understanding of [Node.js]() and [npm]()
- Basic understanding of the command line
- Knowledge of Vue and Nuxt is a bonus but not a requirement.
- Knowledge of Medusa is a bonus but not a requirement.

In addition to knowing these tools, your computer system should have the following packages installed:
- [Node.js]() (v16 and above) 
- [PostgreSQL](). Alternatively, you can create a free PostgreSQL database with a [Neon]() account. This tutorial will use a database created using Neon.
- [yarn]() (optional)
- [git]() (optional)

Before proceeding with the tutorial you can check out the following links for useful resources:
- [Video demo]().
- [Live link of the app]().
- [Git repo containing the project source code]().

## Install and setup the Medusa Backend

In this step you will install and set up the Medusa Server backend. 

Open up your terminal and create a project folder to contain all the source code for the entire project. Name it `my-store`.

```bash
mkdir my-store
```

### Set up PostgreSQL on Neon

If you have PostgreSQL installed locally, you can skip this step. 

Visit the [Neon - Sign Up](https://console.neon.tech/signup) page and create a new account.

[Create a new project](https://console.neon.tech/app/projects) in the Neon console. Give your project a name like `mystore` and your database a name like `mystoredb` then click **Create project**.

Take note of your connection string which will look something like: `postgresql://dominggobana:JyyuEdr809p@df-hidden-bonus-ertd7sio.us-east-3.aws.neon.tech/mystoredb?sslmode=require`. It is in the form `postgres://[user]:[password]@[host]/[dbname]`.You will provide connection string as a database URL to your Medusa server.

### Install Medusa CLI

In your terminal, inside the `my-store` folder run the following command to install the Medusa CLI. We will use it to install the Medusa server.

```bash
npm install @medusajs/medusa-cli -g
```

### Create a new Medusa project

```bash
medusa new my-medusa-store
```

You will be asked to specify your PostgreSQL database credentials. Choose "Skip database setup".

A new directory named `my-medusa-store` will be created to store the server files

### Configure Database

Add the connection string as the `DATABASE_URL` to your environment variables. Inside `my-medusa-store` create a `.env` file and add the following:

```
DATABASE_URL=postgresql://dominggobana:JyyuEdr809p@df-hidden-bonus-ertd7sio.us-east-3.aws.neon.tech/mystoredb?sslmode=require
```

Run migrations and seed data to the database by running the following command:

```bash
medusa seed --seed-file="./data/seed.json"
```

### Start your Medusa backend

```bash
medusa develop
```

The Medusa server will start running on port `9000`.

Test your server:
```bash
curl localhost:9000/store/products
```

If it is working, you should see a list of products.

## Install and Serve Medusa Admin with the Backend

This section explains how to install the admin to be served with the Medusa Backend.

### Install the package

Inside `my-medusa-store` stop your Medusa server, `CTRL + C` and run the following command to install the Medusa Admin Dashboard.

```bash
npm install @medusajs/admin
```

Test your install by re-running your server.
```bash
medusa develop
```

Open up your browser and visit `localhost:7001` to see the Medusa Admin Dashboard. Use the Email `admin@medusa-test.com` and password `supersecret` to log in.

![Medusa Admin Dashboard](/medusa-admin-dashboard.png)

## Install and setup the Nuxt.js storefront

### Install a Nuxt.js project

Create a Nuxt project, by running the following command inside the `my-store` directory:
```bash
npx nuxi@latest init my-nuxt-storefront
```

### Run Nuxt.js project

Once the Nuxt.js project is created, change to the directory of the storefront and start the Nuxt.js project:
```bash
cd my-nuxt-storefront
npm install
npm run dev -- -o
```

This command will run the Nuxt.js frontend on port `3000`. To test it, open your browser and visit `localhost:3000`. 

![Nuxt default frontend](nuxt-default-frontend.png)

## Make the Storefront Layout










