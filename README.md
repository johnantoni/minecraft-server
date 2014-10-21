minecraft-server
================

minecraft server setup notes

http://msmhq.com/

#### install

    apt-get purge apache*
    apt-get purge samba*
    apt-get update
    apt-get install wget curl tmux default-jdk screen git-core
    wget -q http://git.io/Sxpr9g -O /tmp/msm && bash /tmp/msm
    msm update
    
#### create server

    msm server create myserver
    msm jargroup create msm18 https://s3.amazonaws.com/Minecraft.Download/versions/1.8/minecraft_server.1.8.jar
    msm jargroup getlatest msm18
    msm myserver jar msm18
    cd /opt/msm/servers/myserver/
    cd worldstorage/
    chown -R minecraft:minecraft world/
    msm myserver start
    msm myserver stop
    ...edit eula.txt and set agree=true
    msm myserver start

#### write to disk

    msm myserver save all

or every 1 hour

    0 */2 * * *  msm myserver save all

#### backup

    msm myserver 
