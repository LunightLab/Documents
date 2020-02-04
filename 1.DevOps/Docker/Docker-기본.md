<div align=right>
	<a href="https://github.com/LunightLab">
		<img alt="author" src= "https://img.shields.io/badge/author-lunight-blue?style=glat-square" target="_blank"></a>
	</a>
	<a href="https://github.com/LunightLab/LuLabTemplate">
		<img alt="template version" src= "https://img.shields.io/badge/template%20version-1.0-blue?style=glat-square" target="_blank"></a>
	</a>
</div>

# Title

## Contents
* [테스트 환경](#테스트-환경)
* [Docker setting](#Docker-setting)
* [CentOS 다운로드](#CentOS-다운로드)
* [CentOS docker container](#CentOS-docker-container)
* [Ubuntu docker container](#Ubuntu-docker-container)
* [nginx docker container](#nginx-docker-container)
* [gitlab docker container](#gitlab-docker-container)
* [주제6](#주제7)
* [#HashTag](##HashTag)
* [About LuLabTemplate](#About-LuLabTemplate)
* [Document History](#Document-History)
* [License](#License)
* [Author](#Author)

## 테스트 환경
- macOS Catalina(version 10.15.2)

## Docker setting
### brew install
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### docker client install
```
$ brew install docker
```

### docker hub install 
- link : [docker hub download url](https://docs.docker.com/docker-for-mac/install/)

### install result
```
$ docker version
Client: Docker Engine - Community
 Version:           19.03.4
 API version:       1.40
 Go version:        go1.12.10
 Git commit:        9013bf5
 Built:             Thu Oct 17 23:44:48 2019
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.4
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.10
  Git commit:       9013bf5
  Built:            Thu Oct 17 23:50:38 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
$ ~
```

### docker hub setting
- url : [docker hub](https://hub.docker.com/)

```
#docker hub에 로그인(or docker Desktop에서 로그인할 수 있음.)
$ docker login
Username: [Docker hub ID]
Password: [Password]
Email: [email]
Login Succeeded
```

## CentOS docker container
### 기본설치방법
```
#docker search
➜  docker search centos
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
centos                             The official build of CentOS.                   5798                [OK]
ansible/centos7-ansible            Ansible on Centos7                              127                                     [OK]
jdeathe/centos-ssh                 OpenSSH / Supervisor / EPEL/IUS/SCL Repos - …   114                                     [OK]
consol/centos-xfce-vnc             Centos container with "headless" VNC session…   109                                     [OK]
centos/mysql-57-centos7            MySQL 5.7 SQL database server                   67
imagine10255/centos6-lnmp-php56    centos6-lnmp-php56                              58                                      [OK]
tutum/centos                       Simple CentOS docker image with SSH access      44
centos/postgresql-96-centos7       PostgreSQL is an advanced Object-Relational …   40
kinogmt/centos-ssh                 CentOS with SSH                                 29                                      [OK]
pivotaldata/centos-gpdb-dev        CentOS image for GPDB development. Tag names…   10
guyton/centos6                     From official centos6 container with full up…   9                                       [OK]
nathonfowlie/centos-jre            Latest CentOS image with the JRE pre-install…   8                                       [OK]
drecom/centos-ruby                 centos ruby                                     6                                       [OK]
mamohr/centos-java                 Oracle Java 8 Docker image based on Centos 7    3                                       [OK]
darksheer/centos                   Base Centos Image -- Updated hourly             3                                       [OK]
pivotaldata/centos                 Base centos, freshened up a little with a Do…   3
pivotaldata/centos-gcc-toolchain   CentOS with a toolchain, but unaffiliated wi…   2
pivotaldata/centos-mingw           Using the mingw toolchain to cross-compile t…   2
miko2u/centos6                     CentOS6 日本語環境                                   2                                       [OK]
blacklabelops/centos               CentOS Base Image! Built and Updates Daily!     1                                       [OK]
mcnaughton/centos-base             centos base image                               1                                       [OK]
indigo/centos-maven                Vanilla CentOS 7 with Oracle Java Developmen…   1                                       [OK]
pivotaldata/centos7-dev            CentosOS 7 image for GPDB development           0
smartentry/centos                  centos with smartentry                          0                                       [OK]
pivotaldata/centos6.8-dev          CentosOS 6.8 image for GPDB development         0

#docker 이미지 다운로드 
➜  docker pull centos
Using default tag: latest
latest: Pulling from library/centos
8a29a15cefae: Pull complete
Digest: sha256:fe8d824220415eed5477b63addf40fb06c3b049404242b31982106ac204f6700
Status: Downloaded newer image for centos:latest
docker.io/library/cento

#docker container 목록
➜  docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
centos              latest              470671670cac        2 weeks ago         237MB

#docker centos 실행
# -t 옵션 : sudo-TTY를 할당
# -d 옵션 : 컨테이너를 백그라운드에서 실행
# -name 옵션 : 컨테이너 이름
➜  docker run -td --name centos8 \
centos:latest
166861a3e8cc022720650595ae089d207eb8b07e6007d8987433f84fd7536754

#docker 기동상황
➜  docker ps -a
CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                     PORTS               NAMES
166861a3e8cc        centos:latest             "/bin/bash"         9 seconds ago       Up 8 seconds                                   centos8
4e0c7359e1f3        lunight_gitlab:20191022   "/assets/wrapper"   2 months ago        Exited (137) 5 hours ago                       gitlab

#컨테이너에서 bash  ssh 접근
# -i옵션 : 대화형(interactive)조작을 위해 표준입력을 유지
# -t옵션 : docker run에서 -t옵션과 같이 TTY 할당
➜  docker exec -it centos8 /bin/bash
[root@33e856dd1054 /]#

#container stop
➜  docker stop centos8
➜  docker ps -a
CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                        PORTS               NAMES
33e856dd1054        centos:centos7            "/bin/bash"         8 minutes ago       Exited (137) 20 seconds ago                       centos7
4e0c7359e1f3        lunight_gitlab:20191022   "/assets/wrapper"   2 months ago        Exited (137) 5 minutes ago                        gitlab

#docker container 삭제
➜  docker rm -f centos8
```

### centos 이미지 만들어서 hub에 등록하기

- Dockerfile(Dockerfile-centos8참고)

```
# centos8 dockerfile
# centos:latest // centos8 docker container image
FROM centos:latest
#ADD <file name> <save path>
#RUN : install script
RUN yum install -y epel-release
CMD ["/bin/bash"]
```

- 이미지 생성

```
➜  docker build -t lunightlab/centos8-lunight:1.0 .
Sending build context to Docker daemon  11.78kB
Step 1/3 : FROM centos:latest
 ---> 470671670cac
Step 2/3 : RUN yum install -y epel-release
 ---> Running in c30e22c98c31
CentOS-8 - AppStream                            2.1 MB/s | 6.0 MB     00:02
CentOS-8 - Base                                 114 kB/s | 4.0 MB     00:36
CentOS-8 - Extras                               4.7 kB/s | 2.1 kB     00:00
Dependencies resolved.
================================================================================
 Package               Architecture    Version            Repository       Size
================================================================================
Installing:
 epel-release          noarch          8-5.el8            extras           22 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 22 k
Installed size: 30 k
Downloading Packages:
epel-release-8-5.el8.noarch.rpm                 613 kB/s |  22 kB     00:00
--------------------------------------------------------------------------------
Total                                            53 kB/s |  22 kB     00:00
warning: /var/cache/dnf/extras-cbfb2f07b0021b7e/packages/epel-release-8-5.el8.noarch.rpm: Header V3 RSA/SHA256 Signature, key ID 8483c65d: NOKEY
CentOS-8 - Extras                               879 kB/s | 1.6 kB     00:00
Importing GPG key 0x8483C65D:
 Userid     : "CentOS (CentOS Official Signing Key) <security@centos.org>"
 Fingerprint: 99DB 70FA E1D7 CE22 7FB6 4882 05B5 55B3 8483 C65D
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1
  Installing       : epel-release-8-5.el8.noarch                            1/1
  Running scriptlet: epel-release-8-5.el8.noarch                            1/1
  Verifying        : epel-release-8-5.el8.noarch                            1/1

Installed:
  epel-release-8-5.el8.noarch

Complete!
Removing intermediate container c30e22c98c31
 ---> 54142fcf25c1
Step 3/3 : CMD ["/bin/bash"]
 ---> Running in 7c3fd998d846
Removing intermediate container 7c3fd998d846
 ---> 1d1b433cdaa5
Successfully built 1d1b433cdaa5
Successfully tagged lunightlab/centos8-lunight:1.0

➜  docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
lunightlab/centos8-lunight   1.0                 1d1b433cdaa5        50 seconds ago      271MB

```

- 컨테이너 실행

```
➜  docker run -td --name lunight-centos8 \
> lunightlab/centos8-lunight:1.0
f9081f13dcc0edd90fc117ec71e183cdaccd592a0e0b3677a9ca98b563c34e4d
➜  docker ps -a
CONTAINER ID        IMAGE                            COMMAND             CREATED             STATUS                     PORTS               NAMES
f9081f13dcc0        lunightlab/centos8-lunight:1.0   "/bin/bash"         6 seconds ago       Up 5 seconds                                   lunight-centos8
4e0c7359e1f3        lunight_gitlab:20191022          "/assets/wrapper"   2 months ago        Exited (137) 6 hours ago                       gitlab
```

- 실행상태에서 커밋하기 (이미지가 변경되면 바로 저장할 수 있음.)

```
➜  docker ps -a
CONTAINER ID        IMAGE                            COMMAND             CREATED             STATUS                     PORTS               NAMES
f9081f13dcc0        lunightlab/centos8-lunight:1.0   "/bin/bash"         9 minutes ago       Up 9 minutes                                   lunight-centos8
4e0c7359e1f3        lunight_gitlab:20191022          "/assets/wrapper"   2 months ago        Exited (137) 6 hours ago                       gitlab
➜  docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
lunightlab/centos8-lunight   1.0                 1d1b433cdaa5        14 minutes ago      271MB
nginx                        latest              2073e0bcb60e        47 hours ago        127MB
➜  Docker git:(master) ✗ docker commit lunight-centos8 lunightlab/centos8-lunight
sha256:ee5da0b3052522820b9b5d91afe781a4aa97790dbabcade2ead2fb83534e1e38
➜  docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
lunightlab/centos8-lunight   latest              ee5da0b30525        4 seconds ago       271MB
lunightlab/centos8-lunight   1.0                 1d1b433cdaa5        15 minutes ago      271MB
nginx                        latest              2073e0bcb60e        47 hours ago        127MB
➜  Docker git:(master) ✗ docker commit lunight-centos8 lunightlab/centos8-lunight:2.0
sha256:f28c33753f34327e96b9b77eb1b342ab80f1f64690a940c4c5c7041f679789a5
➜  docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
lunightlab/centos8-lunight   2.0                 f28c33753f34        4 seconds ago       271MB
lunightlab/centos8-lunight   latest              ee5da0b30525        37 seconds ago      271MB
lunightlab/centos8-lunight   1.0                 1d1b433cdaa5        16 minutes ago      271MB
nginx                        latest              2073e0bcb60e        47 hours ago        127MB

```

- docker hub에 업로드하기

```
➜  docker push lunightlab/centos8-lunight:2.0
The push refers to repository [docker.io/lunightlab/centos8-lunight]
29e08c235e1e: Pushed
f7aa30878f3c: Pushed
0683de282177: Mounted from library/centos
2.0: digest: sha256:974e2f9fe63daf7edb530d3aeab6ea4cee71737686f40f87ae898fb4c72aa275 size: 948
```

## #HashTag

## About LuLabTemplate
- Lunight Lab Github Template  
- Temlate version 1.0 : 초기작성, issue 및 pull request template 추가  

## README.md History
- 2020.2.3 : 템플릿 첫작성.
- 2020.2.4 : 첫작성.

## License
- MIT

## Author
👤 **Lunight**

- Github: [@Lunight](https://github.com/LunightLab)
- Email: [kimkshahaha@gmail.com](kimkshahaha@gmail.com)

<div align="center">

<sub><sup>Written by <a href="https://github.com/LunightLab">@Lunight</a></sup></sub><small></small>

</div>



