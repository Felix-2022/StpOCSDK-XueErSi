# StpOCSDK
SDK 以 pod 引入方式 获取。 SDK 包括：

设备相关API

```ruby
@interface STPDeviceApi 
```
用户账户相关API

```ruby
@interface STPAuthApi
@interface STPUserApi

```
绘本相关API

```ruby
@interface STPPictureBookApi
```

学习报告相关API

```ruby
@interface STPStudyReportApi
```

## Installation

安装方式

```ruby
pod 'StpOCSDK'
```

## 相关流程

### Config配置

在调用SDK相关API之前，需要先配置

```ruby
@interface STPAccessConfig

设置开发环境
STPAccessConfiger.developEnv = Env_Development;
[STPAccessConfiger setPackageId:@"输入分配给您的PackageId"];

```

### 登录流程
#### 用户选择登录方式，包括 普通用户登录 和 第三方登录的方式。

. 普通用户登录

```ruby

 @param phoneNum 手机号码
 @param passWord 用户密码
 @param pushToken 推送token
+ (void)login:(NSString*_Nonnull)phoneNum passWord:(NSString*_Nonnull)passWord pushToken:(NSString*)token completionBlock:(nullable void (^)(STPUserModel *user,NSError *error)) completionBlock;
```

. 第三方登录


```ruby

/**
 第三方登录

 @param phone 手机号码
 @param passwd 用户密码
 @param thirdCode 第三方code
 */
+(void)loginEx:(NSString*)phone passwd:(NSString*)passwd thirdCode:(NSString*)thirdCode block:(void (^)(STPUserModel *user,NSError *error))block;
```

. 设置当前操作的设备ID与设备AppId

```ruby
/**
设置操作点读笔

@param currDeviceID 点读笔设备ID
@param appId 点读笔AppId
*/
-(void)setCurrDeviceID:(NSString * _Nonnull)currDeviceID  appId:(NSString *_Nonnull) appId;

```
### 配网流程

. 首先连接硬件蓝牙，然后将wifi名称和密码信息（包括wifi密码和用户ID）发送到硬件设备端。发送之后硬件会提示：正在配网中。 此时APP端定时轮询获取配网的结果。

/**
 获取配网的结果  建议采用定时轮询
 */
 
```ruby
+(void)getDeviceBindInfo:(void (^)(STPBindInfo* _Nullable response, NSError *_Nullable error))block;
```

. 蓝牙配网Demo

```ruby
参见blueTooth Demo
https://github.com/Felix-2022/StpDemo
```

### 全部SDK接口使用Demo
https://github.com/Felix-2022/StpOCSDK/blob/master/Example/StpOCSDK/STPViewController.m

