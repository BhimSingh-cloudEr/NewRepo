# This is my first file to create on github using git workspace.
				3-tire Application Server Hosting

# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

# download and install Node.js (you may need to restart the terminal)
nvm install 23

# verifies the right Node.js version is in the environment
node -v # should print `v23.0.0`

# verifies the right npm version is in the environment
npm -v # should print `10.9.0`





nstall MongoDB Community Edition
Follow these steps to install MongoDB Community Edition using the apt package manager.

1
Import the Public Key
From a terminal, install gnupg and curl if they are not already available:

sudo apt-get install gnupg curl

To import the MongoDB public GPG key, run the following command:

curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor

2
Create the List File
Create the list file /etc/apt/sources.list.d/mongodb-org-8.0.list for your version of Ubuntu.


Ubuntu 24.04 (Noble)

Ubuntu 22.04 (Jammy)

Ubuntu 20.04 (Focal)
Create the list file for Ubuntu 24.04 (Noble):

echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list

3
Reload the Package Database
Issue the following command to reload the local package database:

sudo apt-get update

4
Install MongoDB Community Server
You can install either the latest stable version of MongoDB or a specific version of MongoDB.


Latest Release

Specific Release
To install the latest stable version, issue the following

sudo apt-get install -y mongodb-org

For help with troubleshooting errors encountered while installing MongoDB on Ubuntu, see our troubleshooting guide.

Run MongoDB Community Edition
ulimit Considerations
Most Unix-like operating systems limit the system resources that a process may use. These limits may negatively impact MongoDB operation, and should be adjusted. See UNIX ulimit Settings for Self-Managed Deployments for the recommended settings for your platform.

Note
If the ulimit value for number of open files is under 64000, MongoDB generates a startup warning.

Directories
If you installed through the package manager, the data directory /var/lib/mongodb and the log directory /var/log/mongodb are created during the installation.

By default, MongoDB runs using the mongodb user account. If you change the user that runs the MongoDB process, you must also modify the permission to the data and log directories to give this user access to these directories.

Configuration File
The official MongoDB package includes a configuration file (/etc/mongod.conf). These settings (such as the data directory and log directory specifications) take effect upon startup. That is, if you change the configuration file while the MongoDB instance is running, you must restart the instance for the changes to take effect.

Procedure
Follow these steps to run MongoDB Community Edition on your system. These instructions assume that you are using the official mongodb-org package -- not the unofficial mongodb package provided by Ubuntu -- and are using the default settings.

Init System

To run and manage your mongod process, you will be using your operating system's built-in init system. Recent versions of Linux tend to use systemd (which uses the systemctl command), while older versions of Linux tend to use System V init (which uses the service command).

If you are unsure which init system your platform uses, run the following command:

ps --no-headers -o comm 1

Then select the appropriate tab below based on the result:

systemd - select the systemd (systemctl) tab below.

init - select the System V Init (service) tab below.



systemd (systemctl)

System V Init (service)
1
Start MongoDB.
You can start the mongod process by issuing the following command:

sudo systemctl start mongod

If you receive an error similar to the following when starting mongod:

Failed to start mongod.service: Unit mongod.service not found.

Run the following command first:

sudo systemctl daemon-reload

Then run the start command above again.

2
Verify that MongoDB has started successfully.
sudo systemctl status mongod

You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:

sudo systemctl enable mongod

3
Stop MongoDB.
As needed, you can stop the mongod process by issuing the following command:

sudo systemctl stop mongod

4
Restart MongoDB.
You can restart the mongod process by issuing the following command:

sudo systemctl restart mongod

You can follow the state of the process for errors or important messages by watching the output in the /var/log/mongodb/mongod.log file.

5
Begin using MongoDB.
Start a mongosh session on the same host machine as the mongod. You can run mongosh without any command-line options to connect to a mongod that is running on your localhost with default port 27017.

mongosh



