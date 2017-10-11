idea编辑快捷键

1、alt+enter 自动导入包

2、shit+command+u 自动切换大小写

3、command+f12 显示当前文件结构

4、command+alt+r 运行

5、command+shit+向上，向下 （选中行上移或者下移）

6、command+alt+左键 进入实现类

7、command+e 查找最近使用过的类

8、command+shift+o 按照文件名查找文件

编辑快捷键，keymap中查找cyclic，去除Alt+斜杠，查找basic，添加上。

调试快捷键

单步调试

1、f8 （step over）

程序向下执行一行（如果当前行有方法调用，这个方法将被执行完毕返回，然后到下一行）

2、f7 （step into）

程序向下执行一行。如果该行有自定义方法，则运行进入自定义方法（不会进入官方类库的方法）

3、shift+alt+f7（Force step into）

该按钮在调试的时候能进入任何方法

4、shift+f8 （step out）

如果在调试的时候你进入了一个方法\(如f2\(\)\)，并觉得该方法没有问题，你就可以使用stepout跳出该方法，返回到该方法被调用处的下一行语句。值得注意的是，该方法已执行完毕。

5、command+alt+r （跳到下个断点）

程序将运行一个断点到下一个断点之间需要执行的代码。如果后面代码没有断点，再次点击该按钮将会执行完程序。

6、shit+command+f8（查看断点）

可以查看你曾经设置过的断点并可设置断点的一些属性

