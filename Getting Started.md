## Getting-In RunADock

RunADock can be used to start and run docker containers. In the following you will find an example on how to use our RunADock terminal.
If you are interessted in Docker itself, please visit https://www.docker.com

Note: We provide our service to open source developers and administrators. So appropriate technical knowledge is required to use it.

#### Example: The little web server
In our example we will run a small web server including a web site. The web server is based on NGINX. The docker file can be viewed in https://github.com/dockerfile/nginx

There you will find the docker file with the description of the container build.

Now start with the following steps:

1. Open RunADock: https://runadock.io
2. Log in with the following credentials:

    * user name: runadock-guest1
    * password: use the password you have received via email

3. After successful log-in you will be guided to our Welcome site. Please check that you have already accepted our terms.
4. Now you can start our RunADock terminal. Open the Containers site using the button "Create a container".
5. To start a container you have to fill out the form:

    * source: https://github.com/dockerfile/nginx
    * name: myfirstcontainer
    * now click the button Create

6. After refreshing the terminal site the list of running containers contains now the recently started container.
7. To open the web site of the container you have to use the entries Public DNS and Ports in the following way:

    [public dns]:[ports], in example: e9161e7a74.c.runadock.io:49908

Please consider: for our example you have to use the entry for port 80.

If you have copied correctly you can see the site "Welcome to nginx on Debian!".

#### out of charge

In case your quota is exhausted you can order new contingents on our Billing page. Just open the site using the menu item. At Billing site you can choose between 5, 10, 25, or 50 Euro. After clicking on "Charge" the Novalnet application will be started. Please follow the provided process.

Usually you will get a confirmation about your successful charge. Further you can see your actual balance at the Billing site.

