
## PHP Container & Facade Manager
从 thinkphp=v5.1.42 剥离的 container

### 安装
~~~
composer require ibibicloud/tp5-container
~~~

### Container 用法
~~~
// 获取容器实例
$container = \think\Container::getInstance();

// 从容器中获取对象的唯一实例，没有则自动实例化
$container->get('cache');

// 删除容器中的对象实例
$container->delete('cache');
~~~

支持获取其他命名空间的类
~~~
$config = [
    'a' => '20180910000205172',
    'b' => 'OioYxFWLz5ZwHbIUX',
];
$container = \think\Container::get('\ibibicloud\Demo', [$config]);
$container->hello('aaaaaa');
~~~

### Facade 用法
~~~
<?php

namespace think;

class App 
{
    public function name()
    {
        return 'app';
    }
}
~~~

定义一个app\facade\App类
~~~
<?php

namespace app\facade;

use think\Facade;

class App extends Facade
{
    /**
     * 获取当前Facade对应类名
     * @access protected
     * @return string
     */
    protected static function getFacadeClass()
    {
        return '\think\App';
    }
}
~~~

然后就可以静态方式调用\think\App类的动态方法
~~~
<?php

use app\facade\App;

echo App::name(); // app
~~~