# MAD-ICP

## Intended use 

This small toolset allows to integrate SLAM solution provided by [MAD-ICP](https://github.com/rvp-group/mad-icp) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains workspace that :
  - submodule to tested revision of MAD-ICP

## Dependencies

```shell
pip install --upgrade pip setuptools wheel
```

## Building
```shell
pip install mad-icp
```

## Example:

Download the dataset from [NTU-VIRAL](https://ntu-aris.github.io/ntu_viral_dataset/)
For this example, download eee_03.

## Convert(If it's a ROS1 .bag file):

```shell
rosbags-convert --src {your_downloaded_bag} --dst {desired_destination_for_the_converted_bag}
```

## MAD-ICP LAUNCH
Changes:

Create new config file:

```shell
code  ~/.local/lib/python3.10/python3.10/site-packages/mad_icp/configurations/datasets/
```

Create a new file named
```shell
ntu-viral.cfg
```

Add the following content:
```shell
min_range : 1.3
max_range : 120
sensor_hz : 20
deskew : True
rosbag_topic : "/os1_cloud_node1/points"
lidar_to_base: 
  - [1, 0, 0, 0]
  - [0, 1, 0, 0]
  - [0, 0, 1, 0]
  - [0, 0, 0, 1]
```

Run MAD-ICP
```shell
~/.local/bin/mad_icp --data-path {path_for_rosbag2} --estimate-path {path_for_output} --dataset-config ~/.local/lib/python3.10/site-packages/mad_icp/configurations/datasets/ntu-viral.cfg
```