## How to Run WordPress Locally on macOS With Docker Compose

WordPress is a free and open-source content management system that you can use to create websites and blogs. In this article, you will learn how to run WordPress on your Mac device with Docker Compose.

## Docker Installation

The first step is to install Docker on your device. If you already have Docker installed, you can skip the section. Otherwise, go to the [Docker website](https://docs.docker.com/desktop/mac/install/) and download Docker Desktop.

Follow the installation instructions and once it's done, open the application.

![Screenshot of Docker Desktop on Mac](https://cdn.hashnode.com/res/hashnode/image/upload/v1648886195777/pwNzPcU-J.png)

The above image illustrates what you should see when you open the application. In the next step, you will configure WordPress with Docker.

## Setup WordPress with Docker Compose

To use WordPress locally, you need to create a "docker-compose" file. Go to your preferred folder and create the Docker file as follows:

```
touch docker-compose.yml
```

Now open the newly created file and add the following code:

```
version: "3.9"
    
services:
```

The "version" from the top of the file specifies the version of the Compose file format. Things like the file structure, permitted configuration keys, and the compose behaviour depends on the version specified in the "docker-compose" file.

When it comes to "services", we will use two services:
* MySQL
* WordPress

Add the remaining code in the `docker-compose.yml` file:

```
version: "3.9"
    
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: dbpassword
      MYSQL_DATABASE: wordpress_local
      MYSQL_USER: wordpress_db_user
      MYSQL_PASSWORD: wordpress_db_password
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress_db_user
      WORDPRESS_DB_PASSWORD: wordpress_db_password
      WORDPRESS_DB_NAME: wordpress_local
volumes:
  db_data: {}
  wordpress_data: {}
```

Save the file and you are ready to run WordPress locally! To do so, run the following command in your terminal:

```
docker-compose up -d
```

After the command finishes, WordPress should be available at `localhost:8000`.

![Screenshot 2022-04-04 at 20.58.01.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649095347275/mI3MFjBin.png)

You can proceed further and install WordPress. Once it's installed, you can use it for things such as local WordPress development.

## Error: No Matching Manifest For linux/arm64/v8

If you use a Mac device with the "M1" processor or any "M" processor, you might encounter an error.

> ERROR: no matching manifest for linux/arm64/v8 in the manifest list entries

One way to solve the issue is to add the `platform` key for the database. See the updated version:

```
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: dbpassword
      MYSQL_DATABASE: wordpress_local
      MYSQL_USER: wordpress_db_user
      MYSQL_PASSWORD: wordpress_db_password
    platform: linux/x86_64
```

Now you can re-run `docker-compose up -d`, and it should work!
