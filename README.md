使用http代理加速下载游戏BAR的地图，这个办法适用linux系统。它是否适用windows系统？请往下读自行判断。

# windows系统
在BAR游戏中，当需要下载地图的时候，就会调用launcher的bin/pr-downloader进程。我估计这个文件在windows系统中会有一个.exe后缀。

在linux系统中，我们可以用一个可执行bash脚本或者python脚本替换掉pr-downloader这个可执行的二进制文件，然后在这个脚本中插入我们自己的代码，即用http代理加速地图下载。

我不知道在windows系统中，插入一个同名不同后缀的bat文件能不能起到一样的效果，来帮我们插入自己的代码。如果能做到这一点，这个办法就是可行的。

# 安装
1. 在linux系统中，找到BAR的launcher中的bin/pr-downloader，把它重命名为bin/pr-downloader-old。
2. 然后把这个repo中的pr-downloader下载，放到bin/目录中，要用chmod +x 赋予它可执行权限。
3. 然后用文本文件打开pr-downloader，修改其中的proxy, path_maps, pr_old 三个变量

proxy是你自己本地使用的http代理。

path_maps的默认地址是：/home/你的用户名/.local/state/Beyond All Reason/maps，检查确认下你有这个目录。

pr_old设置为 launcer/bin/pr-downloader-old 目录，因为原本的pr-downloader除了下载地图还有其他指责，当我们的脚本发现BAR调用的时候不是为了下载地图，就需要调用原本的pr-downloader进程。


