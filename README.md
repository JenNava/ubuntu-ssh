# ubuntu-ssh
just for fun, this is a test proj

Simple Ubuntu docker images with SSH access

Running JenNava/ubuntu-ssh
--------------------

To run a container from the image you created earlier with the `trusty` tag
binding it to port 99 in all interfaces, execute:

	docker run -d -p 99:22 jennava/ubuntu-ssh:trusty

The first time that you run your container, a random password will be generated
for user `root`. To get the password, check the logs of the container by running:

	docker logs <CONTAINER_ID>

You will see an output like the following:

	========================================================================
	You can now connect to this Ubuntu container via SSH using:

	    ssh -p <port> root@<host>
	and enter the root password 'F45uIVUM789y' when prompted

	Please remember to change the above password as soon as possible!
	========================================================================

In this case, `F45uIVUM789y` is the password allocated to the `root` user.

Done!


Setting a specific password for the root account
------------------------------------------------

If you want to use a preset password instead of a random generated one, you can
set the environment variable `ROOT_PASS` to your specific password when running the container:

	docker run -d -p 99:22 -e ROOT_PASS="mypass" jennava/ubuntu-ssh:trusty


Adding SSH authorized keys
--------------------------

If you want to use your SSH key to login, you can use `AUTHORIZED_KEYS` environment variable. You can add more than one public key separating them by `,`:

    docker run -d -p 99:22 -e AUTHORIZED_KEYS="`cat ~/.ssh/id_rsa.pub`" jennava/ubuntu-ssh:trusty
