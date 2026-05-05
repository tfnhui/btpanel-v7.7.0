# btpanel-v7.7.0
btpanel-v7.7.0-backup  官方原版v7.7.0版本面板备份

**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）**

```Bash
curl -sSO https://raw.githubusercontent.com/tfnhui/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```

**备用安装链接，适用于不能访问GitHub的服务器。文件公开存放在[d.moe.ms](https://d.moe.ms/AAAAA)**

```
curl -sSO https://d.moe.ms/AAAAA/btpanel-v7.7.0/install/install_panel.sh && bash install_panel.sh
```

# 手动解锁插件：

1，屏蔽手机号

```
sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
```

2，删除强制绑定手机js文件

```
rm -f /www/server/panel/data/bind.pl
```

3，手动解锁宝塔所有付费插件为永不过期
```
sed -i 's/"endtime": -1/"endtime": 999999999999/g' /www/server/panel/data/plugin.json
```
4，给plugin.json文件上锁防止自动修复为免费版

```
chattr +i /www/server/panel/data/plugin.json
```

============================

！！如需取消屏蔽手机号

```
sed -i "s|if (bind_user == 'REMOVED') {|if (bind_user == 'True') {|g" /www/server/panel/BTPanel/static/js/index.js
```
============================

！！修复不能下载文件

```
sed -i 's/add_etags=True,//g' /www/server/panel/BTPanel/__init__.py && sed -i 's/attachment_filename/download_name/g' /www/server/panel/BTPanel/__init__.py && sed -i 's/cache_timeout=0//g' /www/server/panel/BTPanel/__init__.py && bt restart
```
============================
