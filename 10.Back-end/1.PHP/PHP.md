# PHPunit install

```
wget https://phar.phpunit.de/phpunit.phar
chmod +x phpunit.phar
sudo mv phpunit.phar /usr/local/bin/phpunit
phpunit --version
```

# PHPDoc

```
brew isntall php71
```

## 代码规范

[jupeter/clean-code-php](https://github.com/jupeter/clean-code-php)

## OOP

继承：类分层、接口分层 实现：类实现接口 依赖：类作为另一个类方法的参数 关联：类属性 聚合：可以有 组合：必须有

- PHP异步调用
- 正则匹配src标签
- 处理回文字符

## 模型

数据模型

业务模型

## 功能

trait就是为了避免代码重复而生

```
Trait OwnerTrait{
    public function owner(){
        var_dump('comment owner');
    }
}

class Comment{
    use OwnerTrait;
}
//(new Comment())->owner();
// 或者以下两行代码是一样的效果
$comment = new Comment();
$comment->owner();
```

优先级:从基类继承的成员会被 trait 插入的成员所覆盖。优先顺序是来自当前类的成员覆盖了 trait 的方法，而 trait 则覆盖了被继承的方法。

接口与抽象类：

1.接口中的每个方法，继承类里面都要去实现 2.接口中的方法后面不要跟大口号{},因为接口只是定义需要有这个函数，并不是自己去实现 3.抽象类中 abstract 的方法，继承类里面都要去实现，也可以理解成接口中的每个方法都是 abstract 方法 4.抽象方法中没有abstract 的方法，继承类不必非要写那个方法

举例,场景：我们在记录日志的时候，有时候可能需要写入文件，有时候可能写入数据库 这时候，我们可以写一个Log接口，定义需要的方法 然后分别写一个FileLog类和一个DatabaseLog类 然后我们写一个UsersController类做一个依赖注入，这样我们需要使用哪种方式写日志，实例化的时候，注入哪种类即可

```
<?php
// 定义接口
interface  Log{
    public function save($message);
}

// 稳健型日志
class FileLog implements Log{
    public function save($message){
        var_dump('log into file'.$message);
    }
}
// 数据库型日志
class DatabaseLog implements Log{
    public function save($message){
        var_dump('log into database'.$message);
    }
}

//自定义类实现接口
class UsersController{
    protected $log;
    public function __construct(Log $log)
    {
        $this->log = $log;
    }

    public function register(){
        $name= 'long';
        $this->log->save($name);
    }
}

//$controller = new UsersController(new DatabaseLog());
//string(21) "log into databaselong"
$controller = new UsersController(new FileLog());
//string(17) "log into filelong"
$controller->register();
```

### 扩展

- intl
- mcrypt
- memeache
- memeached
- mongo
- opcache
- pdo-pgsql
- phalcon
- redis
- sphinx
- swoole
- xdebug

TP参考：<https://github.com/ijry/lyadmin>

laravel->symfony

<https://leanpub.com/phptherightway/read#test_driven_development_title>

## 框架

- [pinguo/php-msf](https://github.com/pinguo/php-msf)PHP微服务框架即"Micro Service Framework For PHP"，是Camera360社区服务器端团队基于Swoole自主研发现代化的PHP协程服务框架，简称msf或者php-msf，是Swoole的工程级企业应用框架，经受了Camera360亿级用户高并发大流量的考验

## 资源

- [Awesome PHP](http://coffeephp.com/resources)
- [开源项目](https://my.oschina.net/editorial-story/blog/1535228)

## 社区

- [coffeephp](http://coffeephp.com/)

<http://www.jianshu.com/p/a5d905778b47>