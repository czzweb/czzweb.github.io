# 进入PHP的第一天

## 安装PHP

拉下一个后端仓库，无从下手。
拥有两台电脑： 
  1. Windows: 纯粹的前端环境，没有apache，没有php，没有composer，没有数据库...
  2. Mac: 很久运行过php项目（即前后端未分离的项目），有php, composer，自带apache，装过nginx，只是版本可能都比较老了。

  ### windows
  第一反应是要装php，那么问题来了，为啥写js的时候没说要装js呢？

    试着解释一下， Js是客户端语言，php是服务端语言。浏览器可以直接解析js，但php需要一个特定的环境，就和js需要浏览器一样？
    本来想就需要一个像php.exe的东西，现在又想的更明白了。不用装东西，用记事本也可以写出一个php文件，只是无法运行而已。所以才说记事本可以写一切语言吧。

  百度一下，其实是要装一个PHP的运行环境，即web服务器。
  三大主流web服务器：Apache，Nginx，IIS。

  搜 windows下php安装，看过去大部分是wamp，即Windows apache mysql php，可能apache认可的比较早。不管怎样，我就照步骤来了。参考https://segmentfault.com/a/1190000003409708。
  如果没有别人的步骤文档，单看官方下载页，对于一个英语很弱的人，各个版本，各个名称无从下手。所以依据别人选了ApacheHaus，对于这个Haus，不懂。

  #### 启动apache
  下载完解压缩就可以了。以管理员身份运行cmd，进入apache/bin下运行，httpd -k start。有报错： httpd.conf: ServerRoot must be a valid directory
  找到有ServerRoot那一行，更改路径
  ```
    Define SRVROOT "your apache path" 
    ServerRoot "${SRVROOT}"
  ```
  再次start。ok. 浏览器打开localhost会看到apache页，即apache/htdocs.index.html

  #### httpd.conf关于php的配置
    ```
      LoadModule php7_module "PATH/wamp/php/php7apache2_4.dll"
      PHPIniDir "PATH/wamp/php/php.ini"
      # 添加php类型支持
      AddType application/x-httpd-php .php
      # 修改首页文件类型支持
      <IfModule dir_module>
        DirectoryIndex index.html index.htm index.php
      </IfModule>
    ```

  #### 安装php
    进入php官方下载页，涉及几个概念
      1. x86与x64的区别

        这个拉出来讲是因为php安装完后重启apache报一大段\x.\x..\x... win32 \x..\x..的报错。也就是只看到有个win32，搜索了一圈，对我有用的答案就是PHP装成win32的版本了。对的，我装了x86。

        x86是32位，x64是64位。

        于是，较真的我又问会被对象打的问题：为啥x86是32位，x64是64位。
          引用网络解释
            英特尔出了划时代的8086之后，后来使用该架构出了80286、80386等等，这一系列CPU就称作x86。对于这种CPU架构的话，可以称作x86，正式一点称作IA-32（Intel Architecture 32-bit）。
            x64的话，指的是x86-64
        所以，略提一下，带86的不一定是32位处理器，只是这些带86的32位处理器比较出名。略略略。
      2. Non Thread Safe与Thread Safe

        TS(Thread Safe)，线性安全，一般在IIS以ISAPI方式加载选择此版本
        NTS(Non Thread Safe)，一般以fast cgi方式运行时选择此版本，性能更好
        Linux/Unix采用多进程工作方式，Windows采用多线程方式。
        好吧，略深奥，太晚，脑子思考不下去，下次再补吧。
        
    下载完后解压到php下，将php.ini-production拷贝一份成php.ini。将; extension_dir = "./"修改为extension_dir = "PATH/wamp/php/ext"，同时放开一些.dll的注释。
    在Apache\htdocs路径下新建x.php，添加<?php phpinfo(); ?>，浏览器访问localhost/x.php就能看到php页面。即成功。

    MySql暂时先不涉及，继续项目。
  
  #### composer
    以前公司项目是Laravel框架的项目，有印象用composer install。
    所以这次也习惯性composer install，但是有报错，虽然看上去像权限上的问题，但怕过去问出丑。所以稍微查看了下composer。
    感觉类似于node的npm包管理工具，但区别是，npm不存在权限问题。用了哪个镜像，该镜像下的所有的包都可以使用。但composer还需要包所link的git仓库的权限，感觉不大合理...
    加了好几个仓库的权限后composer install成功了。
    
  end.

  ### Mac
    Mac下没费多大力，该有的都有。唯一没权限前后端来看说要升级下composer,需要版本在1.5以上。composer self-update。





