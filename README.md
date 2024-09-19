# Termius-cracked

## 破解方法

安装npm 安装asar
```shell
npm config set registry http://mirrors.cloud.tencent.com/npm/
npm install -g @electron/asar
```

### for Windows
1. 解包app.asar
```shell
cd C:\Users\[XXXXX]\AppData\Local\Programs\Termius\resources
npx asar extract app.asar ./app
rm app-update.yml  # 防止自动更新
```

### for MAC

1. 解包app.asar
```shell
cd /Applications/Termius.app/Contents/Resources/
npx asar extract app.asar ./app
rm app-update.yml  # 防止自动更新
```

### 修改js

#### 修改app/background-process/assets/main-xxxxxxx.js

搜索`await this.api.bulkAccount`

`const e=await this.api.bulkAccount();` -> `var e=await this.api.bulkAccount();`

```js
var e=await this.api.bulkAccount();
e.account.pro_mode=true;
e.account.need_to_update_subscription=false;
e.account.current_period={
    "from": "2022-01-01T00:00:00",
    "until": "2099-01-01T00:00:00"
};
e.account.plan_type="Premium";
e.account.user_type="Premium";
e.student=null;
e.trial=null;
e.account.authorized_features.show_trial_section=false;
e.account.authorized_features.show_subscription_section=true;
e.account.authorized_features.show_github_account_section=false;
e.account.expired_screen_type=null;
e.personal_subscription={
    "now": new Date().toISOString().slice(0, -5),
    "status": "SUCCESS",
    "platform": "stripe",
    "current_period": {
        "from": "2022-01-01T00:00:00",
        "until": "2099-01-01T00:00:00"
    },
    "revokable": true,
    "refunded": false,
    "cancelable": true,
    "reactivatable": false,
    "currency": "usd",
    "created_at": "2022-01-01T00:00:00",
    "updated_at": new Date().toISOString().slice(0, -5),
    "valid_until": "2099-01-01T00:00:00",
    "auto_renew": true,
    "price": 12.0,
    "verbose_plan_name": "Termius Pro Monthly",
    "plan_type": "SINGLE",
    "is_expired": false
};
e.access_objects=[{
    "period": {
        "start": "2022-01-01T00:00:00",
        "end": "2099-01-01T00:00:00"
    },
    "title": "Pro"
}]
return .......
```
3. 启动Termius，登录账号，重启Termius
