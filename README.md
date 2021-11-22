# a_star_turtlebot3_navigation
A* search implementation of global_planner for turtlebot3_navigation package.

## Opening Instructions
This project was done on ROS melodic running on Linux 18.04 LTS on WSL2 for windows.

#### **THE FILES INCLUDED ARE THE `turtlebot3_navigation` folder of the `turtlebot3` package.**

## Installation
* Install suitable ROS distro on Linux, the details to which can be found here: http://wiki.ros.org/ROS/Installation
* After a successful installation of ROS proceed to creating a workspace (preferably catkin)
* Make sure to have git installed on your linux system.
* After setup of the workspace install the turtlebot3 packages
  * Navigate to `<workspace_folder>/src/` and clone this by running `git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git -b melodic-devel` (replace melodic with your distro of ROS)
  * now clone another package `git clone https://github.com/ROBOTIS-GIT/turtlebot3.git -b melodic-devel` (replace melodic with your distro of ROS)
  * now go back to your workspace folder simply by the command `cd ..`
  * run `catkin_make`
  * Upon successful build of the workspace go to the `<workspace_folder>/src/` folder again and run `git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git`
  * go back to the workspace folder and again and build the workspace one final time using the `catkin_make` command.
* After the installation of the turtlebot3 packages certain changes to the `.bashrc` file can be made to load the turtlebot3 robot load by default.
* The default robot  used in the project is the `turtlebot3 burger`
## Running the application
### Part-1 Making the MAP
* The map was made usning the `gmapping` algorithm of the turtlebot3
* Upon successful installation the map can be made by the following commands
  * `roslaunch turtlebot3_gazebo turtlebot3_house.launch` (any other gazebo environment can be used)
  * `roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping` (starting the slam mapping algorithm the details of the various algorithms can be found here https://www.hindawi.com/journals/jat/2020/8867937/)
  * Now to move the robot in the space using teleop run the command `roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`
  * After a satisfactory map is made save the map to be used later in navigation by the following command `rosrun map_server map_saver -f ~/<name_of_the_map>`
### Part-2 Navigating the Environment
* The gazebo world can be launched using the command `roslaunch turtlebot3_gazebo turtlebot3_house.launch`
* The regular NavFn global_planner uses the dijkstra algorithm, the regular navigation launch file is in the turtlebot3_navigation folder and can be run using the command `roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=/home/victorkash/tb3_house_map.yaml`
* However the A* search implementation can be implemented by using separate `move_base.launch` file and different set of parameters as included in this repository.
  * A new set of global parameters files `GlobalPlanner` that has been included in this file allows us to switch from `NavFn` global planner to `GlobalPlanner` `gobal_planner`.
