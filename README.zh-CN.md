# MOMA Patrol System

[中文](README.zh-CN.md) | [English](README.MD)

广州机车巡检系统工作空间。

本仓库 [Zeuss-0/moma-patrol-system-1-](https://github.com/Zeuss-0/moma-patrol-system-1-) 是 Zeuss-0 对 [yangzhaofeng496/moma-patrol-system](https://github.com/yangzhaofeng496/moma-patrol-system) 的工作副本。名称里的 `-1-` 是 GitHub 创建 fork 时留下的后缀，此处保持不变，不重命名仓库。

本仓库只将各功能包作为 Git submodule 纳入管理。

所有使用但**不会修改**的第三方软件包（例如硬件驱动）应放置在 `3rd/` 目录下。若 Zeuss-0 已有公开远程仓库，则使用该远程。`dobot_v4_bringup` 只登记在 `3rd/dobot_v4_bringup`。

建议将本仓库放置在 ROS 工作空间的 `src/` 目录中：

```bash
git clone --recurse-submodules https://github.com/Zeuss-0/moma-patrol-system-1-.git <your_workspace_dir>/src
```

## Submodule 来源

| 路径 | 来源 |
| --- | --- |
| `moma_nav` | https://github.com/Johnson3176/moma_nav |
| `teleop_joy_ctrl` | https://github.com/Zeuss-0/teleop_joy_ctrl |
| `hybrid_video_recorder` | https://github.com/Zeuss-0/hybrid_video_recorder |
| `3rd/battery` | https://github.com/Lucid-A/lebang_battery_driver |
| `3rd/livox_ros_driver2` | https://github.com/Lucid-A/livox_ros_driver2（分支 `Guangtie`） |
| `3rd/dobot_v4_bringup` | https://github.com/Zeuss-0/dobot_v4_bringup |
| `3rd/rs_driver` | https://github.com/RoboSense-LiDAR/rs_driver |
| `3rd/mvs_ros_pkg` | https://github.com/WilsonGuo/mvs_ros_pkg |
| `3rd/modbus_interface` | https://github.com/Zeuss-0/modbus_interface |
| `3rd/wj_716N_lidar` | https://github.com/Zeuss-0/wj_716N_lidar |
| `3rd/realsense-ros` | https://github.com/realsenseai/realsense-ros |
| `3rd/yikun_msgs` | https://github.com/Zeuss-0/yikun_msgs |

上游 `master` 还登记了 `yangzhaofeng496` 下的 `moma_service`、`patrol`、`ros_http_bridge`、`demonstrate`、`detect` 和 `teleop_joy_ctrl`。这些远程仓库无法公开读取，因此不纳入本工作副本。手柄遥操作使用 Zeuss-0 的公开仓库。由于 `teleop_joy_ctrl` 将 `hybrid_video_recorder` 声明为 exec 依赖，本仓库一并加入该功能包。上游 `.gitmodules` 还在仓库根目录登记了第二份 `dobot_v4_bringup`，这里只保留 `3rd/dobot_v4_bringup`。

> [!TIP]
> 如果克隆时没有使用 `--recurse-submodules`，可以执行：
>
> ```bash
> git pull
> git submodule update --init --recursive
> ```
>
> 或者：
>
> ```bash
> git pull --recurse-submodules
> ```

## Git 命令说明

以下命令默认在当前本地仓库的根目录执行。

以 `battery` 为例，其仓库地址为：
`https://github.com/Lucid-A/lebang_battery_driver.git`。

> [!IMPORTANT]
> 编写提交信息时，请遵循
> [Conventional Commits 规范](https://www.conventionalcommits.org/en/v1.0.0/)。
> 如有需要，可以使用 LLM 帮助将提交信息修改为规范格式。

> [!IMPORTANT]
> 提交后请使用 `git push` 将提交推送到远程仓库。
> 建议在推送前先执行 `pull`，并及时解决可能出现的冲突。

### 添加 Submodule

```bash
git submodule add https://github.com/Lucid-A/lebang_battery_driver.git battery
git add battery .gitmodules
git commit -m "chore(battery): add battery driver submodule"
```

> [!TIP]
> 虽然远程仓库名称是 `lebang_battery_driver`，但可以在本工作空间中将它命名为 `battery`。

### 移动 Submodule

```bash
git mv battery 3rd/battery
git add 3rd/battery .gitmodules
git commit -m "chore(battery): move battery to 3rd/battery"
```

### 更新 Submodule 到指定版本

```bash
git -C 3rd/battery fetch
git -C 3rd/battery checkout <commit-hash>
git add 3rd/battery
git commit -m "chore(battery): update battery to <short-hash>"
```

> [!NOTE]
> 此时不需要再次执行 `git add .gitmodules`。

> [!TIP]
> 可以使用 `git submodule update --remote` 更新到远程仓库的最新版本。

### 删除 Submodule

```bash
git submodule deinit -f 3rd/battery # 删除本地工作空间中的注册信息和文件
git rm -f 3rd/battery               # 删除父仓库中的 submodule 引用
rm -rf .git/modules/3rd/battery     # 删除已删除 submodule 的本地缓存
git commit -m "chore: remove <repo> submodule"
```

## 各功能包的 README

### 机器人厂商提供

- [电池信息发布节点](https://github.com/Lucid-A/lebang_battery_driver/blob/6e3a86be3d8b97b30107e738b974ca5d68297a82/readme.md)

### 传感器驱动

- [Livox MID360 驱动](https://github.com/Lucid-A/livox_ros_driver2/blob/Guangtie/README.md)

### 工作空间功能包

- [手柄遥操作](https://github.com/Zeuss-0/teleop_joy_ctrl/blob/main/README_ZH.md)
- [混合录像](https://github.com/Zeuss-0/hybrid_video_recorder/blob/main/README_ZH.md)
- [越疆 Dobot V4 驱动](https://github.com/Zeuss-0/dobot_v4_bringup)（`3rd/dobot_v4_bringup`）
