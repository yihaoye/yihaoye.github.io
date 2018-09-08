---
layout: post
title:  "Auth0 Hosted Pages"
date:   2018-02-27 11:45:22 +1200
categories: auth0
---
原文链接：  
https://auth0.com/docs/hosted-pages  
https://auth0.com/docs/hosted-pages/login  
  
### 使用Auth0以助你认证用户有两种方式：  
1. Universal Login（包含三种：Lock Widget、Lock Passwordless Widget、Custom Login Form。前两种使用lock.js，最后一个使用auth0.js）（用户进行登录或注册操作时会redirect到托管在Auth0的服务器的Hosted Page页面，比如https://{your_username}.{country_code}.auth0.com/login?client={your_client_code}，完成后再被redirect回你的App的网址，但是如果重定向地址里包含了connection参数及其值（与IDP相关），则用户可能会直接跳过Auth0的Hosted Page页面而直接跳转到该IDP的认证登录页面、网址）
2. 自定义自己App的登录页面（不托管在Auth0的服务器而是你的前端代码）你的App代码使用Lock库或Auth0的SDK或直接调用Auth0的API（Authentication API）。（在自己的代码里使用Lock库就类似Auth0 Dashboard里的Hosted Page里的实例代码一样，比如lock.show()，弹出来的登录框造型一样，也叫embed Lock Widget）
Auth0 Hosted Page就是第一种情况。
注意库Lock和库Auth0 SDK是两码事。（Lock包括CDN的lock.js、Lock for iOS、Lock for Android，只提供一些常用标准Authentication操作和UI）（Auth0 SDK包括CDN或npm的auth0.js、Auth0.Swift、Auth0.Android、Node-Auth0 etc，Auth0 SDK不包括UI但包括所有Authentication操作）（Auth0 SDK让开发者更方便直观的实现Authentication API提供的所有功能并提供一些额外的功能或便利，Lock和Auth0 SDK都是基于Authentication API的）  
  
Auth0可以Host的Page有四种：Login、Password Reset、Guardian Multifactor、Error Page，分别处理不同的业务需求。
使用Auth0 Hosted Page的好处是更安全更方便，因为该登陆页面是托管在Auth0的服务器上的，因此更容易无缝接入CSRF保护，比如防止第三方冒充或sessions劫持。  
  
### Single Sign-On  
如果你想使用、实现SSO，你最好使用Universal Login而不是你自定义的自己App的登录页面。  
当用户通过Hosted Page登录了其余任意一个同Tenant下的App后，Auth0的tenant层域名（比如https://{your_username}.{country_code}.auth0.com/）的cookie会存放在浏览器中，其过程是当下次执行认证请求时（同一个App或另一个App），会检查该App的Tenant层域名的cookie（前提是在Auth0 dashboard做好相关配置，如该App的client启用“Use Auth0 instead of the IdP to do Single Sign On”甚至启用“silent SSO”），如果cookie被验证通过，则用户可能会直接登录进App（如果没启用silent SSO则会重定向到一个显示过往登录账号的Hosted Login Page，用户只要点选过往账号按钮即可立刻登录该账号）。  
除了上面讲的dashboard配置，你无需在dashboard的Hosted Page的托管页面代码上做任何改动。  
  
### 传递自定义参数到Universal Login Page（Hosted Page）  
你可以传递自定义参数到Universal Login Page，并基于参数的值做出响应，首先你在自己的App发送请求或重定向时在URL中加入该参数名（比如title）及其值，然后你在Auth0 dashboard的Hosted Page的代码中通过访问config.extraParams.title可以获取参数的值并以此编写响应逻辑与动作。  
但是在使用config对象前需要在代码里先设置:  
```javascript
        var config = JSON.parse(decodeURIComponent(escape(window.atob('@@config@@'))));
```
然后才能调用config或config.extraParams  
  
如果要使你不同的App应用使用不同的Hosted Page或Rules或Tenant配置，你需要创建新的tenant，然后在相关tenant下创建client（即应用），然后该tenant下的Hosted Page、Rules、Tenant配置会被该Tenant下的所有应用share。  
使用不同Tenant的坏处是不同Tenant不在共享数据与配置，所以要根据你的业务要求考虑是否选择这一方式。  
创建新的Tenant只需要在左上方下拉菜单点击“Create Tenant”，然后以后想要切换Tenant时只需要点击“Switch Tenant”，非常方便。  
  
  
### Auth0有两套API：  
1. Authentication API：所有关于自定义的用户认证、登录登出、注册等后端操作。
2. Management API：几乎所有Auth0 Dashboard上的操作（比如配置等等）都可以用此API完成。
  
### 使用SDK或API的自定义页面的认证过程：
（在Auth0设置不开启OIDC Conformant，点开embedded lock widget后点选IdP，如果发现用户浏览器已登录该IdP则不用用户consent直接跳往下面第1个URL，这一过程很可能使用了Oauth2.0中的Client Credentials Grant所以跳过了用户需要在IdP页面授权这一过程）  
1. https://{username}.{country}.auth0.com/authorize?scope=openid&response_type=token&connection=google-oauth2&sso=true&client_id={auth0_client_id}redirect_uri=http://localhost:3000/#access_token=xxxxxxx&id_token={jwt}&expires_in={expire_time}&token_type=Bearer&auth0Client=xxxxxxxx
2. https://login.{country}.auth0.com/{username}/authorize?scope=openid&response_type=token&connection=google-oauth2&sso=true&client_id={auth0_client_id}redirect_uri=http://localhost:3000/#access_token=xxxxxxx&id_token={jwt}&expires_in={expire_time}&token_type=Bearer&auth0Client=xxxxxxxx
3. https://accounts.google.com/o/oauth2/auth?response_type=code&redirect_uri=https：//login.{country}.auth0.com/login/callback&scope=email profile&state=xxxxxxxx&client_id=xxxxxxxx.apps.googleusercontent.com
4. https://login.{country}.auth0.com/login/callback?state=xxxxxxxx&code=xxxxxxxx#
5. http://localhost:3000/#access_token=xxxxxxxx&id_token={jwt}&expires_in={expire_time}&token_type=Bearer
注意：2的这个URL是1这个URL的响应数据，3是2的响应数据，4又是3的响应数据，5是4的响应数据。1、2中的access_token一样，1、2中的id_token也一样，1、2中的auth0Client也一样。  
  
### Cross Origin Authentication以及third party cookie在这里的应用：  
embedded lock widget不像universal login那样重定向到某一central（即Auth0 Server），因为该widget托管在你的App而不是Auth0。用户 credentials在这之后会发送至authentication provider（如Google）进行用户身份第三方认证，在你的web app这将是cross-origin 请求。  
Third-party cookies：  
虽然浏览器会限制网页只得取得它自己对应的cookie，但大部分浏览器允许第三方cookies的使用，即比如你的Web App使用了一些托管在Google服务器上的资源或组件（比如图片、文件、iframe等等），则用户打开你的App时，谷歌服务器也可以实时访问该用户的浏览器中属于它的cookies。  
  
  
（但如果点开embedded lock widget后点选IdP后发现用户浏览器未登录IdP，则与普通的第三方认证一样了）  
比如第一个重定向的IdP的consent页面上显示比如“Google: Choose an account to continue to auth0.com”  
（https://accounts.google.com/signin/oauth/oauthchooseaccount?client_id=xxxxxxxx.apps.googleusercontent.com&as=xxxxxxxx&destination=https://login.au.auth0.com&approval_state=xxxxxxxx&xsrfsig=xxxxxxxx&flowName=GeneralOAuthFlow）  
待续...  
  
  
#### 题外话：应该何时选择使用Auth0 Universal Login（即Hosted Page）何时选择结合Auth0 API使用自定义页面？  
Universal Login：当你想方便或允许多种登陆方式（第三方认证登陆、账号密码等等）（第三方认证登陆包括企业网站或社交网站），你想更安全  
自定义页面并使用SDK或API：你有多个数据库或Active Directory Connections（但是此方式需要实现Cross-origin Authentication，即处理不同域名间发送用户credentials要面对的安全问题比如网络钓鱼等等，Cross-origin Authentication有一定限制所以要注意）（不过Cross-origin authentication仅限于针对directory的账号密码登陆方式，其他如OpenID Connect或SAML等不需要）  