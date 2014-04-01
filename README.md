ctlc-docker-dropbox
===================

A secure isolated Dropbox Docker Container. Why? Because do you really know what dropboxd really does?

	# on boot2docker via boot2docker ssh -o password_stdin
	$ sudo mkdir /mnt/sda1/share
	$ sudo chown -R docker:docker /mnt/sda1/share
		
	# on Mac
	$ mkdir ~/SafeDropbox
	$ brew install sshfs
	$ echo tcuser | sshfs docker@localhost:/mnt/sda1/share ~/SafeDropbox -oping_diskarb,volname=SafeDropbox -p 2022 -o reconnect -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o password_stdin

	# in a new terminal window on your Mac run this and go to the URL it tells you
	$ docker run -i -t -v /mnt/sda1/share:/Dropbox ctlc/dropbox /.dropbox-dist/dropboxd
	This computer isn't linked to any Dropbox account...
	Please visit https://www.dropbox.com/cli_link?host_id=694cee0dcfe6220644ed503120838b49 to link this device.
	This computer is now linked to Dropbox. Welcome Lucas

	# without killing the new terminal window, in the old Mac terminal window, type this
	$ docker commit `docker ps -l -q` my-dropbox
	$ docker kill `docker ps -l -q`
	$ docker run -d -v /mnt/sda1/share:/Dropbox my-dropbox /.dropbox-dist/dropboxd

Now you can go and delete your Dropbox app from your mac and not worry about Dropbox being able to ever do anything outside of its little Linux Container.