### Sign in
To sign in into RunADock you have to use your username or email address of your GitHub account. With this information we will direct you to the GitHub login using the OAuth2 functionality. With the login to GitHub you give the permission that RunADock is allowed to use your GitHub account information. After your confirmation you will be redirected back to RunADock and we will create your RunADock account and send you an email with a confirmation link. After clicking the confirmation link we will ask you for your credit card information. Only with this information we are able to provide you the full service including the 120 minutes free of charge.

### Authorization key
You need an authorization key to run docker containers using our RunADock interfaces. You can find your authorization key after successful sign up within the Token menu. At the Token site you can create additional tokens, and also delete tokens.

### Using CLI
We provide you a CLI for using our RunADock. You can find a CLI for Windows, Mac/OS, and Linux. There are two possibilities to get the CLI:

  - download and unzip the CLI of your need from our mainpage <https://runadock.io>
  - copy the CLI from our github project using the git clone command with the address https://github.com/runadock/runadock-cli

#### 
To use the CLI you have to build the application first. Go into the directory where you have unzipped the CLI source and start the build with the command

    $ ./build

Next you have to set the environment variables 

    RUNADOCK_USER=<your username of RunADock>
and 

    RUNADOCK_TOKEN=<your authorization key can be found at https://dev.runadock.io/terminal/#/tokens>

Now you are ready to start a container with the following command:

    $ ./runadock run --source <source to the container>

Example:

    $ ./runadock run --source nginx
    $ created: 7e08492e-5db9-489d-9652-90f133df8bea

The return value is the id of your run created by RunADock. There are the following optional parameter available for the run command:

--name      arbitrary name of the container
--size      size of the container with the possible arguments XS (default), S, M, L
--plan      plan for the container with the possible arguments STARTER (default), DEDICATED

You can use the id to check for more details on your container using the command inspect

    $ ./runadock inspect --id <id of the container to inspect>

Example:

    $ ./runadock inspect --id 7e08492e-5db9-489d-9652-90f133df8bea
    {
      "id": "7e08492e-5db9-489d-9652-90f133df8bea",
      "containerId": "7da774585c29d069593649a54ce918d8e2ef5b971a916a6ce666484813c5d775",
      "name": "",
      "publicDns": "7da774585c.c.runadock.io",
      "ip": "37.187.250.7",
      "source": "nginx",
      "state": "RUNNING",
      "cpuShares": 128,
      "memory": 512,
      "diskSize": 5,
      "ordered": 1422016066087,
      "created": 1422016068075,
      "terminated": 0,
      "orderedBy": "runadock-guest1",
      "plan": "Starter",
      "owner": {
        "id": "b88de4f9-25e8-491e-a8c9-d62f478300b9",
        "firstName": "Demoaccount",
        "lastName": "RunADock",
        "street": "am Bay",
        "zip": "65712",
        "city": "Taindorf",
        "country": "Deutschland",
        "houseNumber": "1",
        "username": "runadock-guest1",
        "email": "runadock_guest1@yahoo.com",
        "verifyToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJydW5hZG9jay1ndWVzdDEiLCJpYXQiOjE0MTg3MzQwODIzMDZ9.oIrjTVoAcku5dchayL7WN7tZxB2gO1uFE2iWVRawtyM=",
        "countryCode": "DE",
        "receiveEmail": true,
        "admin": false,
        "emailVerified": false
      },
      "ports": [
        {
          "id": "8ab86c18-af85-412c-8206-b9463844b927",
          "privatePort": 49909,
          "publicPort": 443,
          "scheme": "tcp"
        },
        {
          "id": "32fb327c-d407-4a91-b05f-fca2a9e6f0c2",
          "privatePort": 49910,
          "publicPort": 80,
          "scheme": "tcp"
        }
      ],
      "env": [],
      "cmd": [],
      "pricePerMinute": {
        "amount": 0.000115,
        "currency": "EUR"
      },
      "pricePerOrder": {
        "amount": 0.05,
        "currency": "EUR"
      },
      "cost": {
        "amount": 0.000805,
        "currency": "EUR"
      },
      "buildLog": ""
    }

As you can see there are two id parameter. The first parameter *id* is the RunADock-ID of your run. The parameter *containerId* is the ContainerID of your container running by Docker.

For stopping a container you can use the kill command:

    $ ./runadock kill --id <id of the container to kill>

Example:

    $ ./runadock kill --id 
    $

Last but not least we also provide a command to list all your running and stopped containers. Use

    $ ./runadock ps

and you will get the following output:

    ContainerID  SOURCE                                                       CREATED              STATUS   DNS                       PORTS           NAME
    9f3087c1ec4  nginx                                                        2015-01-23 14:18:52  RUNNING  9f3087c1ec.c.runadock.io  443->49915/tcp  
    e9161e7a743  https://github.com/dockerfile/nginx                          2015-01-23 10:54:09  RUNNING  e9161e7a74.c.runadock.io  443->49907/tcp  testtest
    248d3615301  nginx                                                        2015-01-23 14:30:03  RUNNING  248d361530.c.runadock.io  443->49917/tcp  
    4bb03cd80d8  https://github.com/runadock/dockerfiles/tree/master/itworks  2015-01-14 12:36:04  RUNNING  4bb03cd80d.c.runadock.io  443->49886/tcp  Torn1




### Java


### curl
