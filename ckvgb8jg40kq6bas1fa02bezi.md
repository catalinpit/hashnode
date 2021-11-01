## Deploy a PostgreSQL Database on Heroku

Heroku Postgres is an SQL database service that allows you to use a relational database such as PostgreSQL on the Heroku platform.

The Heroku Postgres service is a great option when you need a hosted database for your projects, MVPs or proofs-of-concept.

Heroku has several pricing plans for this service, including a free plan. This article teaches you how to deploy a free PostgreSQL database on Heroku.

## Create a new application

The first step is to create a new application on Heroku. To do that, log in to your Heroku account and go to the dashboard.

You can either access your existing applications from the dashboard *(if you have any)* or create new applications.

![Heroku Dashboard Create New App](https://cdn.hashnode.com/res/hashnode/image/upload/v1635513380212/PTnBj3CtT.png)*Figure 1*

In this case, you need to create a new application for the database. Click on the "New" button and choose "Create new app", as shown in figure 1.

After that, it prompts you to:
* Choose a name for your application
* Select a region

Once you choose a name and a region for your application, press on "Create app".

![Heroku Create New Application Name and Region](https://cdn.hashnode.com/res/hashnode/image/upload/v1635513438935/fW7802UN6.png)*Figure 2*

After clicking the button, Heroku creates the application in the background. It takes seconds to create the application, and then it takes you to the app's dashboard.

![Heroku Application Dashboard](https://cdn.hashnode.com/res/hashnode/image/upload/v1635516874302/shbEPH6eT.png)*Figure 3*

Figure 3 illustrates my application's dashboard.

## Add PostgreSQL

The next step is to add PostgreSQL to the application. 

You can install add-ons to your application from the "Resources" page. In figure 3, you can see the option "Resources" next to "Overview" and under the application name. Click on it.

Once you are on the "Resources" page, go to the "Add-ons" section and search for "Postgres", as shown in figure 4.

![Heroku Postgres - Add PostgreSQL Add-on on Heroku](https://cdn.hashnode.com/res/hashnode/image/upload/v1635513600054/xDMNqeKdM.png)*Figure 4*

From the drop-down, choose the option "Heroku Postgres". When you click on it, a new pop-up appears from where you can select plans. Figure 5 illustrates the pop-up.

Choose the `Hobby Dev` plan, which is the free plan. This plan is more than enough for side projects, MVPs or proofs-of-concept.

![Heroku Postgres - Set up PostgreSQL plan](https://cdn.hashnode.com/res/hashnode/image/upload/v1635513524061/CI3gvA7bD.png)*Figure 5*

Click "Submit Order Form" and you are done. The PostgreSQL database is created and ready to be used.

## Database credentials

You need to grab the database credentials to connect your applications to the database.

Go back to your application dashboard and click on "Heroku Postgress", as illustrated in figure 6.

![Heroku Application Dashboard](https://cdn.hashnode.com/res/hashnode/image/upload/v1635516999615/XOyZzBLOz.png)*Figure 6*

That takes you to the database's dashboard page. On this page, you can see information such as:
* the health of the database
* the number of connections
* data size

See figure 7 for reference.

![Heroku PostgreSQL Database Overview Page](https://cdn.hashnode.com/res/hashnode/image/upload/v1635517511967/AYm4S917D.png)*Figure 7*

To get the database details, click on the "Settings" option. On the settings page (shown in figure 8), you can:
* reset your database
* destroy your database
* get the database credentials.

![Heroku PostgreSQL Database Settings Page](https://cdn.hashnode.com/res/hashnode/image/upload/v1635517645029/aFzJsGvGN.png)*Figure 8*

The last step is to click on the button "**View Credentials...**" to get the database information.

![Heroku Postgres Database Credentials](https://cdn.hashnode.com/res/hashnode/image/upload/v1635608476377/31960_Q3p.png)*Figure 9*

Figure 9 illustrates what you should see when you press the "**View Credentials...**" button.

## Connect to the database

There are multiple ways to connect to the database. It depends on what operating system and application you are using.

In my case, I use Postico on MacOS. When using Postico, you can copy the **URI** (see figure 9) and paste it into your browser's address bar. That automatically creates a database connection in Postico.

![Postico Database Connection](https://cdn.hashnode.com/res/hashnode/image/upload/v1635609024936/Ysx48hqw1.png)*Figure 10*

Figure 10 illustrates what you should see when you access the **URI** in the browser. Press "Connect" and you can start using the database.

Alternatively, you can manually enter the database details (from figure 9) in Postico.

![Entering Heroku Postgres database details in Postico](https://cdn.hashnode.com/res/hashnode/image/upload/v1635612133343/9EPD7Hsss.png)*Figure 11*

From Postico, you can create tables, add data into your database, perform SQL operations, and more.

It may come in handy to learn [how to set environment variables on Heroku](https://catalins.tech/heroku-environment-variables) if you decide to deploy applications on the platform. Alternatively, you might run the "[No pg_hba.conf entry for host, SSL off](https://catalins.tech/nodejs-postgresql-heroku-error-no-pghbaconf-entry-for-host-ssl-off)" error when you deploy your Node.js and PostgreSQL application on Heroku.