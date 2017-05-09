0、下载好gitbush之后安装，过程非常无脑，所以我做的非常快;    
1、进入到想要作为仓库的目录，比如test文件夹，输入git init，会在相应的目录之下（test文件夹下）生成.git文件（隐藏文件）。这样我们的git仓库就建好了呢！\^_^

2、在test文件目录下，随便先建一个什么东西，比如说test.txt，在输入git status，会看见红色的test.txt 也就是 untracked（没有被追踪）没有提交到git仓库中去呢！\^_^  
3、到现在具体的操作代码如下，关于一些错误的输入，要看清楚了呢！\^\_^
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard.png)  
4、此时已经添加到代码仓库中去了，提示还没有提交代码，当然可以移除这个缓存 git --cached filename  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard4.png)  
5、进行第一次提交，提示我没有告诉它我是谁？劳资是大帅比！记住了吗？
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard5.png)  
6、输入完成邮箱和用户名之后，再次提交，提交之后提示已经没有可以提交的了！  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard6.png)  
7、git log 查看提交的日志  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard7.png)  
8、分支：git branch查看当前分支  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard8.png)  
9、新建一个分支：git branch test，切换到分支，git checkout test    
合并两步变成一步：git checkout -b test1  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard9.png)  
10、合并分支 merge，首先要切换到master分支，然后从其他分支合并到主分支：  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard10.png)  ![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard101.png)  

11、卸磨杀驴 /_\，test1分支的代码已经合并到master分支了，想要删除：git branch -d test1 大写的D强制删除（如果test1的代码未提交的话），  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard11.png)  
12、补充！想要查看都修改了那些代码，可以使用git diff来查看：我只是加了一个回车而已。。。。  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard12.png)  
二、向GitHub提交代码 ：  
1、生成SSH key并添加到github：$ ssh-keygen -t rsa，虽然看不懂下面的英文，但是yes和no还是认识的 \^\_^  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard21.png)  

2、克隆github新建的项目 git clone git@github.com:o0o0oo00/test.git 选择clone with ssh；  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard22.png)  
3、克隆之后的项目就是一个自带了仓库的项目，不需要init，克隆之后将克隆下来的文件改点东西，然后  
git add .  
git commit -m "随便输入点什么，作为提交的注释"  
git push origin master  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard23.png)  
此时前往我的github上发现已经添加了新的内容哦！  
4、如果出现了这些不知道该怎么办的情况，那么不要慌张，看本帅的！  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard24.png)  
解决方法人家都告诉你了咩。。。。  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/clipboard241.png)  
总结一下，在公司链接上我的github：我一开始想直接clone可以不  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE242.png)  
这里说，，，，第一个danci就不认识，反正看见rsa就想起来，我的github上需要配置本机的RSA，然后去配置：、  
第一步：点击头像，点击setting  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE243.png)  
第二步：点击添加ssh key  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE244.png)  
第三步：   
完事了……^_^  
然后回去clone，发现成功了呢！  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE31.png)    
进入到test目录：随便改点东西。。  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE32.png)  

关于最后的哪个FBI warning 不用管它吧！好像只有第一次的时候会出现：  
![image](https://raw.githubusercontent.com/o0o0oo00/test/master/%E6%88%AA%E5%9B%BE33.png)

写的不好的地方一定要告诉我！哦内噶依稀马斯!   
本文链接：http://blog.csdn.net/technologyc/article/details/71427354  
BGM： Heaven  ^_^ http://music.163.com/#/m/song?id=29808787&userid=362969461  
阿里嘎头：stromzhang;