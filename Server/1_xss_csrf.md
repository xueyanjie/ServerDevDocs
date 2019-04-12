# XSS和CSRF攻击
# XSS攻击
实施XSS攻击需要具备两个条件：
1. 需要向web页面注入恶意代码；
2. 这些恶意代码能够被浏览器成功的执行。

## XSS攻击的分类
1. **XSS反射型攻击**，恶意代码并没有保存在目标网站，通过引诱用户点击一个链接到目标网站的恶意链接来实施攻击的。
2. **XSS存储型攻击**，恶意代码被保存到目标网站的服务器中，这种攻击具有较强的稳定性和持久性，比较常见场景是在博客，论坛等社交网站上，但OA系统，和CRM系统上也能看到它身影，比如：某CRM系统的客户投诉功能上存在XSS存储型漏洞，黑客提交了恶意攻击代码，当系统管理员查看投诉信息时恶意代码执行，窃取了客户的资料，然而管理员毫不知情，这就是典型的XSS存储型攻击。

## XSS攻击可以做的事情
窃取cookie等数据，传送到第三方服务器

## 攻击防御
对用户输入的参数进行过滤。特别是那些需要把用户输入的数据显示出来的场景

# PHP CI中的XSS过滤
CI框架的Security.php内之类防止XSS和CSRF攻击的方法

# CSRF攻击
## 概述
CSRF（Cross Site Request Forgery），中文是跨站点请求伪造。CSRF攻击者在用户已经登录目标网站之后，诱使用户访问一个攻击页面，利用目标网站对用户的信任，以用户身份在攻击页面对目标网站发起伪造用户操作的请求，达到攻击目的。

## CSRF攻击的防御手段
1. 尽量使用POST请求代替GET，注意COOKIE安全
2. 加验证码
3. Referer Check
4. Anti CSRF Token <br />
&nbsp;&nbsp;&nbsp;&nbsp;CSRF攻击是攻击者利用用户的身份操作用户帐户的一种攻击方式，通常使用Anti CSRF Token来防御CSRF攻击，同时要注意Token的保密性和随机性。

```php
<?php 
    function submitcheck($var) {
    	if(!empty($_POST[$var]) && $_SERVER['REQUEST_METHOD'] == 'POST') {
    		if((empty($_SERVER['HTTP_REFERER']) || preg_replace("/https?:\/\/([^\:\/]+).*/i", "\\1", $_SERVER['HTTP_REFERER']) == preg_replace("/([^\:]+).*/", "\\1", $_SERVER['HTTP_HOST'])) && $_POST['formhash'] == formhash()) {
    			return true;
    		} else {
    			return false;
    		}
    	} else {
    		return false;
    	}
    }
    
    //产生form防伪码
    function formhash() {
    	$hashadd = 'sogou~!@';
    	$formhash = substr(md5(substr(strtotime("now"), 0, -7).'|'.$_SESSION['email'].'|'.$hashadd), 8, 8);
    	return $formhash;
    }
?>
```
