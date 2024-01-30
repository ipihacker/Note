## git

### Time Out

> ssh: connect to host github.com port 22: Connection timed out fatal: Could not read from remote repository. 

**solve**

**使用https协议，不要使用ssh协议**

在GitHub的本地repo目录，执行如下命令：

```bash
$ git config --local -e
```

然后把里面的url配置项从git格式

```bash
url = git@github.com:username/repo.git
```

修改为https格式

```bash
url = https://github.com/username/repo.git
```

这个其实修改的是repo根目录下的`./git/config`文件。