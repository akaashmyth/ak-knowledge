## 文件目录结构

 	
<table>
	<tbody>
		<tr>
			<td valign="top"><span>&nbsp;</span></td>
			<td valign="top">
			<p><span>可分享的(shareable)</span></p>
			</td>
			<td valign="top">
			<p><span>不可分享的(unshareable)</span></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" valign="top">
			<p><span>不变的(static)</span></p>
			</td>
			<td valign="top">
			<p><span>/usr (软件放置处)</span></p>
			</td>
			<td valign="top">
			<p><span>/etc (配置文件)</span></p>
			</td>
		</tr>
		<tr>
			<td valign="top">
			<p><span>/opt (第三方协力软件)</span></p>
			</td>
			<td width="5" valign="top">
			<p><span>/boot (开机与核心档)</span></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" valign="top">
			<p><span>可变动的(variable)</span></p>
			</td>
			<td valign="top">
			<p><span>/var/mail (使用者邮件信箱)</span></p>
			</td>
			<td valign="top">
			<p><span>/var/run (程序相关)</span></p>
			</td>
		</tr>
		<tr>
			<td valign="top">
			<p><span>/var/spool/news (新闻组)</span></p>
			</td>
			<td valign="top">
			<p><span>/var/lock (程序相关)</span></p>
			</td>
		</tr>
	</tbody>
</table>






| 目录    | 应放置档案内容 |
| --------|:-----:|
| /bin | 系统有很多放置执行档的目录，但/bin比较特殊。因为/bin放置的是在单人维护模式下还能够被操作的指令。在/bin底下的指令可以被root与一般帐号所使用，主要有：cat,chmod(修改权限), chown, date, mv, mkdir, cp, bash等等常用的指令。 |
| /boot|主要放置开机会使用到的档案，包括Linux核心档案以及开机选单与开机所需设定档等等。Linux kernel常用的档名为：vmlinuz ，如果使用的是grub这个开机管理程式，则还会存在/boot/grub/这个目录。|
|/dev|在Linux系统上，任何装置与周边设备都是以档案的型态存在于这个目录当中。 只要通过存取这个目录下的某个档案，就等于存取某个装置。比要重要的档案有/dev/null, /dev/zero, /dev/tty , /dev/lp*, / dev/hd*, /dev/sd*等等|
|/etc|系统主要的设定档几乎都放置在这个目录内，例如人员的帐号密码档、各种服务的启始档等等。 一般来说，这个目录下的各档案属性是可以让一般使用者查阅的，但是只有root有权力修改。 FHS建议不要放置可执行档(binary)在这个目录中。 比较重要的档案有：/etc/inittab, /etc/init.d/, /etc/modprobe.conf, /etc/X11/, /etc/fstab, /etc/sysconfig/等等。 另外，其下重要的目录有：/etc/init.d/ ：所有服务的预设启动script都是放在这里的，例如要启动或者关闭iptables的话： /etc/init.d/iptables start、/etc/init.d/ iptables stop|
|/etc/xinetd.d/ |这就是所谓的super daemon管理的各项服务的设定档目录。|
|/etc/X11/|与X Window有关的各种设定档都在这里，尤其是xorg.conf或XF86Config这两个X Server的设定档。|
|/home|这是系统预设的使用者家目录(home directory)。 在你新增一个一般使用者帐号时，预设的使用者家目录都会规范到这里来。比较重要的是，家目录有两种代号：~ ：代表当前使用者的家目录，而 ~guest：则代表用户名为guest的家目录。|
|/lib|系统的函式库非常的多，而/lib放置的则是在开机时会用到的函式库，以及在/bin或/sbin底下的指令会呼叫的函式库而已 。 什么是函式库呢？妳可以将他想成是外挂，某些指令必须要有这些外挂才能够顺利完成程式的执行之意。 尤其重要的是/lib/modules/这个目录，因为该目录会放置核心相关的模组(驱动程式)。|
|/media|media是媒体的英文，顾名思义，这个/media底下放置的就是可移除的装置。 包括软碟、光碟、DVD等等装置都暂时挂载于此。 常见的档名有：/media/floppy, /media/cdrom等等。|
|/mnt|如果妳想要暂时挂载某些额外的装置，一般建议妳可以放置到这个目录中。在古早时候，这个目录的用途与/media相同啦。 只是有了/media之后，这个目录就用来暂时挂载用了。|
|/opt|这个是给第三方协力软体放置的目录 。 什么是第三方协力软体啊？举例来说，KDE这个桌面管理系统是一个独立的计画，不过他可以安装到Linux系统中，因此KDE的软体就建议放置到此目录下了。 另外，如果妳想要自行安装额外的软体(非原本的distribution提供的)，那么也能够将你的软体安装到这里来。 不过，以前的Linux系统中，我们还是习惯放置在/usr/local目录下。|
|/root|系统管理员(root)的家目录。 之所以放在这里，是因为如果进入单人维护模式而仅挂载根目录时，该目录就能够拥有root的家目录，所以我们会希望root的家目录与根目录放置在同一个分区中。|
|/sbin|Linux有非常多指令是用来设定系统环境的，这些指令只有root才能够利用来设定系统，其他使用者最多只能用来查询而已。放在/sbin底下的为开机过程中所需要的，里面包括了开机、修复、还原系统所需要的指令。至于某些伺服器软体程式，一般则放置到/usr/sbin/当中。至于本机自行安装的软体所产生的系统执行档(system binary)，则放置到/usr/local/sbin/当中了。常见的指令包括：fdisk, fsck, ifconfig, init, mkfs等等。|
|/srv|srv可以视为service的缩写，是一些网路服务启动之后，这些服务所需要取用的资料目录。 常见的服务例如WWW, FTP等等。 举例来说，WWW伺服器需要的网页资料就可以放置在/srv/www/里面。呵呵，看来平时我们编写的代码应该放到这里了。|
|/tmp|这是让一般使用者或者是正在执行的程序暂时放置档案的地方。这个目录是任何人都能够存取的，所以你需要定期的清理一下。当然，重要资料不可放置在此目录啊。 因为FHS甚至建议在开机时，应该要将/tmp下的资料都删除。|


























