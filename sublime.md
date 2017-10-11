# Sublime Text 3

### 安装插件Package Control

点击顶部菜单的 View -&gt; Show Console（或者使用快捷键 command + \` ）。在下面的输入框里复制下面的代码

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```



