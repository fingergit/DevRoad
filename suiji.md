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

### 2016/9/15 周四   
### 2016/9/16 周五   
### 2016/9/17 周六   
- 中秋放假

### 2016/9/18 周日
- visual-app-creator更新为angular2.0正式版
- 更新过程中的坑：
  1. npm start过程中出现错误：   
     ```
     Variable '$' must be of type 'JQueryStatic', but here has type 'cssSelectorHelper'
     ```

     原因：JQuery与angular-protractor冲突。
     临时解决方法：将`typings\globals\angular-protractor\index.d.ts`中`declare var $: cssSelectorHelper;`行注释掉。

  1. 拖拽控件到编辑区时，无法Drop。   
     原因：edit-panel.component.ts中，`if (this.appFrame.hasOwnProperty('attachEvent'))`进不去，`this.actionService.platformChanged`中，进入initFrame时，appFrame.contentDocument属性不存在。

     解决方法：无需修改，在apache服务器下是正常的，只是npm start时，会不正确。

  1. QT调用ionic build时，如何将ionic的命令行输出输出到指定的文件中？
     启用QProcess.start代替execute，并调用mProcess.waitForFinished();等待结束，然后   
     ```
    QByteArray qba = mProcess.readAllStandardOutput();
    char* myChar = new char[qba.length()];
    for (int i = 0; i < qba.length(); i++)
    {
      myChar[i] = qba[i];
    }
    string str2 = string(myChar);
    delete[] myChar;
    wprintf(L"----\n");
    wprintf(L"%s\n", QString::fromLocal8Bit(qba).toStdWString().c_str());
     ```     
     
  1. 如何使用QT的Log类？
     
### 2016/9/20 周二
- How to add conditional attribute in Angular 2?   
  http://stackoverflow.com/questions/36745734/how-to-add-conditional-attribute-in-angular-2

- Can't bind to 'vac-page-type' since it isn't a known property of 'button'.   
  使用`<div [attr.vac-page-type]="EVacProjectPageType.NORMAL"></div>`代替`<div vac-page-type="{{EVacProjectPageType.NORMAL}}"></div>`。

- angular2，如何设置一个DOM element的style？   
  `<div [style.background-color]="blackColor">`
  其中，blackColor为component中的变量。

  如果想直接赋值，需加单引号。   
  ```<div [style.background-color]="'red'">```
  
### 2016/9/23 周五
- ionicframework使用的angular已更新为2.0正式版，下载编译。(还有问题未解决。)   
  问题：npm install ionic时，提示：`no such file or directory, rename 'C:\Users\laj\AppData\Roaming\npm\node_modules\.staging\ansi-5ceb118d'`   
  解决方法：将C:\Users\laj\AppData\Roaming\npm\node_modules下的ionic文件夹删除，重新执行。

- 在modal中使用component组件。component组件通过EventEmitter向modal调用者发送消息。   
  component中：
   ```
   @Component(
   export class IonicIconsComponent implements OnInit{
       @Output() iconSelected: EventEmitter<any> = new EventEmitter(false);

       onSelect(item:string){
        this.iconSelected.emit(item);
      }
    }
  ```
  
  modal调用者中：   
  ```
  <button type="button" class="btn btn-sm btn-default btn-select-icon " title="..." (click)="iconModal.open()">...
  </button>
  <modal #iconModal>
      <modal-header [show-close]="true">
          <h4 class="modal-title">Select icon</h4>
      </modal-header>
      <modal-body>
          <vac-ionic-icons (iconSelected)="iconSelect($event)"></vac-ionic-icons>
      </modal-body>
      <modal-footer [show-default-buttons]="true"></modal-footer>
  </modal>
  ```
  ```
  export class IconItemComponent implements OnInit{
      @ViewChild('iconModal')
      iconModal: ModalComponent;

      iconSelect(icon:string){
          this._selectIcon(icon);
          this.iconModal.close();
      }
  }
  ```
  