# 为静态网站接入 Twikoo 评论系统邮件通知（Mailgun 免费发信方案）

在搭建个人博客时，及时获取读者评论提醒是提升内容互动性的关键。作为一名长期使用Twikoo评论系统的站长，近期通过Mailgun服务实现了邮件通知功能的全流程配置，现将具体实现方案分享如下。

## 一、Email 服务基础搭建

### 1.1 注册 Mailgun 发信服务
登录**Mailgun**官网（保留官方链接的服务名称），其免费套餐提供100封/日的发信额度：
![Pricing](https://bbtdd.com/wp-content/uploads/img/593308950.webp)

> 技术提示：需准备VISA/MasterCard信用卡进行身份验证。建议使用👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/yeka) 虚拟卡控制消费限额。

### 1.2 域名绑定验证
接入博客主域（示例使用`senjianlu.com`）进行授权：
1. 控制台添加自定义域名
![Add a Custom Domain](https://bbtdd.com/wp-content/uploads/img/7685770451375.webp)
2. 按指引配置域名解析
![添加 DNS 解析](https://bbtdd.com/wp-content/uploads/img/8330081173.webp)
3. 完成验证后显示绿标状态
![验证通过](https://bbtdd.com/wp-content/uploads/img/8069624553960326.webp)

## 二、SMTP 认证配置
通过发信域名页面获取 **SMTP credentials**：
python
smtp_server = 'smtp.mailgun.org'
smtp_port = 587
smtp_user = 'postmaster@yourdomain.com'
smtp_password = 'your_generated_password'


测试验证步骤：
1. 使用多邮箱测试列表
python
to_addrs = ['test1@domain.com','test2@domain.com']

2. 成功接收测试邮件
![脚本发信成功](https://bbtdd.com/wp-content/uploads/img/1025024366.webp)

## 三、Twikoo 接入配置
通过管理后台完成参数对接：

SMTP_HOST: smtp.mailgun.org 
SMTP_USER: postmaster@yourdomain.com
SMTP_PASS: ***********

关键设置节点截图：
![邮件通知配置 01](https://bbtdd.com/wp-content/uploads/img/49958246997371.webp)

## 四、功能验证流程
### 4.1 管理通知测试
- 当用户发布新评论时  
![管理员收到通知](https://bbtdd.com/wp-content/uploads/img/66976396039.webp)

### 4.2 用户侧验证
- 评论实时回复触发邮件  
![用户接收测试](https://bbtdd.com/wp-content/uploads/img/45139978363773.webp)

## 五、发信安全设置
控制台开启发信防护：
1. 设置每月上限阈值  
![单月的发信上限](https://bbtdd.com/wp-content/uploads/img/105160134577482.webp)
2. 自动归档历史记录

> 若配置过程中遇到API对接问题，可通过👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/yeka) 获取境外服务开通支持。

## 改进亮点总结
该方案实现效果：
√ 邮件投递响应速度 <3s  
√ 消息正文支持Markdown渲染  
√ 发信域名SPF/DKIM认证齐全