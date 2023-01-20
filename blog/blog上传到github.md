# Git版本控制

控制Hexo版本，以防出现太多bug，无法修复，可以回溯到原来的版本

~~~
git init
git add .
git commit -m "2022-08-23 13：40：00"
git branch -M main
git remote rm origin  # 首次不用执行这个
git remote add origin https://github.com/kongshier/kongshier.github.io.git  # 指定GitHub 的版本仓库
git push -u origin main
~~~

# 发布到远程访问

在博客的根目录下 打开git bash

~~~bash
npm install hexo-deployer-git --save
hexo g
hexo d
--更新
npm update hexo-theme-butterfly
~~~



# 新疆分支



1、git branch                   // 查看当前分支情况

2、git branch test           // 新建一个分支test

3、git checkout test         // 切换到新建的分支test

4、git push origin test  或者 git push origin test:test           // 将新建分支test推送到GitHub上







# 发布到互联网



```bash
在博客根目录下打开 git bash hare

输入 

hexo g

git config --global user.name "kongshier"
git config --global user.email "2927527234@qq.com"

hexo d
```

