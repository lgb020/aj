
### 开发接口

#### 1. 用户模块接口
  - [注册](docs/user/user_register.md)
  - [登录](docs/user/user_login.md)
  - [个人中心]
	  - [获取用户信息](docs/user/user_get_msg.md)
	  - [修改用户信息](docs/user/user_put_msg.md)
	  - [实名认证](docs/user/user_auth.md)
	  - [注销](docs/user/user_logout.md)
	  - [我的房源--实名认证/房屋信息展示](docs/house/auth_myhouse.md)
	  

#### 2. 房屋模块接口

  - [首页](docs/house/index.md)
  - [首页搜索](docs/house/search.md)
  - [获取区域和设施信息](docs/house/area_facility.md)
  - [房屋详情](docs/house/detail.md)

#### 3. 预约模块接口

  - [预约页面](docs/order/order.md)
  - [创建预约](docs/order/create_order.md)
  - [所有预约单](docs/order/allorders.md)
  - [房东预约单](docs/order/lorders.md)
  - [修改预约单状态](docs/order/changeorder.md)

***

### 功能点讲解

#### 用户模块

1. 登录注册退出

	a) 注册, 手机号、密码、确认密码、图片验证码

		a1）图片验证码，使用session + redis
		a2) 加密解密
			generate_password_hash
			check_password_hash
	b）登录，手机号、密码

		登录成功向session中存user_id
	c）退出

		清空session中的保存的用户id值

2. 个人中心信息展示

	a) 获取用户的姓名、头像、电话号

		<img src="/static/media/{{ avatar }}">

3.修改头像

	a) 上传选择的头像，使用ajaxSubmit
		阻止默认事件： e.preventDetault()

		$(this).ajaxSubmit(){
			url:'',
			dataType:'json',
			type:'POST/PATCH/PUT/DELETE/GET',
			success:function(data){},
			error:function(data){}
		}

4.修改用户名


5.用户登录状态的校验

	验证session中是否存在user_id

	def is_login(func):
    @wraps(func)
    def check_status(*args, **kwargs):
        try:
            user_id = session['user_id']
        except:
            return redirect(url_for('user.login'))
        return func(*args, **kwargs)
    return check_status

6.实名认证功能

	a) 提交用户名和身份证号码
		校验身份证号码，使用正则表达式
	十八位： ^[1-9]\d{5}(18|19|([23]\d))\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$

	十五位： ^[1-9]\d{5}\d{2}((0[1-9])|(10|11|12))(([0-2][1-9])|10|20|30|31)\d{2}$
	
	b) 实名认证只能认证一次，认证后页面中的提交按钮需要隐藏

部分功能图片：

![图](static/intro_images/aj_user_register.png)
![图](staitc/intro_images/aj_user_login.png)
![图](staitc/intro_images/aj_user_my.png)
![图](staitc/intro_images/aj_user_profile.png)
![图](static/intro_images/aj_user_auth.png)

房屋模块：



#### 房屋模块

#### 订单模块

