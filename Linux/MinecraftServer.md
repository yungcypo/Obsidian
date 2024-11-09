# Minecraft Server
Step to configure Minecraft Server on Ubuntu Server OS  

# Prerequisites 
## Java
Make sure Java is installed by typing `java --version`  
If it's not, install it with `sudo apt install openjdk-21-jdk-headless`  

## `server.jar`
Command to download stuff: `wget <link>`  
Download `server.jar` from [this link](https://piston-data.mojang.com/v1/objects/450698d1863ab5180c25d7c804ef0fe6369dd1ba/server.jar)` 
> If link doesn't work, see [this tutorial](https://www.minecraft.net/en-us/download/server) 

# Running server
The problem with running the server is that by default if you close your terminal, the server shuts down  
There are two ways of solving this problem  
## `screen`
### Create a screen session
`screen -S <name>`  for example `screen -S minecraft`  
Now you are in a screen session  
If you run the server inside screen session, it doesn't shut down when you leave  
You can run the server with following command: `java -Xmx7G -Xms7G -jar server.jar`  
### Exiting a screen session
`ctrl+a` and `ctrl+d`  
### Listing screen sessions
`screen -ls`
### Rejoin screen session
`screen -r <name>` for example `screen -r minecraft`
### Delete screen session
`sreen -XS <name> quit` for example `screen -XS minecraft quit`

## `nohup`
You just run this command: `nohup java -Xmx7G -Xms7G -jar server.jar nogui &`  
While this method is easier, you can not go back to the server  

# Connecting to the server
## LAN
With `ip add` command, you can see an IP Address of your server  

## WAN
### Port forwarding
Add Port Forwarding option on your router  
It could look something like this  

| Service Name     | Source Target | Port Range | Local IP      | Local Port | Protocol           |
| ---------------- | ------------- | ---------- | ------------- | ---------- | ------------------ |
| Minecraft Server |               | 25565      | 192.168.1.231 | 25565      | BOTH (TCP and UDP) |
You can find your Public IP Address on your router settings, or via sites like [whatsmyipaddress.com](https://whatismyipaddress.com/)  

### Playit
If you can't open a port for some reason, check out [Playit tutorial](./Playit.md)


# Update server
If you want to update server to newer version, it's as simple as this  
1. Download new `server.jar` file from [official Minecraft website](https://piston-data.mojang.com/v1/objects/45810d238246d90e811d896f87b14695b7fb6839/server.jar)  
2. Stop the server  
3. *(Optional, recommended)* create a backup of the server  
4. Replace old `server.jar` with newly downloaded `server.jar`   
5. Run the server 

After running the server for the first time after update, you will see some extra info  
