# チェックリスト

USB+イヤホンジャックが刺さっているかを確認
腕がライダーにかぶっていないか
緊急停止スイッチOFF
PC起動後
スピーカーの電源ON(青く光る)	
設定->サウンド->入力装置->内部オーディオを消音にし、MobilePreをONにする
sh mic_check.sh
Realsenseが起動できるか
メルのスイッチをONにする
充電器を抜く

roslaunch mikata_arm_bringup bringup.launch
rosservice call /enable_all
roslaunch inspection mimi_base_setup.launch
sh ~/catkin_ws/src/ti_help_me_carry_behavior/scripts/hmc_start.sh
roscd e_human_detector/darknet
rosrun e_human_detector e_human_detector.py
roslaunch realsense r200_nodelet_rgbd.launch
realsenseを物理的に抜き差しする
自己位置を合わせる
rosrun ti_help_me_carry_behavior HelpMeCarryNode.py

音声認識を確認したいとき
~/catkin_ws/src/speech_recog/scripts$ python speech_recog_normal.py
rostopic echo /voice_recog

<mapping>
roslaunch mikata_arm_bringup bringup.launch
roslaunch inspection mimi_setup.launch
roslaunch turtlebot_navigation gmapping_demo.launch
roslaunch turtlebot_rviz_launchers view_navigation.launch
roslaunch turtlebot_teleop keyboard_teleop.launch
<map_save>
rosrun map_server map_saver -f /home/username/maps/mapname

<help_me_carryを実行する前に行うこと>
・locationの名前とその名前の誤認識データをRecognizer.pyのlocation_listに追加
・locationの名前と座標をNavigation.pyのlocation_listに追加
・hmc_start.shのamcl_demo.launchの
　map_fileの.yamlの名前を生成したmapの名前に変更