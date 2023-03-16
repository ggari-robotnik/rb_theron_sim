# rb_theron_sim

=============

Packages for the simulation of the RB-Theron

<h1> Packages </h1>

<h2>rb_theron_gazebo</h2>

Launch files and world files to start the models in gazebo

<h2>rb_theron_sim_bringup</h2>

Launch files that launch the complete simulation of the robot



<h1>Simulating RB-Theron</h1>

### 1) Install the following dependencies:

This simulation has been tested using Gazebo 9 version. To facilitate the installation you can use the vcstool:

```bash
sudo apt-get install -y python3-vcstool
```

### 2) Create a workspace and clone the repository:

```bash
mkdir catkin_ws
cd catkin_ws
vcs import --input \
  https://raw.githubusercontent.com/RobotnikAutomation/rb_theron_sim/melodic-devel/repos/rb_theron_sim.repos
rosdep install --from-paths src --ignore-src -y -r
```

### 3) Compile:

```bash
catkin build
source devel/setup.bash
```


### 4) Launch RB-Theron simulation (1 robot by default, up to 3 robots):
- RB-Theron:

```bash
roslaunch rb_theron_sim_bringup rb_theron_complete.launch
```




## Docker Usage

In order to run this simulation you will need nvidia graphical accelation

### Installation of required files

#### Intel GPU

- [docker engine](https://docs.docker.com/engine/install/ubuntu/)
- [docker compose plugin](https://docs.docker.com/compose/install/linux/)

#### Nvidia GPU

- [docker engine](https://docs.docker.com/engine/install/ubuntu/)

- [docker compose plugin](https://docs.docker.com/compose/install/linux/)

- nvidia-drivers

- [nvidia-docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)

### Usage

```bash
git clone https://github.com/RobotnikAutomation/rb_theron_sim.git
cd rb_theron_sim
git checkout melodic-devel
export ROS_BU_PKG="rb_theron_sim_bringup"
export ROS_BU_LAUNCH="rb_theron_complete.launch"
nvidia-smi &>/dev/null \
&& ln -sf docker-compose-nvidia.yml docker-compose.yml \
|| ln -sf docker-compose-intel.yml docker-compose.yml
cd docker
docker compose up
```