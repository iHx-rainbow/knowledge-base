# 移动光猫获取超管权限



```bash
http://192.168.1.1/usr=CMCCAdmin&psw=aDm8H%25MdA&cmd=1&telnet.gch
telnet 192.168.1.1
sidbg 1 DB p DevAuthInfo
sidbg 1 DB decry /userconfig/cfg/db_user_cfg.xml
cd /tmp
vi debug-decry-cfg
/DevAuthInfo
```

修改

```bash
sidbg 1 DB set DevAuthInfo 0 Pass admin
```



{% embed url="https://zhuanlan.zhihu.com/p/693872017" %}
