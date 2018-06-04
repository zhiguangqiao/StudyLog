## images相关
##### 查看本机上的镜像列表  
```
$ docker images
REPOSITORY                                TAG                 IMAGE ID            CREATED             SIZE
docker.sankuai.com/redis_7379_pass        latest              fdb80a1a76d1        2 hours ago         107MB
docker.sankuai.com:5000/redis_7379_pass   latest              fdb80a1a76d1        2 hours ago         107MB
redis_6379_pass                           latest              3a16fd6ece3f        2 hours ago         107MB
redis_7379_pass                           latest              3a16fd6ece3f        2 hours ago         107MB
docker.sankuai.com/redis_6379_pass        latest              3a16fd6ece3f        2 hours ago         107MB
qiaozhiguang/hyperloop_mysql              2018.5.30           971b130b7a3f        2 days ago          412MB
ubuntu                                    latest              452a96d81c30        5 weeks ago         79.6MB
```
##### 搜索镜像

```
$ docker search ubuntu
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
ubuntu                                                 Ubuntu is a Debian-based Linux operating sys…   7762                [OK]
dorowu/ubuntu-desktop-lxde-vnc                         Ubuntu with openssh-server and NoVNC            186                                     [OK]
rastasheep/ubuntu-sshd                                 Dockerized SSH service, built on top of offi…   151                                     [OK]
ansible/ubuntu14.04-ansible                            Ubuntu 14.04 LTS with ansible                   93                                      [OK]
ubuntu-upstart                                         Upstart is an event-based replacement for th…   86                  [OK]
neurodebian                                            NeuroDebian provides neuroscience research s…   50                  [OK]
```
##### 拉取镜像
```
$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
a48c500ed24e: Pull complete
1e1de00ff7e1: Pull complete
0330ca45a200: Pull complete
471db38bcfbf: Pull complete
0b4aba487617: Pull complete
Digest: sha256:667c4b3820ddfbfe7b2dc9816123c936f45af6f31bd51b01d02e97dc5f09e3d5
Status: Downloaded newer image for ubuntu:latest
```
##### 查看镜像
```
$ docker inspect ubuntu
[
    {
        "Id": "sha256:452a96d81c30a1e426bc250428263ac9ca3f47c9bf086f876d11cb39cf57aeec",
        "RepoTags": [
            "ubuntu:latest"
        ],
        "RepoDigests": [
            "ubuntu@sha256:667c4b3820ddfbfe7b2dc9816123c936f45af6f31bd51b01d02e97dc5f09e3d5"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2018-04-27T23:28:36.319694807Z",
        "Container": "e1a8ac8f61e4bd40dd223471e86b0328609182a3112dd45a435575753bbc7924",
        "ContainerConfig": { ......
```
##### 删除镜像
```
$ docker rmi ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:667c4b3820ddfbfe7b2dc9816123c936f45af6f31bd51b01d02e97dc5f09e3d5
Untagged: ubuntu@sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
Deleted: sha256:452a96d81c30a1e426bc250428263ac9ca3f47c9bf086f876d11cb39cf57aeec
Deleted: sha256:96fccbf869d3c0ee0fb2e976fdf356dc5872f6410030fd094bbc5b34a7559cdb
Deleted: sha256:38ffa1479cb9fd81d0d4d057c282a155a4a83bff5d2b507ee9563f996d74272d
Deleted: sha256:cc6967c5525a55626688a773e4fe578321a2e126a3b1df1bc0763cfd1583c50c
Deleted: sha256:2a2d486f02032f5a6cc56290a244512daa07a8efe0124bccc5701f0a778aa947
Deleted: sha256:65bdd50ee76a485049a2d3c2e92438ac379348e7b576783669dac6f604f6241b
```

### docker run
### docker kill
### docker rm
### docker rmi
