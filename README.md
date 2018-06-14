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
- [ ] 機体のスイッチをONにする
- [ ] 充電器を抜く

- [ ] roslaunch mikata_arm_bringup bringup.launch
- [ ] GATIGATI
rosservice call /enable_all
- [ ] roslaunch inspection mimi_base_setup.launch
- [ ] sh ~/catkin_ws/src/ti_help_me_carry_behavior/scripts/hmc_start.sh
- [ ] roscd e_human_detector/darknet
- [ ] rosrun e_human_detector e_human_detector.py
- [ ] roslaunch realsense r200_nodelet_rgbd.launch
- [ ] realsenseを物理的に抜き差しする
- [ ] 自己位置を合わせる
- [ ] rosrun ti_help_me_carry_behavior HelpMeCarryNode.py




1. リアルセンス
- [ ] リアルセンスが起動できるか
```
$ roslaunch realsense realsense_r200_launch.launch
```
2. 人検知
- [ ] HumanDetectorを起動する
```
$ cd ~/catkin_ws/src/e_human_detector/darknet
$ rosrun e_human_detector e_human_detector.py
```
3. Hark
- [ ] Harkとの接続
```
$ sudo chmod 666 /dev/ttyACM0
```
- [ ] マニピュレーションの有効化
```
$ roslaunch turtlebot_bringup minimal.launch
```
- [ ] hark_localize起動
```
$ cd ~/catkin_ws/src/hark_localize.py
```
- [ ] Harkのデバイス番号を確認
```
$ arecord -l
```
- [ ] harkのデバイス設定、起動
```
$ vim hark_localize.sh
$ ./ros-localize.sh
```
- [ ] SpeechMove起動
```
$ cd ~/catkin_ws/src/speech_move/src
$ python speech_move.py
```
- [ ] Command controler起動
```
$ cd ~/catkin_ws/src/CommandControler/scripts/
$ python CommandControler.py
```
- [ ] ブラウザを開いて、インターネットに繋がっているか確認
- [ ] Speech recognition起動(Google Speech API)
```
$ python ~/catkin_ws/src/speech_recog/scripts/speech_recog_normal.py
```
- [ ] sprのプログラムをrospy.sleep(1)からrospy.sleep(10)に直しているか
- [ ] sprの起動
```
$ python ~/catkin_ws/src/tm_speech_person_recognition/scripts/spr.py
```

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
