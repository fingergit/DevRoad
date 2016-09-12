# 随记

#### 2016/5/23 周一

- 配置使用ssh登录github，耗费1个半小时。
- svn提示时忽略某个文件或文件夹，耗费5分钟。
- 在调查ionic creator时，了解了iframe。
- 分析ionic creator网页，耗时5小时。参见[文档](../../../FingerWeb/blob/master/Doc/ionic_creator.md)
- 向github push时提示：bad file number，耗时40分钟。

#### 2016/5/24 周二
- 鼠标移到html元素上，元素缩放、改变图像的动画效果。(example/zoom-component)
- 学习angularJs的指令。
- 鼠标拖拽、获取子元素在div中的位置。


#### 2016/5/25 周三
- 根据angularjs官方教程进行系统学习（学习到第9节）

#### 2016/5/26 周四
- 根据angularjs官方教程进行系统学习（学习完）
- javascript学习

#### 2016/5/27 周五
- javascript学习

#### 2016/5/28 周日
- javascript学习

#### 2016/5/29 周日
- javascript学习
- 免费短信验证码接收网站: http://receive-sms-online.com/

#### 2016/5/30 周一
- 开发javascript splitter库

#### 2016/5/31 周二
- 完善splitter库
- UndoRedo Manager js

#### 2016/6/1 周三
- 学习[html2canvas](http://html2canvas.hertzen.com/)

#### 2016/6/9 周四 端午放假
- 个人生活

#### 2016/6/10 周五 端午放假
- 个人生活

#### 2016/6/11 周六 端午放假
- 个人生活

#### 2016/6/12 周日
- visual-app-creator项目属性面板各控件的创建指令。

#### 2016/6/13 周一
- visual-app-creator项目的widget拖拽、中间app frame的drop处理的探索。

#### 2016/6/14 周二
- 研究creator.ionic在web操作时数据的请求与接收处理。（ionic创建的一个app的项目结构）
- handlebarsjs库使用。 http://handlebarsjs.com/

#### 2016/6/22 周二
- 学习TypeScript

### 2016/9/8 周四
- CentOS下ionic2和android配置。

### 2016/9/9 周五
- 调查如何最小化ionic 2生成的js文件   
   方法：
   1. 对于ios和android，在build时添加`--release`参数：  
   ```
   ionic build android --release
   ```

   1. 对于serve，修改gulpfile.js文件：
   ```
gulp.task('watch', ['clean'], function(done){
  runSequence(
    ...
    function(){
      ...
      buildBrowserify({ watch: true }).on('end', done);
    }
  );
});

   ```
   改为：
   ```
gulp.task('watch', ['clean'], function(done){
  runSequence(
    ...
    function(){
      ...
      buildBrowserify({ 
        watch: true,
        minify:true,
        uglifyOptions: {
          mangle: false
        }
      }).on('end', done);
    }
  );
});

   ```

- 调查为什么ionic2的cutePuppyPics生成的www可以在iphone上预览，而ionic-preview-app-master的www不行。  
  原因：index.html中缺少一句：
  ```
  <!-- Polyfill needed for platforms without Promise and Collection support -->
  <script src="build/js/es6-shim.min.js"></script>
  ```
  加在`</ion-app>`之后

- VMWare安装OSX 10.11及xCode，在OSX编译ionic2
- php调用可执行程序。

### 2016/9/12 周一
- 调查如何使用QT启动ionic进行build。   
  可以通过如下方式：  
  ```
    QStringList cmdlist;
    // 参数1：ionic执行文件全路径。
    cmdlist.append("C:\\Users\\laj\\AppData\\Roaming\\npm\\node_modules\\ionic\\bin\\ionic");
    // 参数2：执行ionic的build命令。
    cmdlist.append("build");

    // 设置ionic build的代码的根目录
    QDir::setCurrent("F:\\temp\\vac-template");

    // 执行ionic build。
    QProcess mProcess;
    mProcess.execute("node", cmdlist);

  ```

- 调查如何通过vac-template.zip解压后的文件使用共同的node_modules文件夹，而不是每个vac-template项目都带有一个node_modules文件夹。  
  【!!!今日无解】      
  在使用代码生成vac-template项目后，其中需要通过yum install生成node_modules文件夹，这个生成时间非常长，且占用空间非常大。必须要找到使用共享node_modules文件夹的方法。

  https://segmentfault.com/a/1190000002478924

- node常用   
  - `npm root -g` 查看在系统nodejs全局的路径。
  - 设置全局路径:   

  ```
  # in *nix
  npm config set prefix /path/to/global

  # in windows
  npm config set prefix C:\\Users\\pc\\global
  ```

- 判断vac-template项目中有没有node_modules文件夹，没有则解压zip文件，生成此文件夹。