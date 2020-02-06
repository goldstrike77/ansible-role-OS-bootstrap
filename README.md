![](https://img.shields.io/badge/Ansible-Operating_System-green.svg?logo=angular&style=for-the-badge)

>__请注意，此角色的最初设计目标更关注初始安装和引导环境配置，目前不涉及执行连续维护，在您的系统上运行此角色存在潜在危险的可能性，包括服务中断和数据损坏，因此仅适用于测试和开发目的，不应在生产环境中使用。作者不对角色内容之准确性、完整性、可靠性、可用性做保证，在任何情况下，作者都不对因使用本角色而造成的或与之有关的任何间接、附带或结果性损失负责或承担责任。__
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

### = 主任务参数 =
* `os_config`: 是否执行主机初始配置。
* `os_datadisc`: 是否挂载数据盘。
* `os_exporter`: 是否部署普罗米修斯客户端。
* `os_harden`: 是否执行主机加固配置。
* `os_ossec`: 是否部署入侵检测客户端。
* `os_software`: 是否执行主机基本软件安装和更新。

#### - 主机初始配置参数 -
##### 通用参数
* `os_disable_ipv6`: 是否关闭IPv6。
* `os_proxy_server`: 主机代理服务器。
* `os_dns_search`: 域名系统默认搜索域。
* `os_dns_server`: 域名系统服务器。
* `os_time_server`: 时间服务器。
##### 远程日志参数
* `syslog`: 是否启用远程日志。
* `syslog_port`: 远程日志服务器端口。
* `syslog_protocol`: 远程日志服务器协议。
* `syslog_server`: 远程日志服务器地址列表。
##### Linux 初始参数
* `os_linux_disable_unused_service`: 是否禁用不需要的服务。
* `os_linux_enables_needed_service`: 是否启用需要的服务。
* `os_linux_disable_tcp_offloading`: 是否禁用TCP卸载。
* `os_linux_disable_sysstat_collect`: 是否禁用sysstat监测。
* `os_linux_grub_add_args`: GRUB新增参数。
* `os_linux_id_rsa`: 主机SSH密钥。
* `os_linux_MTA_relayhost`: 邮件中继服务器地址。
* `os_linux_resolver_single_request`: 启用域名解析单一请求。
* `os_linux_shell_history`: 历史记录存储在内存中的行数。
* `os_linux_shell_timeout`: 系统终端空闲等待时间(秒)。
* `os_linux_syslog_local_keep`:本地日志保留期(周)。
* `os_linux_tz`: 主机时区。
* `os_linux_ulimit_nofile`: 会话打开的文件/文件描述符的最大数目。
* `os_linux_ulimit_nproc`: 会话打开的系统进程的最大数目。
* `os_linux_default_umask`: 一般用户默认文件创建模式掩码。
##### Windows 初始参数
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
* `os_win_location`: 主机地理位置。
* `os_win_network_location`: 网络位置
* `os_win_pagefile_size`: 虚拟内存页面文件容量(MB)。
* `os_win_tz`: 主机时区。
* `os_win_unicode`: 主机字符集编码。

#### - 主机数据盘操作 -
##### Linux 数据盘参数
* `os_linux_disc_device`: 数据盘块设备。
* `os_linux_fsopts`: 数据盘挂载参数。
* `os_linux_fstype`: 数据盘文件系统。
* `os_linux_lv`: 逻辑卷名称。
* `os_linux_lv_size`: 逻辑卷容量。
* `os_linux_mount_point`: 逻辑卷挂载点。
* `os_linux_vg`: 逻辑卷卷组名称。
##### Windows 数据盘参数
* `os_win_disk_number`: 数据盘编号。
* `os_win_disk_fsystem`: 分区文件系统。
* `os_win_disk_size`: 分区容量。
* `os_win_disk_letter`: 分区盘符。

#### - 主机加固配置参数 -
* `os_pass_length`: 账户最低密码长度。
* `os_pass_maxAge`: Windows主机账户密码有效期。
* `os_update_password`: 修改新部署Linux主机管理账户密码。
##### 审计参数
* `os_audit`: 是否启用主机审计。
* `os_audit_type`: 审计进程服务类型，auditbeat 或 auditd。
* `os_auditbeat_version`: Beats 版本。
* `os_auditbeat_port_arg`: Beats 通信端口。
* `os_auditbeat_output`: Beats 数据收集器参数。
##### Linux 加固参数
* `os_linux_audit_rules`: Linux 审计规则
* `os_linux_disable_fs_exec_flags`: 磁盘分区安全挂载参数。
* `os_linux_disable_fs_home_exec`: /home 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_shm_exec`: /dev/shm 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_tmp_exec`: /tmp 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_fs_vartmp_exec`: /var/tmp 挂载点分区是否启用安全挂载参数。
* `os_linux_disable_RootLogin`: 是否禁用root登录。
* `os_linux_disable_selinux`: 是否禁用selinux。
* `os_linux_disable_unused_module`: 是否禁用不需要的模块。
* `os_linux_user_pw`: 密码复杂度策略。
##### Windows 加固参数
* `os_win_fs_audit_rule`: 文件系统审计规则。
* `os_win_fs_audit_user`: 文件系统审计账户名。
* `os_win_gpo_audit_policy`: 组审计策略。

#### - 入侵检测系统参数 -
* `ossec_version`: WAZUH代理版本。
* `ossec_managers`: WAZUH管理器参数。
* `ossec_agent_authd`: WAZUH代理注册参数。
* `ossec_agent_config`: WAZUH代理参数。

#### - 主机基本软件安装和更新参数 -
##### Linux 参数
* `/var/[specific OS].yml`
##### Windows 参数
* `os_win_roles`: 需要安装的系统组件。
* `os_win_software`: 需要安装的第三方软件。
* `os_win_update_category`: 需要更新的类别列表。

#### - 普罗米修斯客户端配置参数 -
##### Windows 普罗米修斯客户端参数
* `wmi_exporter_collector`: 普罗米修斯客户端收集器。
##### Linux 普罗米修斯客户端参数
* `os_linux_exporter_type`: 普罗米修斯客户端类型。
* `netdata_collector`: NETDATA客户端系统收集器。
* `node_exporter_collector`: 普罗米修斯客户端系统收集器。
* `node_exporter_systemd_collector`: 普罗米修斯客户端服务收集器。
* `node_exporter_ignored_mount_points_collector`: 普罗米修斯客户端收集器忽略的磁盘挂载点。
* `node_exporter_ignored_devices_collector`: 普罗米修斯客户端收集器忽略的块设备。

#### - 公共领事配置参数 -
* `tags`: 对象自定义标签。
* `hardware_sn`: 设备序列编号。
* `hardware_pn`: 设备服务编号。
* `hardware_cu`: 设备机架编号。
* `environments`: 定义系统环境。
* `exporter_is_install`: 是否部署普罗米修斯客户端。
* `consul_public_register`: 是否向公共领事注册普罗米修斯终端。
* `consul_public_exporter_token`: 公共领事客户端访问控制令牌。
* `consul_public_http_port`: 公共领事公共客户端端口。
* `consul_public_http_prot`: 公共领事公共客户端协议。
* `consul_public_clients`: 公共领事公共客户端列表。

### 其他变量
有一些变量位于 vars/main.yml:

## 依赖关系
- Ansible versions >= 2.8 are supported.
- [Beats](https://github.com/goldstrike77/ansible-role-OS-beats.git)

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

## 许可证
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## 作者信息
请发送您的建议使这个角色更好。

## 贡献者
特别感谢[上海联蔚信息科技有限公司](http://www.connext.com.cn)对这个角色的贡献。

----------

##### 如果觉得对您有帮助，可以通过下列形式进行捐赠。
<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/donate.png"/></p>