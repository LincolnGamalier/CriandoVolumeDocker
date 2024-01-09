# CriandoVolumeDocker
 Persistência de dados


**docker volume**

lincoln@UbuntuHML:~$ docker volume

Usage:  docker volume COMMAND

Manage volumes

Commands:
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes
  update      Update a volume (cluster volumes only)

Run 'docker volume COMMAND --help' for more information on a command.

**docker volume ls**

root@UbuntuHML:/home/lincoln# docker volume ls
DRIVER    VOLUME NAME
local     7c05e33043bee59c9675b5bb8ca50c5b160b632a57be0f7b30574888c6091cc7
local     79e995aecf5e14d8fb99329dbf7791e18e9935dab4dcd1eba66d12776db7460a
local     9957f7aca9deb7f2997c02f9b787567c57ae140d8879bbfc7c5d5ca6c1b0ab4f

**docker volume create**

root@UbuntuHML:/home/lincoln# docker volume ls
DRIVER    VOLUME NAME
local     7c05e33043bee59c9675b5bb8ca50c5b160b632a57be0f7b30574888c6091cc7
local     79e995aecf5e14d8fb99329dbf7791e18e9935dab4dcd1eba66d12776db7460a
local     9957f7aca9deb7f2997c02f9b787567c57ae140d8879bbfc7c5d5ca6c1b0ab4f

**docker volume ls**

root@UbuntuHML:/home/lincoln# docker volume ls
DRIVER    VOLUME NAME
local     7c05e33043bee59c9675b5bb8ca50c5b160b632a57be0f7b30574888c6091cc7
local     22ce19c81a1ecfd8fcad84d0baee30b88331f27ab4315553ccdbee00afde1d62
local     79e995aecf5e14d8fb99329dbf7791e18e9935dab4dcd1eba66d12776db7460a
local     9957f7aca9deb7f2997c02f9b787567c57ae140d8879bbfc7c5d5ca6c1b0ab4f
root@UbuntuHML:/home/lincoln# 

**Apagando volumes não utilizados**

--docker volume prune--

root@UbuntuHML:/home/lincoln# docker volume prune
WARNING! This will remove anonymous local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Volumes:
22ce19c81a1ecfd8fcad84d0baee30b88331f27ab4315553ccdbee00afde1d62

Total reclaimed space: 0B

**Anexando volumes a contaniers**

--docker run -v meu_volume postgres--

root@UbuntuHML:/home/lincoln# docker run --name some-postgres -e POSTGRES_PASSWORD=***** -d postgres
9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035
root@UbuntuHML:/home/lincoln# 

**docker ps -a**

root@UbuntuHML:/home/lincoln# docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED              STATUS                          PORTS      NAMES
9d8da9f0414e   postgres      "docker-entrypoint.s…"   53 seconds ago       Up 52 seconds                   5432/tcp   some-postgres


--docker volumes ls--

root@UbuntuHML:/home/lincoln# docker volume ls
DRIVER    VOLUME NAME
local     0cd06175c1bfcaecf4cdfa4054e76134084e6e9441bcc0391b8e201672ae516d
local     2e6d27ae5a34ace7f6f678874f906c3264f617691b5b8d32f0fe1fa908b18044
local     4a3a4e8b5a408bc7c916428f06d67ff163ac6f801cfdfba9928ffa2befc1c373
local     5a6a23806c6ad7900b13e8f71d50f3c1bd929af724f49d8db81df79ced30c14b
local     5ee34b8c3619ae3e17f193c917e89b5c9fdca164308f240a83ea43c0755c261a
local     7c05e33043bee59c9675b5bb8ca50c5b160b632a57be0f7b30574888c6091cc7
local     26b376a9d445708c13ab890d5b59db856dabaa74f2a21ac87efe0aec66a98d7c
local     79e995aecf5e14d8fb99329dbf7791e18e9935dab4dcd1eba66d12776db7460a
local     99b703880040760fb118a8c7da997d0b540a594165b181e9344413cfe5b9fef2
local     217afa1b5de2732c02239207cfc5d20fe81bebc7f4b59486a2fe72a8eeec7ec1
local     00407a164c24d39051d096a13811d6b85d99c51e3c5fcba31c15ca7a541b363c
local     2461bc794258d91170828c21362bf02ea69257e8d4a9b48ebec567d8b1554c91
local     2542d29d99c5522972b608924d51bf88397cfd29053f7a3a5cf58818791b42f1
local     9957f7aca9deb7f2997c02f9b787567c57ae140d8879bbfc7c5d5ca6c1b0ab4f
local     066366f917d1731cfa2e0cbacb54e32446e145319a061d55bb79a2bb1b962617
local     3836670c03503059cb000fc65a958c5b0659c27fbd22f9162e1d4131d189f78c
local     ba7a8eb2aa14cdfe7cce1dd371962b1fa86e5e56a7474441bdb48ab7d4d7b8bd
local     e9ecd6ab569e014dd2dc721e1e39ba95b2edb77c3b57ed41354bd22789920088
local     e54a3cc99ed055b6dcff1c2fe61d947bc40bd376fe1a8ac3a536bb04ca5b932f
local     e61a548df6cb470032965da9b6704f758d43b60e9de15c28c0275e0a7ab447c9
root@UbuntuHML:/home/lincoln# 


docker inspect meu_volume


root@UbuntuHML:/home/lincoln# docker inspect some-postgres
[
    {
        "Id": "9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035",
        "Created": "2024-01-09T14:24:32.387485615Z",
        "Path": "docker-entrypoint.sh",
        "Args": [
            "postgres"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 32718,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-01-09T14:24:32.856938656Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:bdc467e8023271a2f8be7fa1613df3ca57dd9878c8111c39640b9a992ca413bb",
        "ResolvConfPath": "/var/lib/docker/containers/9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035/hostname",
        "HostsPath": "/var/lib/docker/containers/9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035/hosts",
        "LogPath": "/var/lib/docker/containers/9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035/9d8da9f0414ec4808348a1dcd7d4e3bed78ef7dd086d209998f6b71ffe67f035-json.log",
        "Name": "/meu_volume",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                49,
                97
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/340cfc5fdf2fea15ad101b87c3eb47d06a52c965bc29f71bcbb9b851aa1b0cae-init/diff:/var/lib/docker/overlay2/035615455f2c819929e1e881b41be6d8f7bfd7999ead1d67eb0bc8ad19ffd55f/diff:/var/lib/docker/overlay2/2713049ccabac8f84314210df05570cbe5fcb9b668494f7b4711dfe0cda3d801/diff:/var/lib/docker/overlay2/21a214256ef399218418a41f42786220a274cab9b3aac9f6da1fa6b0bacf9b45/diff:/var/lib/docker/overlay2/c67d8ac5ddce39ac4773ccd210b35a6b0fc1ae7070b31e68913b5766ea72ec85/diff:/var/lib/docker/overlay2/e1089b0b81d6e41f009ec81e3546b920f68b105dde9a55f30e1cf4ab36bb9286/diff:/var/lib/docker/overlay2/ec026ff0f90f80c9021597dc8ee3a63b9adc84ef3a02c31d5c988bc5cca13149/diff:/var/lib/docker/overlay2/a90808c8b84342d59451bd9357d877111d685cf995547abe183c9b58f3fce890/diff:/var/lib/docker/overlay2/fb323e71c421c1387c8b1b096e0bedce5af0e166f4e7474b34f3d4e693a39c37/diff:/var/lib/docker/overlay2/8fcf3bb2c0f523ef4db8816331dae83f41b20e0478664df53ed613a11cb94061/diff:/var/lib/docker/overlay2/b5d1c11aa73e9c075717e17dabad467a80e8153249bcbe8ef9e5c38a2ae1c3b3/diff:/var/lib/docker/overlay2/5d879f337c75db5c35af707be6c8c6abd02599159971cc499d998f4f94a08e7b/diff:/var/lib/docker/overlay2/3bebb4bbbc41782557286a3eb22b4b1a548df93576777725b953798e58cd0000/diff:/var/lib/docker/overlay2/d968b2b4949297846a9c4a59c11a1578f81a3603752001f832528a002244fe3d/diff:/var/lib/docker/overlay2/e765ae70eb7abf4fee0f7f4b3496f94cf4455a8cbda4b48789e8772ac4f3520f/diff",
                "MergedDir": "/var/lib/docker/overlay2/340cfc5fdf2fea15ad101b87c3eb47d06a52c965bc29f71bcbb9b851aa1b0cae/merged",
                "UpperDir": "/var/lib/docker/overlay2/340cfc5fdf2fea15ad101b87c3eb47d06a52c965bc29f71bcbb9b851aa1b0cae/diff",
                "WorkDir": "/var/lib/docker/overlay2/340cfc5fdf2fea15ad101b87c3eb47d06a52c965bc29f71bcbb9b851aa1b0cae/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "volume",
                "Name": "5ee34b8c3619ae3e17f193c917e89b5c9fdca164308f240a83ea43c0755c261a",
                "Source": "/var/lib/docker/volumes/5ee34b8c3619ae3e17f193c917e89b5c9fdca164308f240a83ea43c0755c261a/_data",
                "Destination": "/var/lib/postgresql/data",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],
        "Config": {
            "Hostname": "9d8da9f0414e",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "5432/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "POSTGRES_PASSWORD=****",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/postgresql/16/bin",
                "GOSU_VERSION=1.16",
                "LANG=en_US.utf8",
                "PG_MAJOR=16",
                "PG_VERSION=16.1-1.pgdg120+1",
                "PGDATA=/var/lib/postgresql/data"
            ],
            "Cmd": [
                "postgres"
            ],
            "Image": "postgres",
            "Volumes": {
                "/var/lib/postgresql/data": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {},
            "StopSignal": "SIGINT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "e010d2f288adf542fc87ede45ba8e2fb26e6f9033592d0b13310d5f744b0cc14",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "5432/tcp": null
            },
            "SandboxKey": "/var/run/docker/netns/e010d2f288ad",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "7e241874e7d0653753fcd015922111209e804cfa6aeb4cf9f784486fb71c748c",
            "Gateway": "172.17.0.*",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.*",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "5a495942c7893a873972b793ca46397dbe546caf4db0a0518d3e8982cd29af34",
                    "EndpointID": "7e241874e7d0653753fcd015922111209e804cfa6aeb4cf9f784486fb71c748c",
                    "Gateway": "172.17.0.*",
                    "IPAddress": "172.17.0.*",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]

