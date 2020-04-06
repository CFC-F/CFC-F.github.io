# CFC-F.github.io
个人博客


## 代码提交
```
git init   //初始化 Git 仓库
git add .   //添加文件
git commit -m '提交说明'   //提交文件
git remote add origin  仓库地址       //如果出现错误：fatal: remote origin already exists      请先执行 git remote rm origin 命令，再执行次命令
git pull --rebase origin master       //(可选)命令进行合并操作即可
git  push origin  master             // 上传
```
## git分支管理
```
git branch (branchname)     //创建分支命令
git checkout (branchname)    //切换分支命令
git branch                    //列出分支基本命令
```
## hexo常用命令
```
hexo init                       //初始化站点，生成一个简单网站所需的各种文件
hexo generate == hexo g         //生效新增、修改、更新的文件
hexo server == hexo s           //启动本地网站，可在本地观察网站效果
-p 选项，指定服务器端口，默认为 4000
-i 选项，指定服务器 IP 地址，默认为 0.0.0.0
-s 选项，静态模式 ，仅提供 public 文件夹中的文件并禁用文件监视
hexo --debug                    //表示调试模式
hexo s --debug                   //以调试模式启动本地网站，在此模式下，对文件的更改
无需停止网站只需刷新即可看到效果，调试非常方便
hexo deploy == hexo d            //hexo的一键部署功能，执行此命令即可将网站发布到配置中的仓库地址。
hexo clean                        //命令用于清理缓存文件
hexo new <文章标题>                //命令用于新建文章，一般可以简写为 hexo n
```

## 删除
### 删除仓库
进入到我们需要删除的仓库里面，找到“settings”即仓库设置：
然后，在仓库设置里拉到最底部，找到“Danger Zone”即危险区域：
点击“Delete this repository”这样就可以删除该仓库了。
### 删除Github中的某个文件或文件夹
#### 本地仓库和远程仓库同时删除
先在本地把两个文件删除，然后执行以下命令：
```
git add *                   //把本地仓库的文件上传到缓存。
git commit -m 'del'         //把第一步上传到缓存的东西上传到本地仓库，其中'del'是操作标识，内容随便填，方便用户观看。
git push origin master     //把本地仓库的文件上传到远程仓库。
```
#### 只删除远程仓库，不删除本地仓库
```
git pull origin master //将远程仓库里面的项目拉下来。
dir 
git rm -r --cached 文件名称
git commit -m '提交说明'
git push -u origin master
```
