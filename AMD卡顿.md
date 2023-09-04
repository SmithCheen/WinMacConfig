# AMD 卡顿

## 关闭ftmp

首先我们需要登录系统去查看一下 BitLocker 是否已经启用，首先打开传统控制面板（搜索控制面板就可找到），选择「BitLocker 驱动器加密」，在管理界面中选择要解密的磁盘，选择「关闭 BitLocker」等待完成数据解密。如果你在解锁 BitLocker 以前关闭了 TPM，**会导致所有的数据不可逆转地丢失**。

之后使用 Windows 徽标键 + R 打开运行，输入「tpm.msc」打开 TPM 管理，在窗格中选择「关闭 TPM」以显示关闭 TPM 安全硬件页面，在「关闭 TPM 安全硬件」对话框中选择一种方法以输入所有者密码并关闭 TPM。

最后重启并进入到 BIOS 设置，找到 「AMD fTPM Switch」选项，选择 Disable 完成关闭即可。

## 关闭windows defence

关闭windows defence的后台自动扫盘

## 关闭HEPT

步骤1:管理员模式运行cmd命令提示符(重要，一定要管理员运行)
步骤2:
指令①
bcdedit /deletevalue useplatformclock

指令②
bcdedit /set useplatformclock false

先执行指令①，如果提示"操作成功"，那就完成了，剩下的指令②就不用管了。如果不是"操作成功"，那就执行一次指令②，再执行指令①就会提示"操作成功"了