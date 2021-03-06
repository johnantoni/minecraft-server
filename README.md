minecraft-server
================

minecraft server setup notes

http://msmhq.com/

### maintenance

#### install

(currently ubuntu 14.04 LTS 64bit edition)

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

#### write worlds to disk

    msm myserver worlds todisk

or every 1 hour

    0 */1 * * *  msm myserver worlds todisk

#### backup

    msm myserver worlds backup

backups stored in /opt/msm/archives/worlds/[servername]/world

backup every day at 6:30am

    30 6 * * *  msm myserver worlds backup

### layout

    /opt/msm/servers/[servername]
    .../world (symlinked to /opt/msm/servers/[servername]/worldstorage/world
    .../eula.txt (must edit and set to agree=true to start minecraft 1.8)
