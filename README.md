# 1.介绍

- sass 官网

  英文官网：https://sasscss.org/

  中文官网：https://www.sass.hk/
  sass --watch sass:css --style expanded

- sass 特性

  Sass是世界上最成熟，最稳定，最强大的专业级  CSS扩展语言。

  **CSS  兼容**

  Sass与所有版本的CSS完全兼容。我们认真对待这种兼容性，以便您可以无缝地使用任何可用的CSS  库。

- sass 安装

  https://www.sass.hk/install/

# 2.常用命令

## 2.1安装配置命令

ruby安装完成后需测试安装有没有成功,运行`CMD`输入以下命令：

```ruby
ruby -v
//如安装成功会打印
ruby 2.2.2p95 (2015-04-13 revision 50295) [i386-mingw32]
```

如上已经安装成功。但因为国内网络的问题导致`gem`源间歇性中断因此我们需要更换`gem`源。（使用淘宝的gem源https://ruby.taobao.org/）如下：

```ruby
//1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内淘宝源
//(已失效)gem sources -a https://ruby.taobao.org/
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://ruby.taobao.org/
```

`Ruby`自带一个叫做`RubyGems`的系统，用来安装基于`Ruby`的软件。我们可以使用这个系统来 轻松地安装`Sass`和`Compass`。要安装最新版本的`Sass`和`Compass`，你需要输入下面的命令：

```ruby
//安装如下(如mac安装遇到权限问题需加 sudo gem install sass)
gem install sass
gem install compass
```

在每一个安装过程中，你都会看到如下输出：

```
Fetching: sass-3.x.x.gem (100%)
Successfully installed sass-3.x.x
Parsing documentation for sass-3.x.x
Installing ri documentation for sass-3.x.x
Done installing documentation for sass after 6 secon
1 gem installed
```

安装完成之后，你应该通过运行下面的命令来确认应用已经正确地安装到了电脑中：

```
sass -v
Sass 3.x.x (Selective Steve)

compass -v
Compass 1.x.x (Polaris)
Copyright (c) 2008-2015 Chris Eppstein
Released under the MIT License.
Compass is charityware.
Please make a tax deductable donation for a worthy cause: http://umdf.org/compass
```

如下sass常用更新、查看版本、sass命令帮助等命令：

```
//更新sass
gem update sass

//查看sass版本
sass -v

//查看sass帮助
sass -h
```



`sass`编译有很多种方式，如命令行编译模式、sublime插件`SASS-Build`、编译软件`koala`、前端自动化软件`codekit`、Grunt打造前端自动化工作流`grunt-sass`、Gulp打造前端自动化工作流`gulp-ruby-sass`等。

## 2.2命令行编译

```
//单文件转换命令
sass input.scss output.css

//单文件监听命令
sass --watch input.scss:output.css

//如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
```

### 2.2.1 命令行编译配置选项

命令行编译`sass`有配置选项，如编译过后css排版、生成调试map、开启debug信息等，可通过使用命令`sass -v`查看详细。我们一般常用两种`--style``--sourcemap`。

```
//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info
```

- `--style`表示解析后的`css`是什么排版格式;
  sass内置有四种编译格式:`nested``expanded``compact``compressed`。
- `--sourcemap`表示开启`sourcemap`调试。开启`sourcemap`调试后，会生成一个后缀名为`.css.map`文件。

### 2.2.2 四种编译排版演示

```
//未编译样式
.box {
  width: 300px;
  height: 400px;
  &-title {
    height: 30px;
    line-height: 30px;
  }
}
```

### nested 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style nested

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px; }
  .box-title {
    height: 30px;
    line-height: 30px; }
```

### expanded 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style expanded

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px;
}
.box-title {
  height: 30px;
  line-height: 30px;
}
```

### compact 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compact

/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
```

### compressed 编译排版格式

```
/*命令行内容*/
sass style.scss:style.css --style compressed

/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
```

# 3.编译过程中出错

3.1编译的命令语句：命令行输入：    sass  装有scss的文件名/你想要编译的scss文件名  **:**  你的css文件夹名/想要把scss编译后的内容放入的某css文件名字

> 如：sass sass1/style.scss:css1/style.css
>
> 编译后出现以下错误
>
> Errno::ENOENT: No such file or directory @ rb_sysopen - sass1/style.scss
> Use --trace for backtrace.
>
> 原因：你的编译时文件名输入错误，也就是命令行拼写错误

3.2不用每次都进行编译，使用watch进行监视文件夹是否有变化，自动进行编译

> sass --watch  放scsass --watchss的文件夹名：放css的文件夹名
>
> 例如，sass --watch sass :css 
>
> 停止监视  Ctrl+c

# 3.官方文档

- ### 入门文档：https://www.sass.hk/guide/

- ### 标准文档：https://www.sass.hk/docs/