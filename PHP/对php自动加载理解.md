# 自动加载的概念
当我们在PHP中`new`一个不存在的类的时候（类没有被加载或者已经被注销了）,就会调用这个函数`__autoload()`,并将类名传入函数,在该函数中可以去加载那个类，以实现类的自动加载。`__autoload()`需要被实现才可使用,
## 使用spl_autoload实现自动加载的时候
使用`spl_autoload_register`将需要被注册的函数放到SPL的`__autoload`函数栈里面,即将普通的函数转化为自动加载函数