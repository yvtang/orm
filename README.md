Yvtang-ORM

## 项目背景

由于swoole协程环境不可以直接使用php-fpm的orm组件（由于存在静态全局变量、连接层没有做好协程处理，无法协程安全地使用）

参考easyswoole的orm组件，连贯操作等功能设计借鉴TP5.0的ORM组件。

有疑问、功能建议、bug反馈请在QQ群、github issue、直接联系宣言提交。

## 问题反馈模板

一个完整的提问需要包含以下几点：

- 1.出现了问题，怀疑orm组件的bug，需要先行编写最小测试。（比如一个新的类，单独只调用一个功能，都出问题了，排除其他因素影响）
- 2.用文字描述出现的问题，附带运行和调试的参数截图
- 3.附带第一步最小测试复现脚本

## 安装

```
composer require yvtang/orm
```

## RFC
### 1、Model Invoke
```
Model::invoke()->where(col,val)->get()
Model::invoke(function(Model $m){
    $m->where(col,val)
})->get()
```

### 2、Model Where
```
$model = Model::create()

//$op => = , > , < , != , in , between
$model->where(col1,val1,$op)->get()
$model->where(col1,100,">")->get()
$model->where(col1,100,"<")->get()
$model->where(col1,100,"=")->get()
$model->where(col1,[1,100],"in")->get()
$model->where(col1,[1,100],"between")->get()

$model->where(col1,val1)->where(col2,val2)->get()
=> select * from where col1 = val1 and col2 = val2 limit 1


// 数组形式传参 仅支持此种格式数组
$array1 = [
    ['user', 'easyswoole', '='],
    ['age', '18', '!='],
];
$array1 = [
    ['creaet_time', '2021-12-29 14:47:32', '='],
];
$model->where($array1)->where($array2)->get()


// TODO 兼容 原生sql

```

## 官网文档

https://www.easyswoole.com/Components/Orm/install.html

## 单元测试

```php
 ./vendor/bin/co-phpunit tests
```

推荐使用mysql著名的employees样例库进行测试和学习mysql: https://github.com/datacharmer/test_db

## 主要项目负责人



## 参与贡献方式

- 有实际生产使用的，提出升级迭代建议
- 使用过程中遇到问题，并且查看文档，基本排除个人原因导致的问题，怀疑bug，及时反馈
- 参与orm组件的代码维护、功能升级
- 参与orm组件的文档维护（也就是加入easyswoole文档维护团队）

## 开源协议

Apache-2.0

## 功能介绍
 
- 基于easyswoole/mysqli组件，承当构造层职责。
- 基于easyswoole/pool组件，承当基础连接池。
- 支持执行自定义sql语句、构造器查询。
- 支持事务，DbManager连接管理器也可承当事务管理器的职责。
- 支持关联查询。
- 支持多数据库配置，读写分离。
- 便捷的连贯操作、聚合操作。
