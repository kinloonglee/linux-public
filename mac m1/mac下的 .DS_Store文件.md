# Mac中Git忽略.DS Store文件
## Git中多出来的.DS Store
由于我是第一次使用mac，发现每次git上传时会多出来.DS_Store文件，虽然不清楚具体做什么，但看上去并没什么问题。git一般也是自己一个人单机使用，就算换机也一般是直接换，没有遇到过两个同时使用的时候，上传.DS_Store-也就默认都上传了。
但最近用两个mac工作，就发现了问题，一个mac提交了修改，第二个mac想要拉下来时居然遇到了.DS_Store文件被修改过需要提交再merge。所以这个.DS_Store是什么鬼？
# .DS Store	

.DS Store文件，是用于存放目录自定义属性（如图表、位置属性）等元数据信息的系统文件，由Finder自动创建。虽然所有.开头的文件/文件夹默认隐藏（可以使用`Command+Shift+.`显示所有隐藏文件），平时我们看不见，也不影响使用，但是Gt仍会将其记录下来，即便我只是在同目录下移动文件。所以为了防止某些信息不经意间泄露出来，建议使用某些手段使Git忽略`.DS Store`文件。

## Git中处理方案

### 方案一：项目设置.gitignore

仅针对git的处理最先想到就是设置.gitignore文件。
.gitignore文件用于忽略文件，规范如下:

- 所有空行或者以注释符号#开头的行都会被Gt忽略

- 可以使用标准的gob模式匹配

- 匹配模式最后跟反斜杠（/）说明要忽略的是目录

- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（！）取反

- 第一个`/`会匹配路径的根目录，举个栗子，"/**.htm"会匹配"index.htm"，而不是"d/index.htm"。*

- *通配符*`*`匹配任意个任意字符,`?`匹配一个任意字符。需要注意的是通配符不会匹配文件路径中的/，举个栗子，” d/*.html"会匹配"d/index.htm"，但不会匹配"d/a/b/c/index.html"。

- 两个连续的星号

- 有特殊含义：

  - 以`**/` 开头表示匹配所有的文件夹，例如`**/test.md`匹配所有的test.md文件

  - 以`/**`结尾表示匹配文件夹内所有内容，例如`a/**`匹配文件夹a中所有内容。

  - 连续星号`**`前后分别被/夹住表示匹配0或者多层文件夹，例如`a/**/b`匹配到a/b、a/x/b、a/x/y/b等。

  - 前缀！的模式表示如果前面匹配到被忽略，则重新添加回来。如果匹配到的父文件夹还是忽略状态，该文件还是保持忽略状态。如果路径名第一个字符为！，则需要在前面增加\进行转义。

  - 对于一些常用的系统、工程文件的gitignore文件可以参考这个网站进行设置，这里有很多模板。
    针对.DS_Store文件，在git工程文件夹中新建`.gitignore`文件，在文件中设置：

    ```
    .DS_Store 
    **/.DS_Store
    .DS_Store？
      
    ```

    选择语言
    对于已经提交的内容，希望git能够忽略，但同时并不会删除本地文件，需要在控制台输入以下命令：
    `git rm -r --cached $file_path`

    比如 `git rm -r --cached .`

    

    ### 方案二：全局设置忽略
    虽然每个项目配.gitignore文件可以成功，但是每个项目都需要配置就有点烦了。我们可以在git的全局进行配置来忽略.DS_Store文件。

    设置之前我们先看下现在的git configi配置情况
    ```git config --list```
    实际上git配置情况可以在`~/.gitconfig`文件中查看。
    ```vi ~/.gitconfig```

    通过`：q！`退出后，我们需要建立一个文件，把需要全局忽略的文件路径写入其中。该文件起名为.gitignore，打开终端，在某一个位置创建`.gitignore_global`文件（**建议在当前用户目录下**）：

    ```
    vi -/.gitignore_global
    
    .DS_Store 
    **/.DS_Store
    .DS_Store？
      
    ```

    然后对git进行全局设置，让git忽略.gitignore_globalr中的所有文件：

    ```git config --global core.excludesfile ~/.gitignore_global```
    这样就不用每个git目录都设置忽略.DS_Store文件了I
    此时终端输入：

    git config --list

    如果有下面一行配置

    ```
    [core]
    excludesfile =/Users/[username]/.gitignore_global
    ```

    就说明已经添加成功了，以后Git就不会再记录，.DS Store了。

    ### 批量移除已有的.DS Store
    即便后续不会再记录，仓库中的DS Store都还在，需要手动删除。终端进入仓库目录，输入：

    ```find . -name .DS_Store -print0| xargs -0 git rm -f --ignore-unmatch```
    这样就删除了所有该仓库的.Ds_Store。重新提交推送即可。

    

    

    



