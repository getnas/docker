# Docker Container for Syncthing

在容器中运行 Syncthing，省去了手动安装配置的麻烦，非常方便。

容器中默认的存储目录：

    /var/syncthing/config   - 配置文件
    /var/syncthing          - 默认的同步目录

你可依照需求添加和映射额外的目录。

### 用法示例

请将下方命令中的 `/wherever/st-cfg` 和 `/wherever/st-sync` 替换成主机上的真实目录，他们会将容器中的配置文件目录和默认同步目录映射到你所指定的主机路径上，以便于管理 syncthing 配置和同步的文件。

```
$ docker pull getnas/syncthing
$ docker run -d --name syncthing \
    -p 8384:8384 \
    -p 22000:22000 \
    -v /wherever/st-cfg:/var/syncthing/config \
    -v /wherever/st-sync:/var/syncthing \
    getnas/syncthing:latest
```
> 提示：如果希望 syncthing 容器随 docker 自动启动，请添加 `--restart=always` 参数到上述命令中。

如需启用本地设备发现功能，可以使用以下命令创建容器：

```
$ docker pull getnas/syncthing
$ docker run -d --name syncthing \
    --network=host \
    -v /wherever/st-cfg:/var/syncthing/config \
    -v /wherever/st-sync:/var/syncthing \
    getnas/syncthing:latest
```

Be aware that syncthing alone is now in control of what interfaces and ports it
listens on. You can edit the syncthing configuration to change the defaults if
there are conflicts.

## License

The things in this repository are licensed under the MIT license.
Syncthing is distributed under Syncthing's own licensing.
