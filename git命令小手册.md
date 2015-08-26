# git命令&知识点

- 寻求帮助

```
git help <verb>
git <verb>  --help
```

- git add<br>这是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等
- git diff 显示还没有暂存起来的改动，而不是这次工作和上次提交之间的差异.若要看已经暂存起来的文件和上次提交时的快照之间的差异，可以用 git diff --cached 命令
- git commit -m '' /- a 可以跳过暂存
- git rm -f 如果删除文件之前修改过并且已经放到暂存区域的话，必须使用强制删除选项-f
- git mv A B 进行重命名操作想大于执行以下三条指令

```
mv A B
git rm A
git add B
```
- git log 会按提交时间列出所有更新 
	- -p显示提交更新的差异
	- --stat 仅显示叫要的增改行数统计
	- --pretty 展示不同格式的提交历史
		- --pretty=format:"XXXXX",XXX格式控制字符串
		
		<table class="ref"><thead>
<tr>
<th>选项</th>
<th>说明</th>
</tr>
</thead><tbody>
<tr>
<td><code>%H</code></td>
<td>提交对象（commit）的完整哈希字串</td>
</tr>
<tr>
<td><code>%h</code></td>
<td>提交对象的简短哈希字串</td>
</tr>
<tr>
<td><code>%T</code></td>
<td>树对象（tree）的完整哈希字串</td>
</tr>
<tr>
<td><code>%t</code></td>
<td>树对象的简短哈希字串</td>
</tr>
<tr>
<td><code>%P</code></td>
<td>父对象（parent）的完整哈希字串</td>
</tr>
<tr>
<td><code>%p</code></td>
<td>父对象的简短哈希字串</td>
</tr>
<tr>
<td><code>%an</code></td>
<td>作者（author）的名字</td>
</tr>
<tr>
<td><code>%ae</code></td>
<td>作者的电子邮件地址</td>
</tr>
<tr>
<td><code>%ad</code></td>
<td>作者修订日期（可以用 -date= 选项定制格式）</td>
</tr>
<tr>
<td><code>%ar</code></td>
<td>作者修订日期，按多久以前的方式显示</td>
</tr>
<tr>
<td><code>%cn</code></td>
<td>提交者(committer)的名字</td>
</tr>
<tr>
<td><code>%ce</code></td>
<td>提交者的电子邮件地址</td>
</tr>
<tr>
<td><code>%cd</code></td>
<td>提交日期</td>
</tr>
<tr>
<td><code>%cr</code></td>
<td>提交日期，按多久以前的方式显示</td>
</tr>
<tr>
<td><code>%s</code></td>
<td>提交说明</td>
</tr>
</tbody></table>		

- 修改最后一次提交 git commit --amend
- 取消已经暂存的文件 git reset HEAD <file>
- 恢复已修改 git checkout <file>
- 从远程仓库拉取git fetch XX，注意fetch命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支
- git pull命令可以将远端数据拉大本地仓库并合并到当前分支
- git push origin master 将master分支提交推送到origin上
- git tag 将任意时间的版本打标签
- git中的分支其实本质上仅仅是个指向commit对象的可变指针
- git checkout <branch-name> 切换分支，git branch新建分支并不会自动切换 你可以使用git checkout -b branchname，那样便会新建并切换到分支运行
- 分支快进 fast forward
- 跟踪远程分支 git checkout -b branchname orign/branchname
- 删除远程分支 git push remote [空格]:remote-branch name
- rebase 
	
	![](http://git-scm.com/figures/18333fig0331-tn.png)
	
	![](http://git-scm.com/figures/18333fig0332-tn.png)
	
	![](http://git-scm.com/figures/18333fig0333-tn.png)
	![](http://git-scm.com/figures/18333fig0334-tn.png)
	![](http://git-scm.com/figures/18333fig0335-tn.png)
	
- **一旦分支中的提交对象发布到公共仓库，就不要对其做rebase操作**