
# PHP Container & Facade Manager
从thinkphp5.1.42剥离的container

## 安装
~~~
composer require ibibicloud/think5-container
~~~

## Container
~~~
// 获取容器实例
$container = \think\Container::getInstance();

// 从容器中获取对象的唯一实例
$container->get('cache');

// 从容器中获取对象，没有则自动实例化
$container->make('cache');

// 删除容器中的对象实例
$container->delete('cache');
~~~

## Facade
定义一个app\facade\App类之后，即可以静态方式调用\think\App类的动态方法
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
然后就可以静态方式调用动态方法了
~~~
<?php

use app\facade\App;

echo App::name(); // app
~~~