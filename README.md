# MOMA Patrol System

[中文](README.zh-CN.md) | [English](README.MD)

Workspace for the Guangzhou Locomotive Patrol System.

This repository manages each functional package as a Git submodule.

All third-party packages that are used but **not modified**, such as hardware drivers, should be placed in the `3rd/` directory.

It is recommended to place this repository in the `src/` directory of a ROS workspace:

```bash
git clone --recurse-submodules https://github.com/yangzhaofeng496/moma-patrol-system.git
cd moma-patrol-system
rosdep update
rosdep install
catkin_make -j$(nproc) -l$(nproc) -DROS_EDITION=ROS1
```

> [!TIP]
> If the repository was cloned without `--recurse-submodules`, run:
> ```
> git pull
> git submodule update --init --recursive
> ```
> Or:
> ```
> git pull --recurse-submodules
> ```

## Git Commands

The following commands assume that they are run from the root directory of the current local repository.

Using `battery` as an example, its repository URL is:
`https://github.com/Lucid-A/lebang_battery_driver.git`.

> [!IMPORTANT]
> Follow the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/) when writing commit messages.
> If necessary, you can use an LLM to rewrite commit messages in the required format.

> [!IMPORTANT]
> After committing, use `git push` to push the commit to the remote repository.
> It is recommended to run `pull` before pushing and promptly resolve any conflicts that may occur.

### Add a Submodule

```bash
git submodule add https://github.com/Lucid-A/lebang_battery_driver.git battery
git add battery .gitmodules
git commit -m "chore(battery): add battery driver submodule"
```
> [!TIP]
> Although the remote repository is named `lebang_battery_driver`, it can be named `battery` in this workspace.

### Move a Submodule

```bash
git mv battery 3rd/battery
git add 3rd/battery .gitmodules
git commit -m "chore(battery): move battery to 3rd/battery"
```

### Update a Submodule to a Specific Version

```bash
git -C 3rd/battery fetch
git -C 3rd/battery checkout <commit-hash>
git add 3rd/battery
git commit -m "chore(battery): update battery to <short-hash>"
```

> [!NOTE]
> There is no need to run `git add .gitmodules` again at this point.

>  [!TIP]
> You can use `git submodule update --remote` to update to the latest version of the remote repository.

### Remove a Submodule

```bash
git submodule deinit -f 3rd/battery # Remove the registration and files from the local workspace
git rm -f 3rd/battery               # Remove the submodule reference from the parent repository
rm -rf .git/modules/3rd/battery     # Remove the local cache of the deleted submodule
git commit -m "chore: remove <repo> submodule"
```

## READMEs for Functional Packages

### Provided by the Robot Manufacturer

- [Battery information publisher node](https://github.com/Lucid-A/lebang_battery_driver/blob/6e3a86be3d8b97b30107e738b974ca5d68297a82/readme.md)

### Sensor Drivers

- [Livox MID360 driver](https://github.com/Lucid-A/livox_ros_driver2/blob/Guangtie/README.md)
