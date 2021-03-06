Linux外置硬盘加载方案
#####################
:date: 2012-07-17 16:20
:category: Technique
:tags: linux, mount, 
:slug: linux-usb-mount

对于有大容量外置硬盘的Linuxer而言，开机自动加载外置硬盘当然是很舒服的事情，尤其是外置硬盘常年不挪窝的情况。许多Linux发行版都有usb自动加载程序，不过相对手工加载而言速度较慢，所以开机时让系统直接加载外置硬盘而不是搜索usb硬盘再添加会更好一些，这可以通过修改/etc/fstab文件来实现。这个文件语法还是比较简单的，看着其它分区的示例就差不多了，当然也可以详细地参考Arch的\ `fstab
wiki`_\ 。简单地说就是现在/media目录下创建好要加载到的目标目录，然后在fstab中添加常连的外置硬盘mount条目即可。

这个方案是我最开始采用的，没有太大问题，但是还不完美。主要是最近我的外置硬盘接口似乎有点松动，所以用段时间后会自动掉线，这时系统又会自动搜索加载，麻烦在于自动加载的目录和我所设的目录不一致了，这样所有对该硬盘下文件的操作就会“找不到目标”。典型的例子就是用播放器播放外置硬盘的歌曲，掉线重连后播放器就找不到曲目，只能又去手动加载，十分费劲。

Linux下自动加载usb外置硬盘会mount到/media/$partition
label目录下（起码我在Arch和Linux
Mint下是如此），因此，你可以把手工设置的目录名称和外置硬盘分区的label修改成一致即可，这样就算掉线重连，文件位置不改变也就不会出现错误啦。想法是好的，不过可惜，如果系统检测到有同名的目录它就会创建一个带\_的一个新目录作为挂载点，这条路也行不通。（也许可以修改哪里的设置或者权限可以达到这个目的？）

目前只能不采用手动挂载而采用自动搜索挂载，这样其实也没太大的缺点，总比不断手动修改挂载点强。

另外外置硬盘分区的label可以用Gparted修改，先卸载要修改的硬盘，然后右键修改label，再应用这些修改即可。修改成一个简短好识别的id，固定下来以后就不会再有诸如此类的麻烦了。

.. raw:: html

   </p>

.. _fstab wiki: https://wiki.archlinux.org/index.php/Fstab
