## 写在前面( Introduction)：
    灵感来源于对symfony2的学习，对symfony2的学习，深深爱上了它的"一切皆组件"的思想。你可以在任何项目中
    使用symfony2的任何组件。不过，symfony2并没有单独的做一个"服务定位器"组件。因为其整个框架就是由"服务
    定位器"构成的。
    
    在我们的开发工作中，不可避免的会维护或者改造到由那些令我们头疼的俗称"面条代码"构成的项目。
    这些项目的开发者或许他们开发的时候还未出现或者还未掌握一些高级的面向对象的知识，甚至完全没
    有使用MVC思想，无可厚非，习惯工作于面向对象工作台的我们，在对这些代码进行维护的时候，虽然不
    可能彻底将原本的代码进行重构。但是，应该想办法至少在新开发的功能上尽量使用我们熟悉的面向对象
    的开发模式来进行开发。优点自然是为了方便维护。
    
    当然，你可以选择在项目中整合一整个第三方的框架(比如Yii)，但很多时候，我们并不想为了使用"服务定位器"
    这一个功能而引入整个框架。我们需要的仅仅是"服务定位器"这一个功能。因为有了服务定位器，我们就可以在我
    们要改进的项目中利用它注入任何我们想要的其它模块。
    
    本项目所做的事情，正是如此，将Yii中关于"依赖注入"和"服务定位器"相关的代码提取出来，进行重构，抽取成
    一个单独的只包含"服务定位器"的模块。
    
    因为最近很长时间所做的事情都是上面描述的事情，很多时候，项目并不是由程序员定的，有些项目只是为了探路，
    做到后面就来不及也不能重新开发了。很久之前就想写一个单独的，仅仅有"服务定位器"功能的模块，一直犯拖延症。
    还好，最近项目恰好没太多东西要赶，抽了个空，开始做这件事。
    
    本来是想最完全原创的，不过没那么多时间，而且既然有那么多成熟的框架，最近再重复造轮子，终归没前辈们做了
    那么多年的好。鉴于自己对Yii比较熟，也偏好于Yii的注入方法。因此选择了对Yii进行改造。
    
    希望这个小东西能帮到你，也希望你能发现其中的Bug,我们一起完善它。也算为IT人做一点微薄的贡献。
##  安装：
 composer安装
``` code
    composer require duanlujian/servicelocator
```

##  项目结构：
    di--|
        |base---|
                |Base.php
                |Compontent.php
                |configurable.php
                |T.php
        |di-----|
                |Container.php
                |Instance.php
                |ServiceLocator.php
        |demo---|
                |config.php
                |Person.php
                |test.php
## 使用示例：
    在你的项目入口文件index.php中加入以下代码：
    
    include '../vendor/autoload.php';
    use lujian\base\T;
    $config = require './config.php';
    new T($config);
    
    //var_dump(T::$app->person);
    
    在其它地方，你就可以像在Yii中一样使用你注入的模块了，其中$config是配置要注入的模块以及
    依赖的文件，使用方式和在Yii中使用一样。你可以查看我写的Demo。