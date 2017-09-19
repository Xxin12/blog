---
layout: post
title: "在win10下使用Jekyll通过gtihub pages免费搭建自己的博客"
date: 2017-09-19
description: "Jekyll-github-pages"
tag: jekyll,win10
---  


### win10下安装Jekyll环境及可能遇到的问题

  前天因为系统重装了一下，前面一个周末搞明白才弄好的jekyll环境也没了，现在乘着重新搭建环境顺便写个博客，梳理下自己搭建时候遇到的一些问题和解决方法，和搭建环境的完整过程。  

### 安装环境  

#### 1. 下载 railsinstaller  

  在win10系统下需要下载railsinstaller安装后才行，到[本此面去下载](http://railsinstaller.org/en)  

#### 2. 安装  

  建议安装时候用默认路径  

#### 3. 更新gem  

  首先更换国内的RubyGems镜像源  
```ruby
$ gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l
https://gems.ruby-china.org
# 确保只有 gems.ruby-china.org
```  
然后进行更新gem
```
$ gem update
```  
会出现一个错误，提示ruby版本过低
我们就要去下载安装新版ruby[下载地址点我](https://rubyinstaller.org/downloads/)  

默认安装位置安装完成  

会有一个命令窗弹出，如果不知道怎么选择的话按回车就行了  

安装完成后输入下面命令，检查版本信息查看是否完成更新
```
$ ruby -v
```  

ruby更新完成后我们开始更新gem  
```
$ gem update
```    

中途会有两个需要确认信息，输入y之后回车即可  

可能会遇到某个更新包损坏情况，通过提示路径找到删除掉重新输入更新命令更新即可

更新结束后输入命令查看是否更新了新版本
```
$ gem -v
```   

4.安装jekyll  

输入命令进行安装  
```
$ gem install jekyll
```   

安装完成后查看版本信息  
```
$ jekyll -v
```   

#### 5.新建博客  
环境安装完成后开始在本地生成一个博客  

```
$ jekyll new myblog 
```  
这时候我们可能会出现一个错误  

```
  Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.5.2 | Error:  bundler
```   
这里说我们一个bundler损坏了，我们需要重新下载安装  
```
$ gem install bundler
```    

安装完成后我们重复之前的生成博客命令  
可能还会遇到一个问题，输入命令后卡在了生成过程中，我们键盘快捷键`CTRL+C`结束生成，会出现一堆可能看不懂的信息  

输入命令  
```
$ jekyll serve
```   
会出现以下信息  
```
C:/Ruby22-x64/lib/ruby/gems/2.2.0/gems/bundler-1.12.5/lib/bundler/resolver.rb:35     6:in `block in verify_gemfile_dependencies_are_found!': Could not find gem 'mini     ma x64-mingw32' in any of the gem sources listed in your Gemfile or available on      this machine. (Bundler::GemNotFound)
```    
这里的主要信息是提示没有`(Bundler::GemNotFound)`
回到上级目录重新安装  
```
$ bundle install
会提示我们 Could not locate Gemfile
```    
我们需要进入博客根目录然后再执行安装命令

#### 6.生成博客本地查看

安装完成后我们再次生成一个博客 ,过程应该不会太长，一分钟左右 
```
jekyll new blog
Running bundle install in c:/Sites/blog...
  Bundler: The latest bundler is 1.16.0.pre.2, but you are currently running 1.15.4.
  Bundler: To update, run `gem install bundler --pre`
  Bundler: Fetching gem metadata from https://rubygems.org/............
  Bundler: Fetching version metadata from https://rubygems.org/...
  Bundler: Fetching dependency metadata from https://rubygems.org/..
  Bundler: Resolving dependencies...
  Bundler: Using public_suffix 3.0.0
  Bundler: Using bundler 1.15.4
  Bundler: Using colorator 1.1.0
  Bundler: Using ffi 1.9.18 (x64-mingw32)
  Bundler: Using forwardable-extended 2.6.0
  Bundler: Using rb-fsevent 0.10.2
  Bundler: Using kramdown 1.15.0
  Bundler: Using liquid 4.0.0
  Bundler: Using mercenary 0.3.6
  Bundler: Using rouge 1.11.1
  Bundler: Using safe_yaml 1.0.4
  Bundler: Using thread_safe 0.3.6
  Bundler: Using addressable 2.5.2
  Bundler: Using rb-inotify 0.9.10
  Bundler: Using pathutil 0.14.0
  Bundler: Using tzinfo 1.2.3
  Bundler: Using sass-listen 4.0.0
  Bundler: Using listen 3.0.8
  Bundler: Using tzinfo-data 1.2017.2
  Bundler: Using sass 3.5.1
  Bundler: Using jekyll-watch 1.5.0
  Bundler: Using jekyll-sass-converter 1.5.0
  Bundler: Using jekyll 3.5.2
  Bundler: Using jekyll-feed 0.9.2
  Bundler: Using minima 2.1.1
  Bundler: Bundle complete! 4 Gemfile dependencies, 25 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in c:/Sites/blog.
```  
生成完成后我们进入博客目录  
```
$ cd blog
$ jekyll serve
Configuration file: c:/Sites/blog/_config.yml
            Source: c:/Sites/blog
       Destination: c:/Sites/blog/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.829 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'c:/Sites/blog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```    

这时候我们的博客生成全部完成我们可以在浏览器输入`http://127.0.0.1:4000/` 查看生成结果   

这时候我们的所有博客生成环境就完成了安装 


#### 7. 使用模板生成自己的博客
我们并不需要自己写一个博客因为有很多优秀的博客模板可以直接使用，我们只需要稍加修改就可以用上了  

这里有个网站，收集了许多优秀的模板大家可以自己找到自己喜欢的进行修改使用 `http://jekyllthemes.org/`

这里我使用了`https://github.com/leopardpan/leopardpan.github.io/`  
这个模板，同时参考了视频`http://www.bilibili.com/video/av13994132`  

使用模板时下载原模板文件解压后拖到生成博客的目录下，进行一次本地启动生成服务，也就是执行`$ jekyll serve`命令  

初次生成可能会再次出现一个问题  
```
$ jekyll serve
Configuration file: c:/Sites/blog/_config.yml
       Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
  Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.5.2 | Error:  jekyll-paginate
```   

通过报错的信息我回到`Sites`目录执行命令安装  
```
$ gem install jekyll-paginate
```  
 
安装完成后我们再次进入博客根目录启动服务   
这时候可能还会报错   

我们需要在配置文件_config.yml添加一行： 
```
gems: [jekyll-paginate]
```   
保存后重新启动一次服务  
就可以看到博客模板已经成功的启动了，我们可以根据自己的需求修改模板的东西，最后完成自己的博客生成   

最后一步就是在gtihub pages上部署了  

这里我放到下一篇再写，这篇主要就是在win10系统下搭建jekyll需要的环境以及可能会遇到的问题，有些地方写的可能不是非常明白，可以留言等我补充=.=


本次博客参考了以下文章和网页内容  
>http://pwnny.cn/original/2016/06/26/MakeBlog.html#NativeBuild  
>http://www.jianshu.com/p/12e7e1f8007e  
>https://gems.ruby-china.org/  
>http://blog.csdn.net/moonclearner/article/details/52238033  
>http://jekyll.com.cn/  
>http://www.bilibili.com/video/av13994132  
>https://github.com/leopardpan/leopardpan.github.io  
>https://teamtreehouse.com/community/jekyllpaginate-gem
