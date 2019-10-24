
# feuid2

## 使用说明
    提交代码自动为标签添加 唯一ID 属性

    使用原理：git commit 时使用 pre-commit 勾子对已经 git add 的文件里对所有 tag 添加唯一ID属性
    
    解决疼点：UI 自动化测试时，页面上标签的标识变更导致UI测试用例需要重写, feuid2 主要为了减少ID变更造成的影响
    
## 适用范围
    * 使用 git 管理的项目
    
    * 使用 npm package.json 安装依赖的前端项目
    
    * 使用 vue 框架的前端项目

## 一键初始化 (切换到项目根目录, 然后执行以下命令)(执行完这条命令之后以后每次commit的时候会自动生成唯一ID)
    sudo npm install -g feuid2 && feuid2 --auto
    
## 执行效果

### 执行流程
![feuid2-commit-flow.png](http://p6.qhimg.com/d/inn/06dfd366/images/feuid-commit-flow.png)

### 执行前
![pre-execute.png](http://p8.qhimg.com/d/inn/06dfd366/images/pre-execute.png)

### 执行后
![after-execute.png](http://p9.qhimg.com/d/inn/4dd249a9/after-execute.png)

### package.json
![package.json.png](http://btbtd.org/uploads/feuid2/package.json.png)

## 安装全局指令
    sudo npm install -g feuid2

## 设置提交勾子与处理所有文件指令: feuid2 --auto 
    cd projectRoot && feuid2 --auto
    
    # feuid2 --auto = feuid2 --setup && feuid2 --full
    
## 其他操作
    
### 设置提交勾子指令: feuid2 --setup 
    cd projectRoot && feuid2 --setup
    
    # 这个指令自动添加2个npm模块 feuid2、husky
    # 拷贝 feuid2 模块里的 feuid2.config.js 到项目根目录
    # 拷贝 feuid2 模块里的 .huskyrc.json 到项目根目录
    
### 处理所有文件指令: feuid2 --full 
    cd projectRoot && feuid2 --full
    
    # 处理所有符合条件的文件
    
### 处理指定文件指令: feuid2 --target 
    cd projectRoot && feuid2 --target ./filepath.vue
    
    # 处理单个指定的文件 
    
### 更新已经生成的唯一ID: feuid2 --update
    feuid2 --full --update
    
    # 通常与 --full 或者 --target 结合使用
    
### 显示帮助指令: feuid2 --help
    feuid2 --help
    
    # 显示所有可用命令
    
## 参数配置文件 feuid2.config.js
	如果运行命令的项目根目录有 feuid2.config.js，工具会自动读取配置参数

## feuid2.config.js 说明
	{
	    "extension": [ 'vue' ]              //需要处理的文件后缀名
	    , "language": "vue"                 //处理标签的前端框架，目前只支持 vue, 未来会支持 react、angular
	    , "repository": "git"               //代码存储的仓库类型，目前只支持 git, 未来会添加 svn 支持
	    , "dir": [ 'src' ]                  //需要处理唯一ID的目录，默认为 src
	    , "encoding": "utf8"                //项目中的文件编码
	    , "attrname": "data-testid"         //唯一ID的属性名
	    , "countattrname": "data-feuidindex"//列表循环的标签计数索引值
	    , "idprefix": "fe"                  //唯一ID属性值的前缀名
	    , "fixempty": true                  //如果唯一ID属性为空自动修复
	    , "fixrepeat": true                 //如果唯一ID重复自动去重
	    //忽略处理的标签名
	    , "ignoretag": [ "v-hover", "template", "el-table-column" ]   
	}

## git hook 配置文件 .huskyrc.json
    {
        "hooks": {
            "pre-commit": [ "node ./node_modules/feuid2/bin/main.js" ]
        }
    }


