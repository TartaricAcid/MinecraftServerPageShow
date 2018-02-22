添加服务器请修改`/static/data.json`，格式如下

**有选填标记的可以不填，其它均为必填项**
```json
[
	{
		"name": "服务器名称",
        "maxPlayer": "服务器人数上限",
        "logo": "服务器图标",
        "downloadUrl": "整合包下载地址，实在没有就放curseforge吧",
        "qqGroup": "QQ群",
        "qqGroupUrl": "(选填)加群链接",
        "verifyMethod": "验证方式，可选:none(无验证)|mojang(正版验证)|tongyi(统一通行证)",
        "tongyiRegisterUrl": "注册地址，仅限统一通行证填写",
        "ip": "服务器地址",
        "announcement": "(选填)服务器详细介绍，支持markdown，详情见下方"
	}
]
```

请将服务器介绍文件放在`/static/markdown/`文件夹中，然后将文件名**(不包含路径)**填入`announcement`中
