# 视图
BetePHP默认使用原生PHP渲染视图，调用Action的render方法渲染视图。
```
class Home extends Action
{
    public function run($request)
    {
        $this->render('user/home');
    }
}
```