# Explorer Patcher R

本意是想通过[win11-toggle-rounded-corners](https://github.com/rich-ayr/win11-toggle-rounded-corners)项目修复Explorer Patcher失效的禁用圆角功能 后续开发中发现其依赖的ep_dwm项目和win11-toggle-rounded-corners其实都是通过注入任务管理器实现的, 持久化都是通过注册服务实现的. Explorer Patcher自身是没有直接在任务管理器重启后立刻注入的事件监听(可能是我没找到), 所以把win11-toggle-rounded-corners塞到Explorer Patcher的行为本身意义不大.  

因此我把项目中原有的ep_dwm和相关的注册行为去掉了(顺便让那个圆角选项能动了), 额外安装win11-toggle-rounded-corners可以获得同样的效果.  

顺便一提, win11-toggle-rounded-corners是用cpp写的, 直接依赖zydis而且是meson项目, 多字符集. Explorer patcher是拿大量用c而且是Unicode字符集, 移植的难度有点大(怒).  

# 一些编译的注意事项
zydis的头文件原始文件和构建之后输出文件是不一样的, 可能会有缺少符号定义的情况在  
funchook和zlib需要自己动手编译  
funchook默认/MTd 需要把ExplorerPatcher也改成/MTd进行编译 不然会有库冲突  