# Docker Hands-On

In this hands on activity you will learn how to use Docker to pull and run images for standing up and testing out systems. You'll also learn how to use Containerize a basic web site. You'll also learn how to use docker-compose to bring up a semi-complex web application.


## Part 1 Pulling an image

0. Use the docker hub to pull down the `ghost` image with the `alpine` tag
    - https://hub.docker.com
0. Run the image you just pulled down and map it to a local port, you can use the instructions found on the ghost docker hub page under the section *Custom Port*.  
    **Please note** you will need to set the `url` environment variable for ghost to work properly, you can see instructions under the *Configuration* section. If you set the `Custom Port` to the port specified in the *Custom Port* section your `url` will be `http://localhost:3001`.

## Part 2 Creating a custom docker image. 

0. Create a `Dockerfile` `FROM` the `nginx:alpine` image.
0. Download the file to use for the demo: https://raw.githubusercontent.com/CalvinRodo/cicdepresentations/master/example/index.html
   Linux users can run the following command to download the file `wget https://raw.githubusercontent.com/CalvinRodo/cicdepresentations/master/example/index.html` you need to download it to the same location as your `Dockerfile`. This should work on a mac but you might have to run `brew install wget` first. It *should* also work on a windows machine in a Git Bash prompt, otherwise you'll have to download it by hand, honestly I've never bothered to find out if you can do it on windows.
0. `COPY`  the `index.html` to `/usr/share/nginx/html/`
0. Build the image and tag it with `example:1`
0. Run the Image and map the internal port 80 to external port 1337 making sure to clean up the image when you are down with `--rm`
0. Navigate to http://localhost:1337
  
## Part 3 Connecting two applications together using Docker Compose 

0. Copy the text at the bottom of this lesson to a docker-compose.yml file. 
0. Download the following seed file for the database: https:// https://raw.githubusercontent.com/CalvinRodo/cicdepresentations/master/example/seed.sql and place it in a  `postgres-seed` folder below the docker-compose.yml file.
0. Run `docker-compose up` to run your database and navigate to `http://localhost:8081` to see your brand spanking new seeded Postgres database.

```yml
version: '3'
services:
  postgres-database:
    container_name: postgres-database
    restart: always
    image: postgres:alpine
    ports:
      - 5432:5432
    volumes:
      - $HOME/docker/volumes/postgres:/var/lib/postgresql/data
      - ./postgres-seed:/docker-entrypoint-initdb.d #run these scripts on first container creation
    environment: 
      - POSTGRES_PASSWORD=docker
  pgweb:
    container_name: pgweb  # optional
    restart: always  # optional
    image: sosedoff/pgweb
    ports: 
      - "8081:8081" 
    links: 
      - postgres-database:db  # my database container is called postgres, not db
    environment:
      - DATABASE_URL=postgres://postgres:docker@db:5432/postgres?sslmode=disable
    depends_on:
      - postgres-database # my database container is called postgres, not db
```


