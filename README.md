## Zabbix NVMe Health Monitoring

This python script uses `nvme` command on Linux to scan NVMe disks on the server and check the discovered disks' health.

## Install

1) Install `nvme-cli` package on your server

Debian/Ubuntu:

```
$ sudo apt-get install nvme-cli
```

CentOS/RHEL:

```
$ yum install nvme-cli
```


2) Import the `zabbix_template.xml` into your Zabbix templates dashboard. This template is pre-configured and will add a new one called **Template NVMe**.


3) Copy the configuration files:

```
$ mkdir /etc/zabbix/scripts/ && sudo chowd -R zabbix:zabbix /etc/zabbix/scripts/
$ cp zabbix_nvme.conf /etc/zabbix/zabbix_agentd.d/
$ cp nvme_discover.py /etc/zabbix/scripts/
$ cp sudoers_zabbix_nvme /etc/sudoers.d/
$ systemctl restart zabbix-agent
```

4) Add the template to the hosts you want to monitor. 



## Configuration

The pre-defined configuration can be modified directly after importing the template. The default discovery rule is 1 hour and only extracts the **percentage_used** which shows how healthy the disk is.

The default trigger for the template is above 80.