
### 检查密码长度最小值

<i class="fa fa-pencil-square-o" aria-hidden="true"></i>打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\帐户策略\密码策略”，在右边窗格中找到“密码长度最小值”，配置为8

### 检查“强制密码历史”个数

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\帐户策略\密码策略”，在右边窗格中找到“强制密码历史”，配置为5

### 检查管理员帐户名称

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\安全选项”，在右边窗格中找到“(帐户:)重命名(系统)管理员帐户”，更改其默认设置“Administrator”(注意：若当前是以Administrator用户登录，则无法更改)。 不建议为此新增一个具有administrator权限的用户

### 检查帐户锁定阈值是否不为0

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\帐户策略\帐户锁定策略”，在右边窗格中找到“帐户锁定阈值”，配置为非0值。配置为0表示帐户将永远不会被锁定。

### 检查是否已禁止SAM帐户和共享的匿名枚举

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\安全选项”，在右边窗格中找到“网络访问: 不允许 SAM 帐户和共享的匿名枚举”，配置为“启用”(在Windows2000下，将“对匿名连接的额外限制”配置为“不允许枚举SAM账号和共享”)。

### 检查可远程访问的注册表路径和子路径

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\安全选项”，在右边窗格中找到“网络访问: 可远程访问的注册表路径和子路径”，配置为空。Windows2000和WindowsXP没有此设置，不需配置。

### 检查可远程访问的注册表路径

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\安全选项”，在右边窗格中找到“网络访问: 可远程访问的注册表路径”，配置为空。Windows2000没有此设置，不需配置。

### 检查“审核对象访问”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核对象访问”，勾选“成功”和“失败”。

### 检查“审核特权使用”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核特权使用”，勾选“成功”和“失败”。

### 检查“审核进程跟踪”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核进程跟踪”，勾选“成功”和“失败”。

### 检查“审核登录事件”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核登录事件”，勾选“成功”和“失败”。

### 检查“审核目录服务访问”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核目录服务访问”，勾选“成功”和“失败”。

### 检查“审核系统事件”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核系统事件”，勾选“成功”和“失败”。

### 检查“审核帐户登录事件”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核帐户登录事件”，勾选“成功”和“失败”。

### 检查“审核策略更改”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核策略更改”，勾选“成功”和“失败”。

### 检查“审核帐户管理”级别

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\Windows设置\安全设置\本地策略\审核策略”，在右边窗格中找到“审核帐户管理”，勾选“成功”和“失败”。

### 检查是否已开启Windows防火墙

需启用防火墙，不建议使用

### 检查源路由配置

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“DisableIPSourceRouting”、类型为DWORD、数据为标准值的数值，若已存在则修改其数据。此数据的有效值为0-2，其中0表示转发所有数据包，1表示不转发源路由的数据包，2表示丢弃所有传入源路由的数据包。

### 检查是否已修改默认的远程桌面(RDP)服务端口

"[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp] 双击右边 PortNumber——点十进制——更改值为：22389 —— 点确定。
然后找到： [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp] 双击右边 PortNumber——点十进制——更改值为：22389 —— 点确定。"

### 检查TCP连接请求阈值

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“TcpMaxPortsExhausted”、类型为DWORD、数据为标准值(注意：标准值为16进制表示)的数值，若已存在则修改其数据。此数据的有效值为在0-ffff(16进制)。

### 检查是否已启用SYN攻击保护

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“SynAttackProtect”、类型为DWORD、数据为标准值(注意：标准值为16进制表示)的数值，若已存在则修改其数据。此数据的有效值为0-1。

### 检查取消尝试响应 SYN 请求之前要重新传输 SYN-ACK 的次数

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“TcpMaxConnectResponseRetransmissions”、类型为DWORD、数据为标准值的数值，若已存在则修改其数据。此数据的有效值为0-255。

### 检查处于SYN_RCVD 状态下的 TCP 连接阈值

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“TcpMaxHalfOpen”、类型为DWORD、数据为标准值(注意：标准值为16进制表示)的数值，若已存在则修改其数据。此数据的有效值为在64-ffff(16进制)。

### 检查处于SYN_RCVD 状态下，且至少已经进行了一次重新传输的TCP连接阈值

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“TcpMaxHalfOpenRetried”、类型为DWORD、数据为标准值(注意：标准值为16进制表示)的数值，若已存在则修改其数据。此数据的有效值为在50-ffff(16进制)。

### 检查是否已启用TCP最大传输单元(MTU)大小自动探测

打开命令提示符，运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters”，添加名称为“EnablePMTUDiscovery”、类型为DWORD、数据为0，若已存在则修改其数据为0。此数据的有效值为0-1，其中0表示不自动探测MTU大小，都使用576字节的MTU，1表示自动探测MTU大小。

### 检查是否已关闭不必要的服务-DHCPClient

打开命令提示符，运行命令“services.msc”打开服务管理器，停止显示名称为“DHCP Client”的服务

### 检查是否已安装防病毒软件

安装防病毒软件，并及时更新病毒库

### 检查是否已关闭Windows自动播放

打开命令提示符，运行命令“gpedit.msc”打开组策略编辑器，浏览到路径“本地计算机策略\计算机配置\管理模板\Windows组件\自动播放策略”(适用于Windows2008、WindowsVista、Windows2008R2、Windows7)或“本地计算机策略\计算机配置\管理模板\系统”(适用于Windows2000、WindowsXP、Windows2003、Windows2003R2)，在右边窗格中找到“关闭/停用自动播放”，配置为“启用”，且选为对“所有驱动器”生效。

### 检查是否已禁用Windows硬盘默认共享

此项仅适用于非域环境。首先，打开命令提示符，运行命令“compmgmt.msc”打开计算机管理面板，浏览到路径“计算机管理(本地)\系统工具\共享文件夹\共享”，删除所有硬盘默认共享；然后，在命令提示符中运行命令“regedit”打开注册表编辑器，浏览到路径“HKEY_LOCAL_MACHINE\System\CurrentControlSet\ Services\LanmanServer\Parameters\”，添加名称为“AutoShareServer”和“AutoShareWks”、类型为DWORD、数据为0的两个数值，若已存在则修改其数据。注意：若关闭C盘默认共享(C$)，将不能使用BVS的SMB扫描。
