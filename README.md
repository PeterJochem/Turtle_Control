1) mkdir -p <name_of_workspace_folder>/src
	cd <nameOfWorkspace>/src
	catkin_make
	A good idea at this point would be to also source devel/setup.bash 



2) Use wstool to clone the crazy turtle repository from Professor Elwins Github
Run wstool init 
We add repos using wstool set <NameOfPackage> —git https://github.com/m~elwin/crazy_turtle
Finally, run wstool update crazy_turtle to retrieve the code from the Github servers 


3) Add our repo by running wstool set turtle_control —git <my_Repo’s_Url>
Run wstool update turtle_control to update the local code from the repo

4) Run catkin_make

5) source devel/setup.bash

6) roslaunch crazy_turtle go_crazy_turtle.launch  

7) Open a new terminal window, source the devel/setup.bash file and then run rosnode list
The running nodes are /mover, /roaming_turtle, /rosout

8) Run rostopics list
The existing topics are /rosout, /rosout_agg, /turtle1/cmd_vel, /turtle1/color_sensor, /turtle1/pose

9) Run rostopic hz /turtle1/cmd_vel  . The average rate is 99.979

10) Run rosservice list. The existing services are /clear, /kill, /mover/get_loggers, /mover/set_loggers_level, /reset, /roaming_turtle/get_loggers, roaming_turtle/set_logger_level, /rosout/get_loggers, /rosout/set_logger_level,  /spawn, /switch, /turtle1/set_pen, /turtle1/teleport_absolute, /turtle1/teleport_relative 

11) rosservice info /switch. It’s type is crazy_turtle/Switch and the node /mover offers it

12) rosparam list 
The parameters are /background_b, /background_g, /background_r, /mover/velocity, /rosdistro, /roslaunch/uris/host_hal__45817, /rosversion, /run_id

13) Run rqt_graph. Make sure in the graph’s window that the selector in the top left corner is set to “Nodes/Topics (all).” Also be sure to uncheck all the hide boxes and filtering services offered by rqt_graph 

14) Run rospack depends1 crazy_turtle. The immediate dependencies are rosy, message_runtime, turtlesim

15) Run rossrv package crazy_turtle. The only type defined is crazy_turtle/Switch 

16) Run rosservice call /switch “[0, 0, 0, 0, 0]“ (or list it in YAML syntax) - the turtle is replaced by a new turtle in a new location. It believe the turtle’s velocity is changed too both linear and angular. It’s orientation, theta, definitely changes. The service returns and x, y pair 
x = mixedUp.x * mixed_up.angular.velocity, y = mixed_up.y * mixed_up.linear.velocity
 
17) I used rosparam get /mover/velocity to find that /mover/velocity = 5

18) Use rosparam set /mover/velocity 10. Nothing happens. If you kill the node with a service call and run rossun, then the turtle will move faster 

19) rosnode kill /mover

20) Run rosrun crazy_turtle mover cmd_vel:=/turtle1/cmd_vel

21) The turtle moves again and faster the before, the change we made a few steps before (changing the param value for velocity) has taken effect 


