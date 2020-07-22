# voslambot

## Steps to install Google voice assistant
### Step 1: Create project in Google console
Log into your Raspbian with PI Desktop.

Open up a Web Browser and go to "console.cloud.google.com/project"

Log into your Google Account.

Click on "CREATE PROJECT"

Give it any name you like and click "Create"

Wait for your project to show and then click the three dots on the project's name.

Click on the three little lines at the top left of the page, then select "API Manager"

Click on the dropdown menu.

Hit all, then select your project.

Type "Google assistant" on the search bar, this will make the searching process a lot quicker and easier.

Click on the "Google Assistant API" and then click "Enable"

### Step 2: Setup OAuth Key
Go to the bar on the left and select "Credentials" and then click on the "OAuth Consent Screen"

Hit on "Create Credentials", then select "OAuth client ID"

In the next screen, choose "Other" and give it any name that you want.

Hit "Ok" and then move your mouse over to an arrow pointing down at the right of the screen, click on it to download your Credentials file.

### Step 3: Enable Permissions for device
Head over to "myaccount.google/activitycontrols"

Scroll down and activate the following controls:

Web & App Activity
Location History
Device Information
Voice & Audio Activity

### Step 5: Download and Install Dependencies
Open up the Command Prompt.

Update your System.

Once it finishes, type in "sudo apt-get install python3-dev python3-venv" press "Enter" and wait for it to finish.

When the download finishes, type in "python3 -m venv env"

Once you enabled that, type "env/bin/python -m pip install –upgrade pip setuptools –upgrade" and press "Enter"

Type "source env/bin/activate" to get into the enviroment.

## Steps to install ROS on Raspberry Pi
### Step 1: Installing Bootstrap Dependencies and Download the Packages
Let's start by setting up the repositories and installing the necessary dependencies

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo apt-get update
sudo apt-get install -y python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential  cmake
Then initialize rosdep and update it

sudo rosdep init
rosdep update
When that's done let's create a dedicated catkin workspace for building ROS and move to that directory.

mkdir ~/ros_catkin_ws
cd ~/ros_catkin_ws

installing Desktop Install here.

rosinstall_generator desktop --rosdistro melodic --deps --wet-only --tar > melodic-desktop-wet.rosinstall 

wstool init -j8 src melodic-desktop-wet.rosinstall
### Step 2: Build and Source the Installation
Next we use the rosdep tool for installing all the rest of the dependencies:

rosdep install --from-paths src --ignore-src --rosdistro melodic -y
Once it has completed downloading the packages and resolving the dependencies you are ready to build the catkin packages. (Run this command from ros_catkin_ws folder)

sudo ./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/melodic -j2
If the compilation process freezes(very likely, if you install the desktop version), you need to increase swap space available. By default it's 100 MB, try increasing it to 2048 MB.

Now ROS Melodic should be installed on your Raspberry Pi 4. We'll source the new installation with following command:

echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc

##Steps to install ROS Melodic on Ubuntu 18.04
### Step 1: Configure your Ubuntu repositories
Setup your sources.list
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

Set up your keys
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

### Step 2: Installation
First, make sure your Debian package index is up-to-date:
sudo apt update

Desktop-Full Install : ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators and 2D/3D perception
sudo apt install ros-melodic-desktop-full

### Step 3: Environment setup
It's convenient if the ROS environment variables are automatically added to your bash session every time a new shell is launched:

echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
source /opt/ros/melodic/setup.bash

### Step 4: Dependencies for building packages
To install this tool and other dependencies for building ROS packages, run:

sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential

Initialize rosdep
sudo apt install python-rosdep

With the following, you can initialize rosdep.
sudo rosdep init
rosdep update

