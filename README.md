# Help Me Carry 2018 in Canada
## Overview
ロボカップ@homeのSPRタスクのためのpythonスクリプト。  
音声認識や人認識のプログラムなどと通信を行う。  
## Writter
1. Itou
2. Enomoto
--------------------------------------
# チェックリスト:triangular_flag_on_post:
- [ ] USE+イヤホンジャックが刺さっているかを確認
- [ ] 緊急停止スイッチOFF
- [ ] PC起動後にスピーカーの電源ON、スピーカーのLEDが**青く光っているか**を確認
- [ ] スピーカーはしっかりと接触しているか
- [ ] 設定->サウンド->入力装置->内部オーディオを消音にし、MobilePreをONにする
- [ ] MobilePreマイクに触れて、動作していることを確認する
- [ ] 音声の出力をunavailableにする
- [ ] `sh mic_check.sh`(一度エラーが起こる)
- [ ] ブラウザを開いて、インターネットに繋がっているか確認
- [ ] 機体のスイッチをONにする
- [ ] 充電器を抜く

- [ ] roslaunch mikata_arm_bringup bringup.launch
- [ ] rosservice call /enable_all
- [ ] アームがガチガチになっているか
- [ ] roslaunch inspection mimi_base_setup.launch
- [ ] 音が鳴ったか
- [ ] sh ~/catkin_ws/src/ti_help_me_carry_behavior/scripts/hmc_start.sh
- [ ] 自己位置を合わせて少し移動させる
- [ ] roscd e_human_detector/darknet
- [ ] rosrun e_human_detector e_human_detector.py
- [ ] roslaunch realsense r200_nodelet_rgbd.launch
- [ ] 物理的な抜き差しなしでRealSenceが光っているか
- [ ] 自己位置を合わせる
- [ ] rosrun ti_help_me_carry_behavior HelpMeCarryNode.py

--------------------------------

## 音声認識を確認したいとき
~/catkin_ws/src/speech_recog/scripts$ python speech_recog_normal.py
rostopic echo /voice_recog

## mapping
```
roslaunch mikata_arm_bringup bringup.launch
roslaunch inspection mimi_setup.launch
roslaunch turtlebot_navigation gmapping_demo.launch
roslaunch turtlebot_rviz_launchers view_navigation.launch
roslaunch turtlebot_teleop keyboard_teleop.launch
<map_save>
rosrun map_server map_saver -f /home/username/maps/mapname
```

## help_me_carryを実行する前に行うこと
・locationの名前とその名前の誤認識データをRecognizer.pyのlocation_listに追加
・locationの名前と座標をNavigation.pyのlocation_listに追加
・hmc_start.shのamcl_demo.launchの
　map_fileの.yamlの名前を生成したmapの名前に変更
