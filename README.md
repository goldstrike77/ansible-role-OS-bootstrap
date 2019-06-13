![](https://img.shields.io/badge/Ansible-Operating_System-green.svg?logo=angular&style=for-the-badge)

>__请注意，此角色的最初设计目标更关注初始安装和引导环境配置，目前不涉及执行连续维护，在您的系统上运行此角色存在潜在危险的情况，包括服务中断、数据损坏，因此仅适用于测试和开发目的，不应在生产环境中使用。
>作者不对角色内容之准确性、完整性、可靠性、可用性做保证，作者不对因使用本角色而造成的或与之有关的任何损失承担责任，在任何情况下，作者都不对因使用本角色而造成的或与之有关的任何间接、附带或结果性损失负责或承担责任。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_linux_win.png" align="right" /></p>

__Table of Contents__

- [概述](#概述)
- [要求](#要求)
  * [操作系统](#操作系统)
- [ 变量](#变量)
  * [主要变量](#主要变量)
  * [其他变量](#其他变量)
- [依赖关系](#依赖关系)
- [示例](#示例)
  * [主机清单文件](#主机清单文件)
  * [角色配置中的变量](#角色配置中的变量)
  * [组变量和剧本的组合](#组变量和剧本的组合)
- [许可证](#许可证)
- [作者信息](#作者信息)
- [贡献者](#贡献者)

## 概述
此角色负责公有/私有云主机使用模板部署完毕后的一些操作系统基础配置。

## 要求
### 操作系统
此角色将在以下操作系统上工作：

  * CentOS 6, 7
  * Windows 2012, 2016

## 变量

### 主要变量 #
需要（或需要）修改的变量

##### 任务参数
* `os_config`: 是否执行主机初始配置。
* `os_datadisc`: 是否挂载数据盘。
* `os_exporter`: 是否部署普罗米修斯客户端。
* `os_harden`: 是否执行主机加固配置。
* `os_software`: 是否执行主机基本软件安装和更新。

##### 通用参数
* `os_audit`: 是否启用主机审计。
* `os_disable_ipv6`: 是否关闭IPv6。
* `os_pass_length`: 账户最低密码长度。
* `os_pass_maxAge`: Windows主机账户密码有效期。
* `os_proxy_server`: 主机代理服务器。
* `os_update_password`: 修改新部署Linux主机管理账户密码。

##### 公共领事参数
* `environments`: 定义系统环境。
* `consul_public_register`: 是否向公共领事注册普罗米修斯终端。
* `consul_public_exporter_token`: 公共领事客户端访问控制令牌。
* `consul_public_clients`: 公共领事公共客户端列表。
* `consul_public_http_port`: 公共领事公共客户端端口。

##### 远程日志参数
* `syslog`: 是否启用远程日志。
* `syslog_port`: 远程日志服务器端口。
* `syslog_protocol`: 远程日志服务器协议。
* `syslog_server`: 远程日志服务器地址列表。

##### Linux 数据盘参数
* `os_linux_disc_device`: 数据盘块设备。
* `os_linux_fsopts`: 数据盘挂载参数。
* `os_linux_fstype`: 数据盘文件系统。
* `os_linux_lv`: 逻辑卷名称。
* `os_linux_lv_size`: 逻辑卷容量。
* `os_linux_mount_point`: 逻辑卷挂载点。
* `os_linux_vg`: 逻辑卷卷组名称。

##### Linux 系统参数
* `os_linux_disable_fs_exec_flags`: 磁盘分区安全挂载参数。
* `os_linux_disable_fs_home_exec`: /home 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_shm_exec`: /dev/shm 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_tmp_exec`: /tmp 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_vartmp_exec`: /var/tmp 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_tcp_offloading`: 是否禁用TCP卸载。
* `os_linux_disable_RootLogin`: 是否禁用root登录。
* `os_linux_disable_selinux`: 是否禁用selinux。
* `os_linux_disable_sysstat_collect`: 是否禁用sysstat监测。
* `os_linux_disable_unused_module`: 是否禁用不需要的模块。
* `os_linux_disable_unused_service`: 是否禁用不需要的服务。
* `os_linux_enables_needed_service`: 是否启用需要的服务。
* `os_linux_grub_add_args`: GRUB新增参数。
* `os_linux_id_rsa`: 主机SSH密钥。
* `os_linux_MTA_relayhost`: 邮件中继服务器地址。
* `os_linux_syslog_local_keep`: 本地日志保留期(周)。
* `os_linux_tz`: 主机时区。
* `os_linux_ulimit_nofile`: 会话打开的文件/文件描述符的最大数目。
* `os_linux_ulimit_nproc`: 会话打开的系统进程的最大数目。
* `os_linux_user_pw`: 密码复杂度策略。

##### Windows 系统参数
* `os_win_disable_allowindexingencryptedstoresoritems`: 是否禁止对项目建立索引。
* `os_win_disable_allowyouraccount`: 是否禁止用户更改帐户设置。
* `os_win_disable_autodownload`: 是否禁止自动下载更新。
* `os_win_disable_autorun`: 是否禁止自动播放。
* `os_win_disable_autoupdate`: 是否禁止自动更新。
* `os_win_disable_hidefileext`: 是否隐藏已知文件类型的扩展名。
* `os_win_disable_osupgrade`: 是否禁止系统升级。
* `os_win_disable_rss`: 是否禁用接收端缩放。
* `os_win_disable_task`: 需要关闭的系统任务调度程序。
* `os_win_event_log`: 需要配置的系统事件日志。
* `os_win_event_log_MaxSize`: 本地系统事件日志的最大容量(KB)。
* `os_win_format`: 主机语言格式
* `os_win_fs_audit_rule`: 文件系统审计规则。
* `os_win_fs_audit_user`: 文件系统审计账户名。
* `os_win_gpo_audit_policy`: 组审计策略。
* `os_win_location`: 主机地理位置。
* `os_win_network_location`:网络位置。
* `os_win_pagefile_size`: 虚拟内存页面文件容量(MB)。
* `os_win_roles`: 需要安装的系统组件。
* `os_win_software`: 需要安装的第三方软件。
* `os_win_tz`: 主机时区。
* `os_win_unicode`: 主机字符集编码。
* `os_win_update_category`: 需要更新的类别列表。

##### Windows 普罗米修斯客户端参数
* `wmi_exporter_collector`: 普罗米修斯客户端收集器。


##### Linux 普罗米修斯客户端参数
* `node_exporter_port`: 普罗米修斯客户端端口。
* `node_exporter_collector`: 普罗米修斯客户端系统收集器。

### 其他变量
有一些变量位于 vars/main.yml:

## 依赖关系
- Ansible versions > 2.6

## 示例

### 主机清单文件
参见测试/库存示例

    node01 ansible_host='192.168.1.10'

### 角色配置中的变量
变量作为参数传入使用角色的示例

    - hosts: all
      roles:
         - role: ansible-role-OS-bootstrap

### 组变量和剧本的组合
您还可以使用组变量或主机变量文件来设置此角色所需的变量。您应该更改的文件: group_vars/all or host_vars/`group_name`

    os_config: false
    os_datadisc: false
    os_exporter: false
    os_harden: false
    os_software: false
    os_audit: false
    os_disable_ipv6: false
    os_pass_length: '12'
    os_pass_maxAge: '60'
    environments: 'SIT'
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_clients:
      - 'localhost'
    consul_public_http_port: '8500'
    syslog: false
    syslog_port: '12201'
    syslog_protocol: 'udp'
    syslog_server:
      - '127.0.0.1'
    os_linux_disc_device: '/dev/sdb'
    os_linux_fsopts: 'defaults,noatime,nobarrier'
    os_linux_fstype: 'xfs'
    os_linux_lv: 'lv_data'
    os_linux_lv_size: '100%FREE'
    os_linux_mount_point: '/data'
    os_linux_vg: 'VolGroup01'
    os_linux_disable_fs_exec_flags: 'rw,nosuid,nodev,noexec,relatime'
    os_linux_disable_fs_home_exec: false
    os_linux_disable_fs_shm_exec: true
    os_linux_disable_fs_tmp_exec: false
    os_linux_disable_fs_vartmp_exec: false
    os_linux_disable_tcp_offloading: true
    os_linux_disable_RootLogin: true
    os_linux_disable_selinux: true
    os_linux_disable_sysstat_collect: true
    os_linux_disable_unused_module: true
    os_linux_disable_unused_service: true
    os_linux_enables_needed_service: true
    os_linux_grub_add_args:
      - 'ipv6.disable={% if os_disable_ipv6 %}1{% else %}0{% endif %}'
      - 'transparent_hugepage=never'
      - 'numa=off'
    os_linux_id_rsa: 'MFwwDQYJKoZIhvcNAQFBBQADSwAwSAJBAIUcZI4Qk5H60d0gD5zXqOYqmX67N5Qb8q1SdsQckg4b22rcdrZHftc2YPN168WEWWKyviVPG4yk0VEOWdc9l9cCAwEAAQ=='
    os_linux_syslog_local_keep: '2'
    os_linux_tz: 'Asia/Shanghai'
    os_linux_ulimit_nofile: '20480'
    os_linux_ulimit_nproc: '20480'
    os_linux_user_pw:
      minlen: '{{ os_pass_length | default(12) }}'
      dcredit: '-1'
      ucredit: '-1'
      lcredit: '-1'
    os_win_disable_allowindexingencryptedstoresoritems: false
    os_win_disable_allowyouraccount: false
    os_win_disable_autodownload: false
    os_win_disable_autorun: false
    os_win_disable_autoupdate: false
    os_win_disable_hidefileext: false
    os_win_disable_osupgrade: false
    os_win_disable_rss: false
    os_win_disable_task:
      - 'ScheduledDefrag'
      - 'ServerManager'
    os_win_event_log:
      - 'Application'
      - 'Security'
      - 'Setup'
      - 'System'
    os_win_event_log_MaxSize: '4096'
    os_win_format: 'en-US'
    os_win_fs_audit_rule:
      - 'AppendData'
      - 'CreateDirectories'
      - 'CreateFiles'
      - 'Delete'
      - 'DeleteSubdirectoriesAndFiles'
      - 'WriteData'
    os_win_fs_audit_user: 'Everyone'
    os_win_gpo_audit_policy:
      - 'Account Logon'
      - 'Logon/Logoff'
      - 'Account Management'
      - 'DS Access'
      - 'Object Access'
      - 'Policy change'
      - 'Privilege use'
    os_win_location: '45'
    os_win_network_location: 'Private'
    os_win_pagefile_size: 4096
    os_win_roles:
      - 'Telnet-Client'
    os_win_software:
      - 'googlechrome'
      - 'notepadplusplus.install'
      - 'nxlog'
      - 'peazip.install'
    os_win_tz: 'China Standard Time'
    os_win_unicode: 'zh-CN'
    os_win_update_category: ['CriticalUpdates', 'SecurityUpdates']
    wmi_exporter_collector:
      - 'ad'
      - 'cpu'
      - 'cs'
      - 'dns'
      - 'iis'
      - 'logical_disk'
      - 'net'
      - 'os'
      - 'service'
      - 'system'
      - 'tcp'
      - 'textfile'
    wmi_exporter_extra_collector: '--collector.service.services-where="Name=''nxlog''"'
    node_exporter_port: '9100'
    node_exporter_collector:
      - 'arp'
      - 'bcache'
      - 'conntrack'
      - 'cpu'
      - 'entropy'
      - 'filefd'
      - 'hwmon'
      - 'infiniband'
      - 'ipvs'
      - 'loadavg'
      - 'meminfo'
      - 'netdev'
      - 'netstat'
      - 'nfs'
      - 'ntp'
      - 'sockstat'
      - 'stat'
      - 'time'
      - 'uname'
      - 'vmstat'
      - 'timex'
      - 'systemd'
      - 'textfile'
    node_exporter_systemd_collector:
      - 'sshd'
      - 'auditd'
      - 'rsyslog'
      - 'crond'
      - 'ntpd'
    node_exporter_ignored_mount_points_collector:
      - 'data/docker/'
      - 'dev'
      - 'proc'
      - 'rootfs'
      - 'rpc_pipefs'
      - 'run'
      - 'run/docker/netns/'
      - 'sys'
    node_exporter_ignored_devices_collector:
      - 'ram'
      - 'loop'
      - 'fd'
      - 'sr'

## 许可证
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## 作者信息
请发送您的建议使这个角色更好。

## 贡献者
特别感谢[上海联蔚信息科技有限公司](http://www.connext.com.cn)对这个角色的贡献。

----------

##### 如果觉得对您有帮助，可以通过下列形式进行捐赠。
<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/donate.png"/></p>
