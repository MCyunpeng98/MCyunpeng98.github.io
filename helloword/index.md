# Hello,Word


摘要：这是一篇测试文章，一个技术博客的起点。

<!--more-->
** 以下内容为测试文章，复制我自己的文章**

---

在`Windows`中搭建`Homsetead`使用命令`vagrant up` 报错

```
$ vagrant up
Bringing machine 'homestead-7' up with 'virtualbox' provider...
D:/HashiCorp/Vagrant/embedded/gems/2.2.6/gems/vagrant-2.2.6/plugins/provisioners/file/config.rb:20:in `expand_path': incompatible character encodings: UTF-8 and GBK (Encoding::CompatibilityError)
        from D:/HashiCorp/Vagrant/embedded/gems/2.2.6/gems/vagrant-2.2.6/plugins/provisioners/file/config.rb:20:in `expand_path'
        from D:/HashiCorp/Vagrant/embedded/gems/2.2.6/gems/vagrant-2.2.6/plugins/provisioners/file/config.rb:20:in `validate'
```
# **原因就是用户名是中文的**

打开`控制面板`中`更改用户类型`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/TD1pb1gTMM.png!large)
点击`用户`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/19FzQbeCEs.png!large)
选择`更改用户名称`改成`英文`名称

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/hgsopy7o2U.png!large)

此时我们在运行`vagrant up`命令，结果发现还是报错

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/GbJuTLBXmZ.png!large)
**虽然我们修改了用户名称但是我们的文件还是中文的路径:`C:\Users`**

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/u60gjdaSL5.png!large)
现在我们右击`此电脑`选中`管理`
![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/KR0Lp7aTtx.png!large)
选择`本地用户和组`中的`用户`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/RTNGyHpSGq.png!large)
右击`Administrator`选择`属性`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/C512bETbZM.png!large)
把`账号已禁用`取消掉，点击`确定`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/Mf9R1hsV5n.png!large)
`注销`当前账户，选择`Administrator`账户登陆，之后我们打开`此电脑`到`C:\Users`
吧文件改成英文名

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/P39kvELlQC.png!large)

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/mRtui581kF.png!large)

**现在修改注册表**

`windows+R`打开运行，输入`regedit`点击`确定`即可

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/kkKTPAiXJR.png!large)

依次展开`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Profilelist`
![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/Vbep4i7n5m.png!large)
将其修改成对应的名字

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/ZxgcO5OtWC.png!large)

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/xoFLC7fKFJ.png!large)

**到此就完成了，但是，我们要把以前的电脑的环境变量修改一下(有些需要修改)**

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/OPvqNeLn9r.png!large)

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/v6frdDgdQU.png!large)

## 再一次运行`vagrant up`发现还是报错………………
```
Command: ["import", "\\?\C:\Users\Administrator\.vagrant.d\boxes\lc-VAGRANTSLASH-homestead\
6.1.0\virtualbox\box.ovf", "--vsys", "0", "--vmname", "lt-settler_default_1529197839254_477_153171
0722519_67195", "--vsys", "0", "--unit", "9", "--disk", "C:\Users\Administrator\VirtualBox VMs\l
t-settler_default_1529197839254_477_1531710722519_67195\box-disk001.vmdk"]

Stderr: 0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Interpreting \?\C:\Users\Administrator.vagrant.d\boxes\lc-VAGRANTSLASH-homestead\6.1.0\virtualbox\
box.ovf...
OK.
0%...10%...20%...30%...40%...
Progress state: VBOX_E_FILE_ERROR
VBoxManage.exe: error: Appliance import failed
VBoxManage.exe: error: Code VBOX_E_FILE_ERROR (0x80BB0004) - File not accessible or erroneous file c
ontents (extended info not available)
VBoxManage.exe: error: Context: "enum RTEXITCODE __cdecl handleImportAppliance(struct HandlerArg *)"
at line 886 of file VBoxManageAppliance.cpp
```

打开我们的`Oracle VM VirtualBox`软件，左上角`管理`的`全局设定`,`默认电脑的虚拟位置改一下`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/1FQ369VbQF.png!large)

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/4HeGFLwTkp.png!large)

## 此时我们再次运行`vagrant up`,结果他又报错了
```
...
...
There was an error while executing `VBoxManage`, a CLI used by Vagrant for controlling VirtualBox. The command and stderr is shown below.  Command: ["startvm", "da766e1e-a423-4f4d-a37e-8523e39b294f", "--type", "headless"]  Stderr: VBoxManage.exe: error: Raw-mode is unavailable courtesy of Hyper-V. (VERR_SUPDRV_NO_RAW_MODE_HYPER_V_ROOT) VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
```
![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/M803OWoU47.png!large)
这个是因为我们开启了`Hyper-V`，也就是说用了它就不能用`Docker`。

以管理员的方式启动 CMD，输入 `bcdedit` 回车，结果如下图显示：

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/7Q3Mmv6KwE.png!large)

禁用掉 Hyper-V： `bcdedit /set hypervisorlaunchtype off` 然后重启电脑再运行 `vagrant up` 就成功了。如果要打开 Hyper-V：`bcdedit /set hypervisorlaunchtype auto` 需要重启电脑生效。

**重启电脑**，再次运行`vagrant up`命令,终于不在报错
## 成功
输入命令`vagrant ssh`

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/gKORmj95X1.png!large)

附上参考链接：
```
修改系统用户名：https://blog.csdn.net/tanzey/article/details/82657816
关闭HYper-V：https://learnku.com/articles/29420
```

![Windows 搭建 Homsetead 使用 Vagrant up 报错](https://cdn.learnku.com/uploads/images/201911/12/22724/nGzN7zBCvm.png!large)

