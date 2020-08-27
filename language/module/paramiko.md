# Paramiko

## 介绍

paramiko是SSHv2的python实现的一个第三方包


## 安装

pip install paramiko


## 介绍



## API

### **Transport**

| 方法 | 功能描述 | 返回值 |
|-----|-----|------|
|accept|||
|add_server_key|||
|atfork|||
|auth_gssapi_keyex|||
|auth_gssapi_with_mic|||
|auth_interactive|||
|auth_interactive_dumb|||
|auth_none|||
|auth_password|||
|auth_publickey|||
|cancel_port_forward|||
|close|||
|connect|||
|get_banner|||
|get_exception|||
|get_hexdump|||
|get_log_channel|||
|get_remote_server_key|||
|get_security_options|||
|get_server_key|||
|get_username|||
|getpeername|||
|global_request|||
|is_active|||
|is_authenticated|||
|static load_server_moduli|||
|open_channel|||
|open_forward_agent_channel|||
|open_forwarded_tcpip_channel|||
|open_session|||
|open_sftp_client|||
|open_x11_channel|||
|renegotiate_keys|||
|request_port_forward|||
|send_ignore|||
|set_gss_host|||
|set_hexdump|||
|set_keepalive|||
|set_log_channel|||
|set_subsystem_handler|||
|start_client|||
|start_server|||
|use_compression|||


### **SSHClient**

| 方法 | 功能描述 | 返回值 |
|-----|-----|------|
|close|||
|connect|||
|exec_command|||
|get_host_keys|||
|get_transport|||
|invoke_shell|||
|load_host_keys|||
|load_system_host_keys|||
|open_sftp|||
|save_host_keys|||
|set_log_channel|||
|set_missing_host_key_policy|||


### **Channel**

| 方法 | 功能描述 | 返回值 |
|-----|-----|------|
|close|||
|exec_command|||
|exit_status_ready|||
|fileno|||
|get_id|||
|get_name|||
|get_pty|||
|get_transport|||
|getpeername|||
|gettimeout|||
|invoke_shell|||
|invoke_subsystem|||
|makefile|||
|makefile_stderr|||
|makefile_stdin|||
|recv|||
|recv_exit_status|||
|recv_ready|||
|recv_stderr|||
|recv_stderr_ready|||
|request_forward_agent|||
|request_x11|||
|resize_pty|||
|send|||
|send_exit_status|||
|send_ready|||
|send_stderr|||
|sendall|||
|sendall_stderr|||
|set_combine_stderr|||
|set_environment_variable|||
|set_name|||
|setblocking|||
|settimeout|||
|shutdown|||
|shutdown_read|||
|shutdown_write|||
|update_environment|||

### **SFTPClient**

| 方法 | 功能描述 | 返回值 |
|-----|-----|------|
|chdir|||
|chmod|||
|chown|||
|close|||
|file|||
|classmethod from_transport|||
|get|||
|get_channel|||
|getcwd|||
|getfo|||
|listdir|||
|listdir_attr|||
|listdir_iter|||
|lstat|||
|mkdir|||
|normalize|||
|open|||
|posix_rename|||
|put|||
|putfo|||
|readlink|||
|remove|||
|rename|||
|rmdir|||
|stat|||
|symlink|||
|truncate|||
|unlink|||
|utime|||

## 最简ssh

```
import paramiko
s = paramiko.SSHClient()
s.set_missing_host_key_policy(paramiko.AutoAddPolicy())
s.connect(hostname='10.138.111.227', port=22, username='wgadmin',key_filename='/home/automation/Dimension2.2_Key/sshd_ca_key',timeout=60)
channel = s.invoke_shell(width=1024)
channel.send_ready()
channel.recv(1024*1024)
channel.sendall('''/opt/watchguard/dimension/bin/psql -c "select * from cluster_traffic where sn='80DB02BDD68E6' and update_time::timestamp = timestamp '2020-07-07T06:34:27' and msg='ProxyAllow: HTTP request method match';" -U wguser dimension\n''')
channel.recv(1024*1024)
```




https://www.cnblogs.com/xiao-apple36/p/9144092.html

| 属性名 | 含义 | 常用属性值 |
|-----|-----|------|
| border | 设置表格的边框（默认border="0"无边框）  | 像素值 |
| cellspacing | 设置单元格与单元格边框之间的空白间距   | 像素值（默认2像素）|
| cellpadding| 设置单元格内容与单元格边框之间的空白间距   | 像素值（默认1像素）|
| width | 设置表格的宽度   | 像素值|
| height | 设置表格的高度   | 像素值|
| align | 设置表格在网页中的水平对齐方式   | left、right、center|

