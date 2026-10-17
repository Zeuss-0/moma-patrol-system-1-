# MOMA Patrol System

[中文](README.zh-CN.md) | [English](README.MD)

Workspace for Guangzhou Locomotive Patroling system.

This repository, [Zeuss-0/moma-patrol-system-1-](https://github.com/Zeuss-0/moma-patrol-system-1-), is Zeuss-0's working copy of [yangzhaofeng496/moma-patrol-system](https://github.com/yangzhaofeng496/moma-patrol-system). The `-1-` suffix is the existing GitHub fork name. It stays as-is; this repository is not renamed.

Accept only Packages as submodule.

All used and **NEVER modified** 3rd-party packages, such as hardware drivers, should be placed under `3rd/`. Where Zeuss-0 has a public remote, that remote is used. `dobot_v4_bringup` is registered only at `3rd/dobot_v4_bringup`.

It is recommened to be used as `src/` under ROS workspace, i.e:

```bash
git clone --recurse-submodules https://github.com/Zeuss-0/moma-patrol-system-1-.git <your_workspace_dir>/src
```

## Submodule sources

| Path | Source |
| --- | --- |
| `moma_nav` | https://github.com/Johnson3176/moma_nav |
| `teleop_joy_ctrl` | https://github.com/Zeuss-0/teleop_joy_ctrl |
| `hybrid_video_recorder` | https://github.com/Zeuss-0/hybrid_video_recorder |
| `3rd/battery` | https://github.com/Lucid-A/lebang_battery_driver |
| `3rd/livox_ros_driver2` | https://github.com/Lucid-A/livox_ros_driver2 (`Guangtie`) |
| `3rd/dobot_v4_bringup` | https://github.com/Zeuss-0/dobot_v4_bringup |
| `3rd/rs_driver` | https://github.com/RoboSense-LiDAR/rs_driver |
| `3rd/mvs_ros_pkg` | https://github.com/WilsonGuo/mvs_ros_pkg |
| `3rd/modbus_interface` | https://github.com/Zeuss-0/modbus_interface |
| `3rd/wj_716N_lidar` | https://github.com/Zeuss-0/wj_716N_lidar |
| `3rd/realsense-ros` | https://github.com/realsenseai/realsense-ros |
| `3rd/yikun_msgs` | https://github.com/Zeuss-0/yikun_msgs |

Upstream `master` also lists `moma_service`, `patrol`, `ros_http_bridge`, `demonstrate`, `detect`, and `teleop_joy_ctrl` under `yangzhaofeng496`. Those remotes are not publicly readable, so they are not part of this working copy. Joystick teleop comes from the public Zeuss-0 repository. `hybrid_video_recorder` is included because `teleop_joy_ctrl` declares it as an exec dependency. Upstream `.gitmodules` also lists a second `dobot_v4_bringup` path at the repository root; only `3rd/dobot_v4_bringup` is kept.

> [!TIP]
> If already cloned without `--recurse-submodules`, use:
> ```
> git pull
> git submodule update --init --recursive
> ```
> or
> ```
> git pull --recurse-submodules
> ```

## Git Command Usages

The following command is, by default, executed from the root directory of the current local repository.

Take `battery` as example, the repo URL is `https://github.com/Lucid-A/lebang_battery_driver.git`.

> [!IMPORTANT]
> Please follow the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/) when writing commit messages.
> If needed, you can use an LLM to help rewrite your commit message into the required format.

> [!IMPORTANT]
> After commit, use `git push` to push your commit to the remote repository.
> Best pratice is, `pull` before `push`, resolve the conflict in your local workspace.

### ADD Submodule

```bash
git submodule add https://github.com/Lucid-A/lebang_battery_driver.git battery
git add battery .gitmodules
git commit -m "chore(battery): add battery driver submodule"
```
> [!TIP]
>Although the remote repo name is `lebang_battery_driver`, you can give it a new name `battery` in this workspace.

### MOVE Submodule

```bash
git mv battery 3rd/battery
git add 3rd/battery .gitmodules
git commit -m "chore(battery): move battery to 3rd/battery"
```

### UPDATE Submodule to a specificated Version

```bash
git -C 3rd/battery fetch
git -C 3rd/battery checkout <commit-hash>
git add 3rd/battery
git commit -m "chore(battery): update battery to <short-hash>"
```

> [!NOTE]
> No need to `git add .gitmodules` here.

>  [!TIP]
> Use `git submodule update --remote` to update to the newest version of the submodule.

### REMOVE Submodule

```bash
git submodule deinit -f 3rd/battery # Remove registration and files in local ws
git rm -f 3rd/battery               # Remove reference in parent repo
rm -rf .git/modules/3rd/battery     # Remove local cache for deleted submodule
git commit -m "chore: remove <repo> submodule"
```

## README for Packages

+ Provided by Robot Manufacture
  - [Battery Info Publisher](https://github.com/Lucid-A/lebang_battery_driver/blob/6e3a86be3d8b97b30107e738b974ca5d68297a82/readme.md)
+ Sensor Drivers
  - [Livox MID360 Driver](https://github.com/Lucid-A/livox_ros_driver2/blob/Guangtie/README.md)
+ Workspace packages
  - [Joystick teleop](https://github.com/Zeuss-0/teleop_joy_ctrl/blob/main/README.md)
  - [Hybrid video recorder](https://github.com/Zeuss-0/hybrid_video_recorder/blob/main/README.md)
  - [Dobot V4 bringup](https://github.com/Zeuss-0/dobot_v4_bringup) (`3rd/dobot_v4_bringup`)
