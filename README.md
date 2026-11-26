# unitree_ros release

Bloom packaging for [unitree_ros](https://github.com/unitreerobotics/unitree_ros), targeting ROS 2 Jazzy.
ROS package files are added from `master:overlay`; upstream sources are unchanged.
Only `g1_description` is released.

Update `version` and `release_tag` in `tracks.yaml` for each upstream update,
then generate release branches locally:

```bash
git-bloom-release jazzy
```

Bloom reapplies the overlay and exported patches on each release. Resolve any
patch conflicts and test the result. Each ROS distribution needs its own track.
This repository is not yet registered in rosdistro.
