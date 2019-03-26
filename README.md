基于SpringBoot问答网站的设计<br>
=
1.登录与注册模块：<br>
-
用户名与密码合法性检测<br>
如果注册或登录成功，下发ticket作为身份检验依据客户端每次发起请求，与数据库对比ticket是否有效<br>
在数据库中存放的密码使用MD5加密，防止数据库密码泄露<br>
定义第一个拦截器，每次请求都会被拦截，提取cookie里面的ticket，根据ticket查询数据库确认请求方身份<br>
定义第二个拦截器，实现未登录跳转，此时要用到第一个拦截器里的信息，如果未登录就跳转到登录页面<br>
2.问题的发表与敏感词过滤<br>
-
每次发布新问题时进行html标签过滤与敏感词过滤，通过建立敏感词前缀树实现\<br>
3.评论服务<br>
-
评论对象为一个实体，既可以评论问题，也可以评论一个评论\<br>
4.异步队列<br>
-
为了提高网站响应效果，利用redis的list实现了异步队列利用lpush向队列中加入事件，brpop从队列中取出事件处理\<br>
5.粉丝与关注列表<br>
-
利用redis的sortedlist实现粉丝与关注列表，权值为关注的时间<br>
粉丝列表key为entitytype+entityid，value为userid<br>
关注列表key为userid+entitytype，value为entityid<br>
6.赞与踩<br>
-
利用redis的set实现赞踩功能<br>
7.实现推拉模式的feed流<br>
-
推时写入压力大，拉时读取压力大<br>



