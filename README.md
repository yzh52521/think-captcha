# think-captcha

thinkphp6  验证码类库 支持前后端分离，api接口调用

## 安装
> composer require yzh52521/think-captcha

## 使用

### 在控制器中输出验证码

在控制器的操作方法中使用

~~~
public function captcha($id = '')
{
	return captcha($id);
}
~~~
然后注册对应的路由来输出验证码


### 模板里输出验证码

首先要在你应用的路由定义文件中，注册一个验证码路由规则。

~~~
\think\facade\Route::get('captcha/[:id]', "\\yzh52521\\captcha\\CaptchaController@index");
~~~

然后就可以在模板文件中使用
~~~
<div>{:captcha_img()}</div>
~~~
或者
~~~
<div><img src="{:captcha_src()}" alt="captcha" /></div>
~~~
> 上面两种的最终效果是一样的


### 控制器里验证

使用TP的内置验证功能即可
~~~
$this->validate($data,[
    'captcha|验证码'=>'require|captcha'
]);
~~~
或者手动验证
~~~
if(!captcha_check($captcha)){
 //验证失败
};
~~~

## api使用

~~~
public function captcha($id = '')
{
   return yzh52521\captcha\facade\Captcha($id,true);
}
~~~



### api验证

~~~
if (!yzh52521\captcha\facade\Captcha::checkApi($data['verify'], $data['key'])) {
   throw new ValidateException('验证码错误');
}
~~~
