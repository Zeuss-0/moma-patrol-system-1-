# MOMA Patrol System

Workspace for Guangzhou Locomotive Patroling system.

Accept only Packages as submodule.

It is recommened to be used as `src/` under ROS workspace, i.e:
```git clone --recurse-submodules git@github.com:yangzhaofeng496/moma-patrol-system.git <your_workspace_dir>/src```

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

All used and modified 3rd-party packages, such as hardware drivers, should be placed under `3rd/`



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

<details>
<summary><b>Battery Info Publisher</b></summary>

![Battery Info Publisher](3rd/battery/readme.md)

</details>