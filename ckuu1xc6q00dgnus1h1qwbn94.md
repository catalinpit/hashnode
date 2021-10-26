## Node.Js + PostgreSQL + Heroku Error: No pg_hba.conf entry for host, SSL off

If you deploy your Node.Js and PostgreSQL application on Heroku, you might run into the following error:

> error: no pg_hba.conf entry for host "93.68.220.97", user "dbusername", database "musicdb", SSL off

Your error will differ slightly because your host, user and database name will be different from mine.

With that being said, let's see how you can fix it and make your application work.

## Solution

In this example, we use the "pg" package. Thus, let's say you create a new pool with the following configuration:

```javascript
const { Pool } = require('pg');
require('dotenv').config()

const pool = new Pool({
    user: process.env.POSTGRES_USER,
    host: process.env.POSTGRES_HOST,
    database: process.env.POSTGRES_DB,
    password: process.env.POSTGRES_PASSWORD,
    port: process.env.POSTGRES_PORT,
});
```

If you run the application now, you get an error.

The solution to the error is to add a new property to the pool configuration. All you need to do is to pass the following SSL configuration object to the `pool` constructor:

```
ssl: {
    rejectUnauthorized: false,
}
```

Now, your pool configuration should look as follows:

```javascript
const pool = new Pool({
    user: process.env.POSTGRES_USER,
    host: process.env.POSTGRES_HOST,
    database: process.env.POSTGRES_DB,
    password: process.env.POSTGRES_PASSWORD,
    port: process.env.POSTGRES_PORT,
    ssl: {
        rejectUnauthorized: false,
    }
});
```

Save the changes, and you are done. Your application should run without problems now.

## Bonus - Sequelize solution

The above solution is for the "pg" raw driver, but if you use an ORM like Sequelize, the solution syntax differs a bit.

```javascript
const Sequelize = require('sequelize');

const sequelize = new Sequelize({
    database: process.env.POSTGRES_DB,
    username: process.env.POSTGRES_USER,
    password: process.env.POSTGRES_PASSWORD,
    host: process.env.POSTGRES_HOST,
    port: process.env.POSTGRES_PORT,
    dialect: "postgres",
    dialectOptions: {
        ssl: {
            require: true,
            rejectUnauthorized: false
        }
     },
});
```

The above code snippet shows how to solve the error when using Sequelize.

## Alternative

You can omit the SSL configuration object by running `heroku config:set PGSSLMODE=no-verify` in the Heroku CLI.

If you do not know how to do that, you can read this article to [learn how to set environment variables on Heroku](https://catalins.tech/heroku-environment-variables).