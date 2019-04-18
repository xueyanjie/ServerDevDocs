# Golang包管理工具-govendor的使用
govendor会将依赖包下载到GOPATH的路径下。<br/>
vendor目录允许不同的代码库拥有它自己的依赖包，并且不同于其他代码库的版本，这就很好的做到了工程的隔离。
## 安装
```shell
go get -u -v github.com/kardianos/govendor
```
## 使用
```shell
#切换到项目目录下，初始化vendor目录
govender init

#将GOPATH中本工程使用到的依赖包自动移动到vendor目录中
#如果GOPATH中没有依赖包，需要先用 go get 获取
govendor add +external  
#或
govendor add +e 
```

## 注意
1. 我们需要把vendor下边的`vendor.json`添加到git，但忽略vendor下的其他文件。
```
.gitignore写法：

/vendor/*
!/vendor/vendor.json
```
2. 其他人可以使用`vendor.json`重新安装依赖包到vendor
```
govendor sync
```
3. 注意vendor所在的目录一定要在第一个GOPAHT下