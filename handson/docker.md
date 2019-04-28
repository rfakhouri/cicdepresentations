# Docker Hands-On

In this hands on activity you will learn how to use Docker to pull and run images for standing up and testing out systems. You'll also learn how to use Containerize a basic web site. You'll also learn how to use docker-compose to bring up a semi-complex web application.


## Part 1 Pulling an image

0. Use the docker hub to pull down the `ghost` image with the `alpine` tag
    - https://hub.docker.com
0. Run the image you just pulled down and map it to a local port, you can use the instructions found on the ghost docker hub page under the section *Custom Port*.  
    **Please note** you will need to set the `url` environment variable for ghost to work properly, you can see instructions under the *Configuration* section. If you set the `Custom Port` to the port specified in the *Custom Port* section your `url` will be `http://localhost:3001`.
