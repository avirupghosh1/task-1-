
# TASK-1
creating a static map using slam(gmapping) and doing navigation using the map(using default navfn gloabalplanner) 



## Deployment

- create a ws and src folder in it in the src folder clone the repo.

```bash
  git clone https://github.com/avirupghoshiitmandi/task-1-.git
```
- after that catkin_make the workspace and source the .bash file and your ros enviroment.
```bash
 cd ..
 catkin_make
 source devel/setup.bash
 ```
 - now launch the bookstore world 
 ```bash 
  roslaunch turtlebot3_gazebo turtlebot3_world.launch
 ```
 - from here you can go choose either to do mapping(manual) and then navigating across or doing the mapping and navigation simultaniously.
**TWO STEP MAPPING AND NAVIGATION**

- ***change the static_map parameter in turtlebot3_navigation/param/global_costmap_params.yaml file to true and remove the rolling_window parameter*
- after launching the world launch the slam gmapping node using slam launch file
```bash
  roslaunch turtlebot3_slam turtlebot3_slam.launch
  ```
- to move around launch the teleop
```bash
  roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
  ```
  - you can now move around your world and you will see the map being generated.
  - if you are satisfied with the map save it using mapserver node make sure you have mapeserver pkg installed in your ros distribution.
  ```bash
   rosrun map_server map_saver -f <map_name>
   ```

   - for help I have already made a static map of the world which is in the turtlebot3_navigation/maps directory
   - now for navigation launch the following launch file(use the map file's location in the map_file arg of turtlebot3_navigation.launch)
   ```bash
    roslaunch turtlebot3_navigation turtlebot3_navigation.launch
   ```
   - this will open a rviz window and after giving an estimated pose of the robot using the rviz pose estimate tool click anywhere in the static map using 2d nav goal to generate a gloabal planner path . The local planner will try to navigate along the path avoiding the obstacles using the local costmap data .
    
**ONE STEP MAPPING AND NAVIGATION**

- ***change the static_map parameter in turtlebot3_navigation/param/global_costmap_params.yaml file to false and add the rolling_window parameter with value true*
- For this approach after launching the gazebo world launch the following

- yt video for this approach is [here](https://www.youtube.com/watch?v=u2xmxfuysww&ab_channel=AvirupGhosh)

 roslaunch turtlebot3_navigation turtlebot3_navigation_gmapping.launch
 ```
 - this will show a rviz window with a smaller and dinamic global costmap inside the globalcostmap click on any point using 2dnavgoal tool the robot will start moving and also keep on building the map .
 - in the end you can also save the map just like the first method.
 - this way of navigation and mapping helps to increase the manual mapping efficiency as you need to just click a far away point and the map will keep on generating.
