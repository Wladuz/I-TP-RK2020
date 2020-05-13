# Inteligentné plánovanie pohybu robota

Cieľom tohoto tímového projektu bol návrh a zabezpečenie bezkolízneho navigovania mobilného robota v uzatvorenom lokálnom prostredí, pomocou robotického operačného systému (ROS). 

## Prerequisites

Pracujeme s niekoľkými existujúcimi balíkmi, ktoré je potrebné mať nainštalované. Týmto získame zoznam chýbajúcich, ak nejaké sú:

```
rosdep install -si --reinstall --from-path ~/catkin_ws/src
```

## Návod na spustenie

Skopírujeme si ```/src``` adresár do nášho workspace
```
cp -r src/* ~/catkin_ws/src/
```

potom musíme skompilovať náš workspace
```
roscd; cd ..; catkin_make
```

Následne už môžme spúšťať samotné balíky nášho projektu:

Spawnem svet (nezabudni si nahrat bludisko)

```
roslaunch gazebo_ros empty_world.launch 
```

Spawnem robota
```
roslaunch m2wr_description spawn.launch
```

Mapovací balíček
```
roslaunch gmapping slam_gmapping_pr2.launch
```

Ovládanie robota
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

Príkaz na uloženie mapy
```
rosrun map_server map_saver -f test.yaml
```

Príkaz na nahratie mapy
```
rosrun map_server map_server test.yaml.yaml
```

Príkaz na spustenie lokalizácie
```
roslaunch amcl amcl_diff.launch #alebo toto > rosrun amcl amcl scan:=m2wr/laser/scan
```

Príkaz na spustenie navigácie
```
roslaunch move_base move_base.launch
```

Následne si už len pomocou klávesnice prebehneme robotom po mape aby sa zlokalizoval a na vrchnej lište v Rviz si zvolíme pomocou tlačidla 2DNavGoal cieľovú pozíciu robota.



### Návod na spustenie **tp_gui**

Príkaz na spustenie aplikácie (predpokladáme, že beží gazebo simulácia)
```
rosrun tp_gui tp_gui
```
Príkazy na spustenie testu bateriek
```
chmod +x ~/catkin_ws/src/tp_gui/src/test_battery.bash
cd ~/catkin_ws/src/tp_gui/src
./test_battery.bash
```

Následne môžme ovládať robota pomocou tlačidiel a vidieť výstupy riadenia a hodnoty z bateriek.

