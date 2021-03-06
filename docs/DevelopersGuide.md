Developers Guide
================

Overview
--------

runadock.io provides different possiblities to start and run docker containers. The web application provides a        comfortable way for a quick start. Further there is a REST-API which can be accessed via CLI, cURL and Java.

Sign in
-------

To sign in into runadock.io you have to use your username or email address of your GitHub account. This information will direct you to the GitHub login using the OAuth2 functionality. With the login to GitHub you give the permission that runadock.io is allowed to use your GitHub account information. After your confirmation you will be redirected back to runadock.io and we will create your runadock.io account. First of all you have to accept our terms and second we will ask you for your credit card information. We need this information to be able to provide you the full service.

Description of web application
------------------------------

#### Containers

The Containers page gives you the possibility to start and stop docker containers, as well as an overview about your running containers.

- Source: Type here the GitHub URL or the Docker Hub image name of your docker project.
- Command: This field is optional and can be used in case of a command is needed to run your docker container.
- Environment: The environment parameter is optional and provides the possibility of a comma separated list of environment variables to set up the environment of your container.
- Name: In case you will run some containers at a time the Name value will give you an easy possibility to differentiate your docker containers.
- Size: Use this option to choose the size for your container. Information about the available sizes can be found at https://github.com/runadock/docs/blob/master/docs/Introduction.md#features
- Plan: Use the Dedicated button to get a dedicated IPv4 address for your container.

Depending on your selection of size and plan you will get immediatly the information about the costs of the container below the buttons Create and Cancel.

If you have started the container it shows up in the list of already running containers. With the information button you can view the details of the container. The Trash button can be used to stop the container.

#### Tokens

You need an authorization key to run docker containers using our runadock.io REST-API. On the Tokens page you can find your authorization key. There you can create additional tokens, and also delete tokens.

#### Billing

The Billing page provides you an overview about your actual balance, your charges and your orders. At Billing page it is also possible to charge for more starts and runs of your docker containers.

#### Settings

At the Settings page you can provide and change your personal information.

CLI
---

We provide you a CLI for using our runadock.io. You can find a CLI for Windows, Mac/OS, and Linux. There are two possibilities to get the CLI:

  - download and unzip the CLI of your need from our mainpage <https://runadock.io>
  - copy the CLI from our GitHub project using the git clone command with the address https://github.com/runadock/runadock-cli

Before starting your containers prepare your environment by setting the following environment variables:

    export RUNADOCK_USER=<your username of runadock.io>

and

    export RUNADOCK_TOKEN=<your authorization key can be found at https://runadock.io/terminal/#/tokens>

#### Start a container

Now you are ready to start a container. Change to the directory, where you have saved the CLI tool and start your container with the following command:

    $ ./runadock run --source <source to the container>

Example:

    $ ./runadock run --source https://github.com/runadock/dockerfiles/tree/master/itworks
    $ created: 7e08492e-5db9-489d-9652-90f133df8bea

The return value is the id of your run created by runadock.io. There are the following optional parameter available for the run command:

    --name      arbitrary name of the container
    --size      size of the container with the possible arguments XS (default), S, M, L

#### Description of a specific container

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
      "source": "https://github.com/runadock/dockerfiles/tree/master/itworks",
      "state": "RUNNING",
      "cpuShares": 128,
      "memory": 512,
      "diskSize": 5,
      "ordered": 1422016066087,
      "created": 1422016068075,
      "terminated": 0,
      "orderedBy": "username",
      "plan": "Starter",
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

As you can see there are two id parameter. The first parameter *id* is the runadock.io-ID of your run. The parameter *containerId* is the ContainerID of your container running by Docker.

#### Terminate a container

For stopping a container you can use the kill command:

    $ ./runadock kill --id <id of the container to kill>

Example:

    $ ./runadock kill --id 9d608bc6-e066-4686-ae98-b3e6ef3114fd
    $

#### List of containers

Last but not least we also provide a command to list all your running and stopped containers. Use

    $ ./runadock ps

and you will get the following output:

    ContainerID  SOURCE		CREATED              STATUS   DNS                       PORTS           NAME
    9f3087c1ec4  nginx    2015-01-23 14:18:52  RUNNING  9f3087c1ec.c.runadock.io  443->49915/tcp

There are the following command options available for the ps command:

    --detail, -d        show long container ids
    --all, -a           show even terminated container's



Java
----

To manage containers using Java you first have to get the sources from our GitHub project https://github.com/runadock/runadock-java. Integrate the runadock-java project into your Java project.

#### Start a container

The following example shows you how to start a container:

		import com.runadock.*;
		public class Example {
			public static void main(final String[] args) {
				Runadock runadock = RunadockFactory.connect(
					"<your username of runadock.io>",
					"<your authorization key can be found at https://runadock.io/terminal/#/tokens>");

        CreateContainerRequest request = new CreateContainerRequest();
        request.setSource("https://github.com/runadock/dockerfiles/tree/master/itworks");
        Container response = runadock.createContainer(request);
        System.out.println("created container: " + response.getId());
      }
    }

Besides the mandatory source parameter there are the following optional parameters provided by the CreateContainerRequest object:

		setCmd(List<String> cmd); - commands which should be executed
		setEnv(List<String> env); - environment variables to be set
		setName(String name); - an arbitrary name of the container
		setSize(String size); - size of the container with the possible arguments XS (default), S, M, L

There is a further createContainer() method where additionally a Callback object as parameter can be provided:

    createContainer(final CreateContainerRequest containerToCreate, Callback callback);

The Callback object provides two methods you can use to get return information about your running container. Here is an implementation example for the Callback object:

    @Test
    public class Example {
      Runadock runadock;
      private State state;
		
			@BeforeTest
			public void setUp() {
				this.runadock = RunadockFactory.connect(
				    "<your username of runadock.io>", 
            "<your authorization key can be found at https://runadock.io/terminal/#/tokens>");
			}
		
			@Test(enabled = false)
			public void createContainer() {
				CreateContainerRequest containerToCreate = new CreateContainerRequest();
				containerToCreate.setSource("https://github.com/runadock/dockerfiles/tree/master/itworks");
				Container response = this.runadock.createContainer(containerToCreate);
				System.out.println("Created Container: " + response);
			}
		
			void setState(final State newState) {
				this.state = newState;
			}
		
			@Test
			public void createContainerWithCallBack() throws InterruptedException {
				CreateContainerRequest containerToCreate = new CreateContainerRequest();
				containerToCreate.setSource("https://github.com/runadock/dockerfiles/tree/master/itworks");
				Callback callback = new Callback() {
		
					@Override
					public void success(final Container container, final State newState) {
						System.out.println("New State detected for container: " + container.getContainerId() + " " + newState);
						setState(newState);
						if (newState == State.RUNNING) {
							RunadockTest.this.runadock.terminateContainer(container.getId());
						}
					}
		
					@Override
					public void failure(final RunadockError error) {
						System.out.println("Error:" + error.getMessage());
					}
				};
				this.runadock.createContainer(containerToCreate, callback);
		
				while (this.state != State.TERMINATED) {
					Thread.sleep(100l);
				}
			}
		
			@Test
			public void describeContainer() {
				try {
					Container container = this.runadock.describeContainer("unknownContainer");
					Assert.fail("The expectation that describe of an unknown container gives 404 failed. ");
				} catch (RetrofitError e) {
					// Expected.
				}
		
			}
		
			@Test(enabled = false)
			public void describeContainers() {
				List<Container> containers = this.runadock.describeContainers(false);
				for (Container container : containers) {
					System.out.println(container.getContainerId() + " from source: " + container.getSource() + " costs: "
							+ container.getCost());
				}
				System.out.println("-----------------ALL Containers--------------");
				List<Container> allContainers = this.runadock.describeContainers(true);
				for (Container container : allContainers) {
					System.out.println(container.getContainerId() + " from source: " + container.getSource() + " costs: "
							+ container.getCost());
				}
			}
		
			@Test
			public void terminateContainer() {
			}
		}


#### Terminate a container

To terminate a container you have to call the following method:

    runadock.terminateContainer("<the containerID of the container to terminate>");

#### List all containers

With the method

    describeContainers(final Boolean all);

you can get a list of all containers. If the boolean is set to true, then all containers, the running containers as well as the terminated containers will be load into the list. The method returns a java.util.List with the Container objects.

The Container object provides get() methods for the properties of a started container. In the following is a list of the available properties:

    Container [
    id=d9e39317-aba8-4799-9abd-12a9be4e7242,
    containerId=2a19bef262216c43f1b7bb7c6a7f0203bc92f375755506d2b7cdbec1ac1bf67f,
    name=null,
    publicDns=2a19bef262.c.runadock.io,
    ip=37.187.250.7,
    source=https://github.com/runadock/dockerfiles/tree/master/itworks,
    state=RUNNING,
    cpuShares=128,
    memory=512,
    diskSize=5,
    ordered=1423221190270,
    created=1423221192259,
    terminated=null,
    orderedBy=username,
    plan=Starter,
    owner=com.runadock.Container$Person@3c22ed04,
    ports=[com.runadock.Container$Port@18f6c074, com.runadock.Container$Port@6fd50c79],
    env=[],
    cmd=[],
    pricePerMinute=EUR 1.15E-4,
    pricePerOrder=EUR 0.05,
    cost=EUR 0.002875,
    buildLog=Step 0 : FROM nginx
      ---> e46b3488b010
      Step 1 : COPY src /usr/share/nginx/html
      ---> Using cache
      ---> 7615793e4928
      Successfully built 7615793e4928
    ]

cURL
----

Last but not least the cURL description. 

		API_USER="<your username of runadock.io>"
		API_TOKEN="<your authorization key can be found at https://runadock.io/terminal/#/tokens>"

#### Start a container

		curl -X POST -H "X-Authorization: ${API_USER}:${API_TOKEN}" -H "Content-Type: application/json" -d '{"source":"https://github.com/runadock/dockerfiles/tree/master/itworks"}' https://runadock.io/api/v1/container

The answer of the POST request contains the complete description of a container, like the example in the following:

		{"id":"3592f681-07e6-4f8d-a8cc-db068cf1fee5",
		"containerId":null,
		"name":"test",
		"publicDns":null,
		"ip":null,
		"source":"https://github.com/runadock/dockerfiles/tree/master/itworks",
		"state":"ORDERED",
		"cpuShares":1024,
		"memory":4096,
		"diskSize":5,
		"ordered":1423238547683,
		"created":null,
		"terminated":null,
		"orderedBy":"username",
		"plan":"Starter",
		"ports":[],
		"env":[],
		"cmd":[],
		"pricePerMinute":{"amount":3.4E-4,"currency":"EUR"},
		"pricePerOrder":{"amount":0.05,"currency":"EUR"},
		"cost":null,
		"buildLog":""}

There are the following optional parameter available for the container start:

    "name":"<arbitrary name of the container>"
    "size":"<size of the container with the possible arguments XS (default), S, M, L>"

#### Description of a specific container

In case you need the information for one specific container, just append the ID of the container to the URL:

		curl -X GET -H "X-Authorization: ${API_USER}:${API_TOKEN}" -H "Content-Type: application/json" https://runadock.io/api/v1/container/<ID of the container>

#### Terminate a container

To delete a container you can use the following cURL command:

		curl -X DELETE -H "X-Authorization: ${API_USER}:${API_TOKEN}" -H "Content-Type: application/json" https://runadock.io/api/v1/container/<ID of the container to be deleted>

#### Description of all containers

To list all containers including the terminated containers use the following cURL command:

		curl -X GET -H "X-Authorization: ${API_USER}:${API_TOKEN}" -H "Content-Type: application/json" https://runadock.io/api/v1/container?all=true

The parameter "all" is set to false per default. Calling the cURL command without the "all"-parameter you will get the running containers only.

