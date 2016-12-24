### 更新
meteor update --all-packages

### Defining views with React Components
```
meteor npm install --save react react-dom
### router
meteor npm install --save react-router
```

### i18n
meteor add universe:i18n

### schema
meteor add aldeed:simple-schema

### 用户
meteor add accounts-ui accounts-password

### 安全之发布与订阅
meteor remove insecure

meteor remove autopublish

meteor npm install --save classnames

### Testing
Mocha JavaScript test framework:
``` 
meteor add practicalmeteor:mocha
meteor test --driver-package practicalmeteor:mocha
```
输入上面的命令后，可用看到一个空的测试结果浏览窗.

