collectorbot_gazebo
===================

https://github.com/SquadCollaborativeRobotics/collectorbot_gazebo

Contains world, launch, and other files for launching collectorbot simulation with gazebo

To run the simulation, make sure to have this repo and collectorbot_description under your catkin workspace. You'll also need to copy the hokuyo folder from inside the collectorbot_description folder to the ~/.gazebo/models folder, as I modified it to use the ROS plugin as opposed to the default gazebo plugin.  I would recommend using a symlink between the folders (I did this graphically using nautilus, right click the hokuyo folder, make link, and then cut and paste it into the .gazebo/models directory and rename to hokuyo).

After all the code is where it needs to be (this and collectorbot_description under catkin, hokuyo in the gazebo model database), run:

`roslaunch collectorbot_gazebo collectorbot.launch`

This will start gazebo with whatever the world file in collectorbot_gazebo/worlds/collectorbot.world is.

Next, in a new terminal, you'll need to spawn the robot using a rosrun command:

```
rosrun gazebo_ros spawn_model -file `rospack find collectorbot_description`/urdf/collectorbot.sdf -sdf -x 0 -y 0 -z .5 -model collectorbot
```

You can see http://gazebosim.org/wiki/Tutorials/1.9/Using_roslaunch_Files_to_Spawn_Models for more info on spawning models and such.

After that, you should be good to go with the model in the world.  As of 1/3/2014, the model can listen to the /cmd_vel topic and move accordingly, so by publishing to it you can move the robot in gazebo. It also spits out hokuyo laser data to the /scan topic. I have also implemented a static transform in the launch file so that the laser data appears in the correct frame. So all should be ready for testing mapping/navigating code, though I haven't done any of it yet.


Fun w/ gazebo: Use the remote_control_node in scr_proto to control the bot using arrow keys