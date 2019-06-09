Docker

入门：
http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html

命令解释：
https://yeasy.gitbooks.io/docker_practice/

```
admins-MacBook-Pro-6:NavHome junwang$ docker run -it -d --mount type=bind,source=/Users/junwang/git/navcore,target=/git/navcore --name android-ndk-r15c -p 22022:22 ec2d-dockerregistry-01.mypna.com:8082/android-ndk-r15c

docker: Error response from daemon: Conflict. The container name "/android-ndk-r15c" is already in use by container "229c2f4994e1b6638db0ae9b3b4329f94037125a021d29c26e4db52e3131af3a". You have to remove (or rename) that container to be able to reuse that name.

admins-MacBook-Pro-6:NavHome junwang$ docker ps  -l
CONTAINER ID        IMAGE                                                    COMMAND                  CREATED             STATUS                        PORTS               NAMES
229c2f4994e1        ec2d-dockerregistry-01.mypna.com:8082/android-ndk-r15c   "/usr/bin/supervisord"   3 days ago          Exited (137) 19 minutes ago                       android-ndk-r15c

admins-MacBook-Pro-6:NavHome junwang$ docker rm 229c2f4994e1
229c2f4994e1

admins-MacBook-Pro-6:NavHome junwang$ docker ps  -l
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

admins-MacBook-Pro-6:NavHome junwang$ docker run -it -d --mount type=bind,source=/Users/junwang/git/navcore,target=/git/navcore --name android-ndk-r15c -p 22022:22 ec2d-dockerregistry-01.mypna.com:8082/android-ndk-r15c
12131edb4994352df465007354041a17239048390ec6a298ff3d5bba93fa0037

admins-MacBook-Pro-6:NavHome junwang$ ssh root@localhost -p 22022
root@localhost's password: 
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.9.125-linuxkit x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

-bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
root@12131edb4994:~# 

root@12131edb4994:~# ls
remoteHudson

root@12131edb4994:~# cd /git         

root@12131edb4994:/git# ls
navcore

root@12131edb4994:/git# cd navcore/

root@12131edb4994:/git/navcore# ls
README.md      datalogmanager	     junctionviewaccess  mviewerqt	smarthorizon	userservice
admfoundation  datamanager	     landmarkdataaccess  navprotocol	tasdk
buildtools     datasense	     mapdataaccess	 platformhacks	terrainaccess
cregexlib      datastreamingmanager  mapdisplay		 qatools	thirdparty
cxx	       eventmanager	     mapenginebatman	 routingcloud	tnopenlr
datacollector  foundation	     mapmatching	 routingcore	trafficonboard

root@12131edb4994:/git/navcore# cd /opt

root@12131edb4994:/opt# ls
Qt		  android-sdk		androideabi-r15c-arm64	 cmake-3.11.4-Linux-x86_64
android-ndk-r15c  androideabi-r15c-arm	androideabi-r15c-x86_64  svnkit-1.7.14

root@12131edb4994:/git/navcore/buildtools/bin# ./tn integrate -t android-ndk-r15c
Scanning... [-]




BLSDK

docker run -it -d --mount type=bind,source=/Users/junwang/git/blsdkwxfwh,target=/git/blsdkwxfwh --name wx -p 22022:22 ec2d-dockerregistry-01.mypna.com:8082/android-ndk-r15c
12131edb4994352df465007354041a17239048390ec6a298ff3d5bba93fa0037
```
