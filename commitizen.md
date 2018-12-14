# git commitizen
## 为什么使用git commitizen？
## git commitizen有什么好处？
## git commitizen 怎么用？
### git commitizen 配置及安装
- 安装nodejs  
- 安装 git commitizen（以windows系统为例）  
npm install -g commitizen  
- 安装 cz-conventional-changelog  
npm install cz-conventional-changelog  
- 配置 cz-conventional-changelog（windows系统这里必须要在git命令下执行）  
$echo：'{"path":"cz-conventional-changelog"}'>~/.czre  
### git commitizen 主要包括了 commit message 和changelog  
- commit message 的作用  
1.提供更多的历史信息，方便快速浏览  
2.可以过滤某些commit（比如文档改动），便于快速查找信息  
3.可以直接从commit生成Change log  
- commit message的格式（必须包括header，body，footer，header是必须的不可以省略）  
<type>(<scope>): <subject>// 空一行<body>// 空一行<footer>  
其中type是必须的，scope是可选的。subject是必须的  
1.type用于说明 commit 的类别，只允许使用下面7个标识。  
- feat：新功能（feature）  
- fix：修补bug  
- docs：文档（documentation）  
- style： 格式（不影响代码运行的变动）  
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）  
- test：增加测试  
- chore：构建过程或辅助工具的变动  
2.scope：用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同  
3.subject：对本次目的剪短描述，主要采用动词 ，一般为一般时态  
- body:Provide a longer description of the change,一般为项目的具体描述  
- footer： Are there any breaking changes?	是否作出重大改变，默认为N 34  
Does this change affect any open issues? 一般需要一个issuse所对应的编号  
###changlog的配置及安装  
- 安装changelog  
npm install -b conventional-changelog  
- 配置changelog	（这里我弄了好久，一直显示conventional-changelog不是内部命令）  
解决方法：我用 npm ls -g -depth=0  
明明打印出了conventional-changelog，但是就是配置不成功，最后在最后在Git  
提交记录和分支模型中发现Commitizen是依据conventional message，创建起一个生态：  
conventional-changelog-cli：通过提交记录生成 CHANGELOG.md  
conventional-github-releaser：通过提交记录生成 github release 中的变更描述  
conventional-recommended-bump：根据提交记录判断需要升级 Semantic Versioning  
哪一位版本号，所以windows系统并不能采用 conventional-changelog -p angular -i CHANGELOG.md -s -r 0，而是需要使用  conventional-changelog脚手架工具 npm install -g conventional-changelog-cli进行安装  