#**大术读家api**

 ###API接口文档 错误码说明 
####1.注册登录状态码 1000000 
- 1000000          手机号已注册
- 1000001          手机号码不符合规则
- 1000002          短信发送失败
- 1000003          注册字段不符合规则
- 1000004          验证码超时
- 1000005          验证码错误
- 1000006          密码必须是由6-20位的数字或者字母组成 
- 1000007          注册失败 
- 1000008          登录失败，用户名或者密码错误
- 1000009          填写字段不符合规则
- 1000010          token已过期
- 1000011          退出登录失败
- 1000012          手机号未注册
- 1000013          重置密码失败
- 1000014          注册app成功,注册环信失败
- 1000015          重置app密码成功,重置环信账号密码失败 
- 1000016          删除环信用户成功，删除app用户失败
- 1000017          删除环信用户失败


#####2.扫码关注状态码 
- 2000001          扫描条形码有误 
- 2000002          数据库无此书籍 

#####3.阅聊状态码 
#####4.定位搜索状态码 4000000 
- 4000000           设置用户坐标失败
- 4000001           获取附近用户坐标失败，查询不到相关的结果

#####5.个人设置状态码
-   status:401        未授权
-   status:429        请求次数达到上限
-   5000000           个人信息设置失败
-   5000001           图片最大不可超过2M
-   5000002           请上传标准图片文件, 支持gif,jpg,png和jpeg
-   5000003           图片上传成功，保存失败
-   5000004           图片上传失败
-   5000005                 个人信息设置成功，修改环信用户昵称失败

##### 6.用户反馈，投诉建议

- 6000000           用户反馈信息提交失败

#####一、注册 
##### 1.发送手机验证码

######**接口说明：**

**客户端提交手机号码到服务器, 服务器则向该手机号码发送一条带4位数字的手机验证码，有效期为30分钟。30分钟内不断请求接口，都只会返回一个相同的手机验证码。请限制1分钟内只允许发送一次手机验证码。
请求参数：

| 参数           | 含义   | 规则说明        | 参数类型        | 是否必须 | 缺省值  |
| :----------- | ---- | ----------- | ----------- | ---- | ---- |
| mobile_phone | 手机号码 | 用户注册的可用手机号码 | integer(11) | 是    | 无    |


请求实例：

- [ ] GET /register/sendcode?mobile_phone=18508236987 


HTTP/1.1 Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)
 返回结果：
 手机可用： 

    { "code": 200, "message":"手机验证码发送成功" } 

######2.账号注册  
接口说明：客户端填写手机号码、密码、验证码到服务器进行验证，验证成功则注册创建。同时创建即时通讯的账号。

请求参数：

| 参数                | 含义    | 规则说明        | 参数类型        | 是否必须 | 缺省值  |
| ----------------- | ----- | ----------- | ----------- | ---- | ---- |
| mobile_phone      | 手机号码  | 用户注册的可用手机号码 | integer(11) | 是    | 无    |
| password          | 密码    | 密码长度6-20位，由数字或者字母组成   |string    | 是    | 无    |
| verification_code | 短信验证码 | 4位          | integer     | 是    | 无    |

 




 请求实例：

 *POST*  

<u>/register/actregister HTTP/1.1 Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)</u> 
返回结果： 


注册成功：

    { "code": 200， "message":"注册成功" } 

#### 二、登录登出 
######1.账号登录 
接口说明：
用户可以通过用户名和密码直接登录
 请求参数： 

| 参数名          | 含义   | 规则说明        | 参数类型        | 是否必须 | 缺省值  |
| ------------ | ---- | ----------- | ----------- | ---- | ---- |
| mobile_phone | 手机号码 | 用户注册的可用手机号码 | integer(11) | 是    | 无    |
| password      | 密码    | 密码长度6-20位，由数字或者字母组成   |string    | 是    | 无    |



 请求实例：

   POST /login/logincheck HTTP/1.1 Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web) 

返回结果： 
登录成功

     { "code": 200, "message":"登录成功"， "data":{"access_token": "94633564bf58064cca3be21940cc2eb5beea85df" } }

######2.退出登录
 接口说明：
用户退出登录时，清除token和time_out 请求参数： 

| 参数名          | 含义        | 规则说明      | 参数类型       | 是否必须 |
| ------------ | --------- | --------- | ---------- | :--- |
| access-token | 用户授权Token | 用户授权Token | integer(11 | 是    |


 请求实例：
 <u>GET /logout/exit ?access-token=1f62377af75920ce2a6377dd6e83929bf825feb0 HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)</u> 
返回结果：
 退出成功
​    

    { "code": 200, "message":"退出登录成功"，} 

######三、密码修改 
######1.发送验证码 
接口说明：
重置密码时，发送验证码进行验证 请求参数：

| 参数名          | 含义   | 规则说明        | 参数类型        | 是否必须 | 缺省值  |
| ------------ | ---- | ----------- | ----------- | ---- | ---- |
| mobile_phone | 手机号码 | 用户注册的可用手机号码 | integer(11) | 是    | 无    |



请求实例：

 <u>GET /register/resendmsg?mobile_phone=18508236987</u> 

HTTP/1.1

 Host: http://192.168.1.115/reading-partner-php/api/web
 返回结果：
 手机可用：

     { "code": 200， "message":"手机验证码发送成功" } 

######2.重置密码
 接口说明：
用户忘记密码时，通过向手机发送短信验证码，重置密码。同时重置即时通讯中的密码  请求参数：





| 参数名               |    含义 |    规则说明     | 参数类型        | 是否必须    | 缺省值  |
| ----------------- | ----: | :---------: | ----------- | ------- | ---- |
| mobile_phone      |  手机号码 | 用户注册的可用手机号码 | integer(11) | 是       | 无    |
| password            | 密码    | 密码长度6-20位，由数字或者字母组成   |string    | 是    | 无    |
| verification_code | 短信验证码 |     4位      | integer     | 是       | 无    |
 请求实例： POST /register/resetpwd HTTP/1.1 Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web) 
返回结果：
 重置成功： 

    { "code": 200， "message":"重置密码成功"} 
#####四、个人信息相关
###### 1.个人信息获取 接口说明：用于获取个人信息 请求参数：

| 参数名          | 含义        | 规则说明      | 参数类型        | 是否必须 | 缺省值  |
| ------------ | --------- | --------- | ----------- | ---- | ---- |
| access-token | 用户授权Token | 用户授权Token | integer(11) | 是    | 无    |
请求实例：
 GET /userinfo/getuserinfo ?access-token=iIvChOihED8fVBPWq41OvAGAvzPgSDoc HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web) 
返回结果：
 成功

 `{ "code": 200, "message": "获取个人信息成功", "data": { "user_name": "小白", "gender": 2, "signature": "开心", "avatar_url": { "large": "/uploads/17711351007/7452749ee7326a1a.jpg", "mid" : "/uploads/17711351007/thumb_7452749ee7326a1a.jpg" } } }`

###### 2.设置用户头像
 接口说明：用于账户设置个人信息时，上传个人头像 请求参数：

| 参数名          | 含义        | 规则说明        | 参数类型        | 是否必须 | 缺省值  |
| ------------ | --------- | ----------- | ----------- | ---- | ---- |
| access-token | 用户授权Token | 用户授权Token   | integer(11) | 是    | 无    |
| imgpath      | 用户头像      | 用户上传头像对应的字段 | string      | 是    | 无    |

请求实例：
 POST userinfo/uploadavatar ?access-token=1f62377af75920ce2a6377dd6e83929bf825feb0 HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)
 返回结果：
 成功

     { "code": 200, "message": "图片上传成功，保存成功"} 
######3.个人信息设置
 接口说明：设置用户名，个性签名，性别。同时更新即时通讯用户表中的昵称  请求参数：

| 参数名          | 含义        | 规则说明          | 参数类型            | 是否必须 | 缺省值  |
| ------------ | --------- | ------------- | --------------- | ---- | ---- |
| access-token | 用户授权Token | 用户授权Token     | integer(11) 是   | 无    |      |
| user_name    | 修改后的用户名   | 修改后的用户名       | string(15)      | 否    | 无    |
| signature    | 个性签名      | 用户的个性留言       | string(50)      | 否    | 无    |
| gender       | 性别        | 1:女 2:男 3:未设置 | smallinteger(1) |      |      |
请求实例： POST <u>userinfo/setpersonal ?access-token=iIvChOihED8fVBPWq41OvAGAvzPgSDoc HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)</u> 
返回结果：
 成功：

    {"code":200,"message":"个人信息设置成功，修改环信用户昵称成功","data":{"user_name":"小花","gender":"1","signature":"啦啦啦"}}
######4.删除用户  
接口说明：先删除指定用户对应即时通讯表中的账号记录，再删掉本地服务器中对应的该用户  请求参数：

| 参数名          | 含义        | 规则说明          | 参数类型            | 是否必须 | 缺省值  |
| ------------ | --------- | ------------- | --------------- | ---- | ---- |
| access-token | 用户授权Token | 用户授权Token     | integer(11) 是   | 无    |      |
请求实例： GET <u>userinfo/deleteuser ?access-token=iIvChOihED8fVBPWq41OvAGAvzPgSDoc HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)</u> 
返回结果：
 成功：

  {"code":200,"message":"删除环信用户成功，删除app用户成功","data":""}
#####五、LBS

######1.添加或者修改用户定位坐标 
接口说明：将客户端传来的已获取到的用户手机定位坐标写入后台数据库，如果后台已存在该用户的坐标，则用新的坐标覆盖就坐标，否则直接添加。
 请求参数：

 |参数名 |含义| 规则说明| 参数类型|  是否必须|  缺省值|

| access-token | 用户授权Token | 用户授权Token | integer(11) | 是    | 无    |
| ------------ | --------- | --------- | ----------- | ---- | ---- |
| latitude     | 纬度        | 用户坐标所在的纬度 | double      | 是    | 无    |
| longitude    | 经度        | 用户坐标所在的经度 | double      | 是    | 无    |
请求实例：
 POST

 <u>/location/setposition ?access-token=c73925bfa0f08a641be5db9f5cf0d22ea691e0a7 HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)</u> 
返回结果：
 成功 

    { "code": 200, "message": "设置用户坐标成功",}
###### 2.查询LBS定位 
接口说明：
查询距离用户一定范围内的也在使用该APP的用户
 请求参数：

| 参数名          | 含义        | 规则说明      | 参数类型        | 是否必须 | 缺省值  |
| ------------ | --------- | --------- | ----------- | ---- | ---- |
| access-token | 用户授权Token | 用户授权Token | integer(11) | 是    | 无    |
| count        | 页面显示的条数   | 每页显示内容的条数 | integer     | 是    | 无    |
| page         | 当前页       | 当前页的页数    | integer     | 否    | 1    |

请求实例：

- [ ] GET /location/getposition ?access-token=c73925bfa0f08a641be5db9f5cf0d22ea691e0a7&page=1&count=1 HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web](http://192.168.1.115/reading-partner-php/api/web)


返回结果：

 `{ "code": 200, "message": "获取附近用户坐标成功", "data": { "num": 2, "0": { "user_id": "2", "user_name": "小白", "gender": "2", "distance": 0, "avatar_url": { "large": "/images/18228170109/ae8c5711.jpg", "mid": "/images/18228170109/thumb_ae8c5711.jpg" } }, "1": { "user_id": "3", "user_name": null, "gender": "2", "distance": 2.4, "avatar_url": { "large": "/images/18228170109/ae8c57.jpg", "mid": "/images/18228170109/thumb_ae8c57.jpg" } } } }` 
成功： 

| 字段 含义      | 数据类型       | 长度              |
| ---------- | ---------- | --------------- |
| user_id    | 用户ID       | integer         |
| user_name  | 用户姓名       | string 15       |
| signature  | 个性签名       | string 50       |
| avatar_url | 用户头像url    | string          |
| distance   | 用户与对方的详细距离 | integer         |
| gender     | 用户性别       | smallinteger(1) |
######六、用户反馈 
######1.投诉建议 
接口说明：添加或者修改用户的投诉建议
请求参数： 

| 参数名        | 含义   | 规则说明 | 参数类型        | 是否必须 | 缺省值  |
| ---------- | ---- | ---- | ----------- | ---- | ---- |
| suggestion | 投诉建议 | 用户反馈 | string(100) | 是    | 无    |
请求实例：
 POST <u>suggest/useradvise ?access-token=c73925bfa0f08a641be5db9f5cf0d22ea691e0a7 HTTP/1.1Host: [http://192.168.1.115/reading-partner-php/api/web</u>](http://192.168.1.115/reading-partner-php/api/web)
返回结果： 
成功： 

    { "code": 200, "message": "用户反馈信息提交成功", }
