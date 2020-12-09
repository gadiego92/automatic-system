# automatic-system
This project sets up a CentOS 8 environment already provisioned with necessary to start using Flutter. It uses Vagrant and Ansible.

## Setting up Git
In this section we are going to show how to set up Git inside the environment (CentOS 8).

### Customization
Within the project you have two variables to configure Git with your own data. These variables are:

 - git_username
 - git_user_email

You have to set these variables in `/provision/ansible/gourp_vars/all/custom`.

**Note 1:** Don't use Spanish accent marks (this is not a must).

Example:

```
git_username: John Doe
git_user_email: john_doe@gmail.com
```

### Create SSH keys
**Note 2:** The following steps have to be done within the environment (CentOS 8).

Second thing to do is create a SSH pair keys. To do it run the following commands:

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**Note 1:** When the command asks `Enter file in which to save the key (/home/vagrant/.ssh/id_rsa):` just press "Enter".

**Note 2:** When the command asks `Enter passphrase (empty for no passphrase):` leave it empty and press "Enter" twice so no passphrase will be set.

Full example below:

```
[vagrant@localhost ~]$ ssh-keygen -t rsa -b 4096 -C "john_doe@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/vagrant/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/vagrant/.ssh/id_rsa.
Your public key has been saved in /home/vagrant/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:VjL4wS5q1FAM9DqFSpGQ3MMJbn4ZLt1fLWJnO85q9eU john_doe@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|o+=o+o.          |
|o..* +.o         |
| o..+ + = .      |
|o.o.+= o =.      |
| o.=+.ooS= .     |
|  o. ooo=.o  .   |
|    o  ..o. o    |
|   .   .o .. E   |
|      ...o       |
+----[SHA256]-----+
```

### Adding SSH keys to GitHub
Next thing to do is to add the SSH public key to your GitHub account. Let's go to [https://github.com/](https://github.com/) and log in.

Now go to `Settings - SSH and GPG keys` and under `SSH keys` choose `New SSH key`. You will see a new window that asks you for a `Title` and a `Key`.
The `Title` field is just to give a descriptive name to your SSH key and on the `Key` field you have to paste your SSH public key. Finally just press "Add SSH key".

**Note 3:** To copy your SSH public key just run a `cat` command of your SSH public key. In the example above within [Create SSH keys](#create-ssh-keys) is `/home/vagrant/.ssh/id_rsa.pub.`.

Full example:

```
[vagrant@localhost ~]$ cat /home/vagrant/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC9ufBxlQD8BWoG9nsD9TUg41hbF+fR+9y0Iw3HWzq3iK/Heo4HZoUuuskjAPcYQABwvI4rw/4t7dApnI4LDhcIe/5q48IN3OnsiPwS9BvSDQTija+LsIGIQo/og3pCq5F2uwM8G3rrr9CljxGzr3mTRqWKFyGMS5E9+CUvsRrmmRW+B2bHZm6fjdO4CxDngS38I6XaMxvm4IDEf17FgFXf9Q8fLaWUgNpa2xE+fdI21mLN6iemG2OBQXxcvw2vpAPMHzbswmHouXZ/EGUCU+hvAtaLQAa3AB+M9B5JwaHBQv+nUXs9k9HihOW6u5JYM8cSCSMMAKoa2wr1b5jDE6Kj0GN0ALMYYwi4Lb+JZUf83gYhY/kmaUybKqgEXKegdjyLlwAD90C3rMLgn1y1ghpiefNQ33KDsDXj11W9LqJWJvhrKjjQuuL3aFRD6ZVnj8l6BtR/BW9RsVyd1LnMJC5PfzPl8NyvL3K0mQShbzmbPkyt45rSz793sbdPxWLSpiQHyjE98suIvfehd3ucOPdYwxUoFaCpgksuvM6visv1VL7aaucUa/MRPOVrPtAYT1JUprQQGl8RL8q0mE0vMM50RKHckZbCYq9+fVoED4KVLR9Qh/xDTRrfi+CMFVurEZBVNmyhwf8hemNE7E+f71UTleqrY7fAdvP5CZ3elXOXjw== john_doe@gmail.com
```

### Configure GitHub profile
Finally lets see if your profile data is filled and correct.

Go to `Settings - Profile` and check the fields `Name` and `Public email`.

Then go to `Settings - Emails` and verify that the `Primary email address` is set and it's correct.

## Setting up Android Studio

Start Android Studio, and go through the ‘Android Studio Setup Wizard’. This installs the latest Android SDK, Android SDK Command-line Tools, and Android SDK Build-Tools, which are required by Flutter when developing for Android.

1. Import Android Studio Setting - Do not import settings.
2. Data Sharing - Don't send.
3. Android Studio Setup Wizard
   - Welcome: Next.
   - Install Type: Custom
   - Select default JDK Location: JAVA_HOME: /etc/alternatives/java_sdk_1.8.0
   - Select UI Theme: Darcula/Light.
   - SDK Components Setup: Disable Android Virtual Device and Next.
   - Verify Settings: Next.
   - Emulator Settings: Finish.

### Install the Flutter and Dart plugins

To install these:

1. Start Android Studio.
2. Configure > Plugins.
3. Select the Flutter plugin and click "Install".
4. Click "Install" when prompted to install the Dart plugin.
5. Click "Restart IDE" when prompted.

### Install Flutter SDK

1. Start Android Studio.
2. Create New Flutter Project > Flutter Application.
3. On Flutter SDK path select "Install SDK..." and the path `/home/vagrant/Android/flutter`
4. Wait while Flutter repository is downloaded.
5. Click "Restart IDE" when prompted.
