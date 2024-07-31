# Playit
Setup of [playit.gg](https://playit.gg/download/linux) which I mainly use for [Minecraft server](./MinecraftServer.md)  

```shell
curl -SsL https://playit-cloud.github.io/ppa/key.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/playit.gpg >/dev/null
```

```shell
echo "deb [signed-by=/etc/apt/trusted.gpg.d/playit.gpg] https://playit-cloud.github.io/ppa/data ./" | sudo tee /etc/apt/sources.list.d/playit-cloud.list
```

```shell
sudo apt update
```

```shell
sudo apt install playit
```

```shell
playit
```

After doing these steps successfully, you will be asked to open you browser with link specified in console and follow steps there   