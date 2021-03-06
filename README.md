# yii2-rbac

> Yii2 rbac 精简版(无对外接口) **仅供无需rbac接口的api应用使用**
> 根据[yii2-rest-rbac（https://github.com/windhoney/yii2-rest-rbac）](https://github.com/windhoney/yii2-rest-rbac)修改
> 

### **安装**

```php
composer require heimo/yii2-rbac
```

### **使用**

#### **配置权限**

```php
    'components' => [
        'authManager' => [
            'class' => 'heimo\rbac\components\DbManager', //配置文件
        ],
    ],

    'as access' => [
        'class' => 'heimo\rbac\components\AccessControl',
        'allowActions' => [//允许访问的节点，可自行添加
            'login/*',
            'logout/*',
            'callback/*',
        ]
    ],
```

#### **创建所需要的表**

1. 菜单表menu

```php
yii migrate --migrationPath=@vendor/heimo/yii2-rbac/migrations
```

2. rbac相关权限表

```php
yii migrate --migrationPath=@yii/rbac/migrations/
```

#### **授权认证方式**

1. url中增加 `access_token` 参数 或者 header中增加 `Authorization` 参数，值为 `Bearer [access_token值]`

2. UserModel中实现 `loginByAccessToken($access_token)` 方法
