# Minecraft Server
Step to configure Minecraft Server on Ubuntu Server OS  

## Java
Make sure Java is installed by typing `java --version`  
If it's not, install it with `sudo apt install openjdk-21-jdk-headless`  

## `server.jar`
Command to download stuff: `wget <link>`  
Download `server.jar` from [this link](https://piston-data.mojang.com/v1/objects/450698d1863ab5180c25d7c804ef0fe6369dd1ba/server.jar)`
> If link doesn't work, see [this tutorial](https://www.minecraft.net/en-us/download/server) 

## Git *(optional)*
If you have your server backed up on Github, make sure [git](Git.md) is installed with `git --version`  
Clone your repository `git clone git@github.com/yungcypo/MinecraftServer.git`  
Make sure you have access (SSH key) by following section *'Generate SSH key'* in [Git tutorial](Git.md)  

## Running server
`nohutp java -Xmx7G -Xms7G -jar server.jar nogui &`  
You can specify the amount of RAM allocated to the server  

## Connecting to the server
### LAN
With `ip add` you can see IP Address of your server  

### WAN
#### Port forwarding
Add Port Forwarding option on your router  
It could look something like this  

| Service Name     | Source Target | Port Range | Local IP      | Local Port | Protocol           |
| ---------------- | ------------- | ---------- | ------------- | ---------- | ------------------ |
| Minecraft Server |               | 25565      | 192.168.1.231 | 25565      | BOTH (TCP and UDP) |
You can also find your Public IP Address on your router settings  

If you can't open a port for some reason, check out [Playit tutorial](Playit.md)

