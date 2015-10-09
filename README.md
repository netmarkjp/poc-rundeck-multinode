poc-realtime-monitoring-dstat-graphite
=========================================

# Requirements

- CentOS7 x86_64
- Rundeck 2.5.3
- java-1.7.0-openjdk

If did not work well,
try ``vagrant halt`` and ``vagrant up`` to disable SELinux.

# URL

- Rundeck
    - [http://192.168.33.11:4440/](http://192.168.33.11:4440/)
    - [http://192.168.33.12:4440/](http://192.168.33.12:4440/)
- webdav
    - [http://192.168.33.10/webdav/](http://192.168.33.10/webdav/)


# After Installation

## 1. Create project

run below at job01 or job02

```
vagrant ssh job01
sudo su - rundeck
cat <<FIN | bash
rd-project -a create -p exampleProject \
--project.ssh-authentication=privateKey \
--service.NodeExecutor.default.provider=jsch-ssh \
--project.ssh-keypath=/var/lib/rundeck/.ssh/id_rsa \
--resources.source.1.type=url \
--resources.source.1.config.url=http://db01/webdav/node_resources.xml \
--resources.source.1.config.timeout=30 \
--resources.source.1.config.cache=true \
--service.FileCopier.default.provider=jsch-scp
FIN
```

## 2. Use Rundeck

Use rundeck with web browser(any url can use).

admin / admin

- [http://192.168.33.11:4440/](http://192.168.33.11:4440/)
- [http://192.168.33.12:4440/](http://192.168.33.12:4440/)

