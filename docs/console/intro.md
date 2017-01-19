# Console

命令行是另一种运行应用程序的方式，当你的应用需要每天定时执行，你将用到命令行模式。BetePHP将命令行抽象成与HTTP类型的接口形式，```<controller>:<action>```，
```
./bete blog:dailyUpdate
```
以上命令访问的就是```app/Console/Blog/DailyUpdate.php```这个Action。


## 代码自动生成

为了减少大家写代码的时间，BetePHP支持Model、Middleware、HTTP Action、Console Action代码的自动生成。

```
./bete make:model UserFeedback
./bete make:middleware CheckToken
./bete make:http user/feedback
./bete make:console blog:dailyUpdate
```
