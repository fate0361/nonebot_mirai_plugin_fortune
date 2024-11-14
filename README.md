<div align="center">

# Fortune

_🙏 今日运势 🙏_

</div>
<p align="center">

  <a href="https://github.com/MinatoAquaCrews/nonebot_plugin_fortune/blob/master/LICENSE">
	<img src="https://img.shields.io/github/license/MinatoAquaCrews/nonebot_plugin_fortune?color=blue">
  </a>

  <a href="https://github.com/nonebot/nonebot2">
	<img src="https://img.shields.io/badge/nonebot2-^2.0.0rc4-green">
  </a>

  <a href="https://github.com/MinatoAquaCrews/nonebot_plugin_fortune/releases/tag/v0.4.12">
	<img src="https://img.shields.io/github/v/release/MinatoAquaCrews/nonebot_plugin_fortune?color=orange">
  </a>

  <a href="https://www.codefactor.io/repository/github/MinatoAquaCrews/nonebot_plugin_fortune">
	<img src="https://img.shields.io/codefactor/grade/github/MinatoAquaCrews/nonebot_plugin_fortune/master?color=red">
  </a>

  <a href="https://github.com/MinatoAquaCrews/nonebot_plugin_fortune">
	<img src="https://img.shields.io/pypi/dm/nonebot_plugin_fortune">
  </a>

  <a href="https://results.pre-commit.ci/latest/github/MinatoAquaCrews/nonebot_plugin_fortune/master">
	<img src="https://results.pre-commit.ci/badge/github/MinatoAquaCrews/nonebot_plugin_fortune/master.svg" alt="pre-commit.ci status">
  </a>

</p>

## 版本

[v1.0.0](https://github.com/MinatoAquaCrews/nonebot_plugin_fortune/releases/tag/v0.4.12)

⚠️ 适配nonebot_adapter_mirai `^2.3.3`

👉 [如何添加更多的抽签主题资源？欢迎贡献！🙏](https://github.com/MinatoAquaCrews/nonebot_plugin_fortune/blob/master/How-to-add-new-theme.md)

本插件仅适应于mirai及nonebot双开且使用[NoneBot-Adapter-Mirai适配器](https://github.com/nonebot/adapter-mirai)将nonebot和mirai连接使用的情况

## 安装

1. 安装方式：

   - 通过 `zip` 或 `git clone` 下载本插件所有内容，并修改用于启动nonebot的bot.py文件，编写加载插件目录的文件，示例如下：
	```python
	import nonebot
	from nonebot.adapters.mirai2 import Adapter as MIRAI2Adapter  # 引用 nonebot_adapter_mirai2
 
	# 初始化 NoneBot
	nonebot.init()
	app = nonebot.get_asgi()
 
	# 注册适配器
	driver = nonebot.get_driver()
	driver.register_adapter(MIRAI2Adapter)  # 将其塞入 nonebot2 中
 
	# 在这里加载插件
	nonebot.load_from_toml("pyproject.toml")  # 该配置文件请参考Mirai适配器
	nonebot.load_plugins("src/plugins", "src/plugins/nonebot_plugin_fortune")  # 本地插件
 
	if __name__ == "__main__":
	    nonebot.logger.warning("Always use `nb run` to start the bot instead of manually running!")
	    nonebot.run(app="__mp_main__:app")
	```

2. 抽签主题图片 `img` 、字体 `font` 、文案 `fortune` 等资源均位于 `./resource` 下，可在 `env` 中设置 `FORTUNE_PATH`；

   ```shell
   FORTUNE_PATH="your-path-to-resource"    # For example, "./my-data/fortune"，其下有img、font、fortune文件夹等资源
   ```

   ⚠️️ 插件启动时，将自动检查资源是否缺失（**除字体与图片**资源）

3. 在 `env` 下设置 `xxx_FLAG` 以启用或关闭抽签随机主题（默认全部开启），例如：

   ```shell
   AMAZING_GRACE_FLAG=false    # 奇异恩典·圣夜的小镇
   ARKNIGHTS_FLAG=true         # 明日方舟
   ASOUL_FLAG=true             # A-SOUL（默认关闭）
   AZURE_FLAG=true             # 碧蓝航线
   DC4_FLAG=false              # dc4
   EINSTEIN_FLAG=true          # 爱因斯坦携爱敬上
   GENSHIN_FLAG=true           # 原神
   GRANBLUE_FANTASY_FLAG=true  # 碧蓝幻想
   HOLOLIVE_FLAG=true          # Hololive（默认关闭）
   HOSHIZORA_FLAG=true         # 星空列车与白的旅行
   LIQINGGE_FLAG=true          # 李清歌（默认关闭）
   ONMYOJI_FLAG=false          # 阴阳师
   PCR_FLAG=true               # 公主连结
   PRETTY_DERBY_FLAG=true      # 赛马娘
   PUNISHING_FLAG=true         # 战双帕弥什
   SAKURA_FLAG=true            # 樱色之云绯色之恋
   SUMMER_POCKETS_FLAG=false   # 夏日口袋
   SWEET_ILLUSION_FLAG=true    # 灵感满溢的甜蜜创想
   TOUHOU_FLAG=true            # 东方
   TOUHOU_LOSTWORD_FLAG=true   # 东方归言录
   TOUHOU_OLD_FLAG=false       # 东方旧版
   WARSHIP_GIRLS_R_FLAG=true   # 战舰少女R
   ba_flag: bool = True        # 碧蓝档案（取自mirai的[arona插件](https://github.com/diyigemt/arona)）
   kud_flag: bool = True       # 库特（小小克星外传）
   ab_flag: bool = True        # 天使的心跳（只做了立华奏）
   nene_flag: bool = True      # 魔女的夜宴（只做了宁宁）
   siki_flag: bool = True      # 小识（夏日口袋：rb）
   murasame_flag: bool = True  # 千恋万花（只做了丛雨）
   ```

   **请确保不全为 `false`，否则会抛出错误**

4. 因为主题列表太长了，改为转发聊天记录的形式发送，请修改\resource\__init__第81-83行伪造聊天记录的发送者信息

5. 在 `resource/fortune_setting.json` 内配置**指定抽签**规则，例如：

   ```json
   {
     "group_rule": {
       "123456789": "random",
       "987654321": "azure",
       "123454321": "granblue_fantasy"
     },
     "specific_rule": {
       "凯露": ["pcr/frame_1.jpg", "pcr/frame_2.jpg"],
       "可可萝": ["pcr/frame_41.jpg"]
     }
   }
   ```

   _group_rule会自动生成，specific_rule可手动配置_

   ⚠️ 指定角色签想修复，但没修好

6. 占卜一下你的今日运势！🎉

## 功能

1. 随机抽取今日运势，配置多种抽签主题：原神、PCR、Hololive、东方、东方归言录、明日方舟、赛马娘、阴阳师、碧蓝航线、碧蓝幻想、战双帕弥什，galgame主题等……

2. 可指定主题抽签；

3. 每群每人一天限抽签1次，0点刷新（贪心的人是不会有好运的🤗）抽签信息并清除 `resource/out` 下生成的图片；

4. 抽签的信息会保存在 `resource/fortune_data.json` 内；群抽签设置及指定抽签规则保存在 `resource/fortune_setting.json` 内；抽签生成的图片当天会保存在 `resource/out` 下；

5. `fortune_setting.json` 已预置明日方舟、Asoul、原神、东方、Hololive、李清歌的指定抽签规则（没修）；

6. 🔥 更多的运势文案！`copywriting.json` 整合了19种运势及共计700+条文案！

   ⚠️ 文案资源来自于Hololive早安系列2019年第6.10～9.22期，**Hololive主题默认关闭**。

7. TODO in `v1.1.0` ✨

   - [ ] 最近装了llntqq对接nonebot，这运势好像也不能用了，有空修一修；
   - [ ] 文案排版算法；
   - [x] 新增资源：新的抽签主题资源！
   - [x] 修复指定角色签；

## 命令

1. 一般抽签：今日运势、抽签、运势；

2. 指定主题抽签：[xx抽签]，例如：pcr抽签、holo抽签、碧蓝抽签；

3. 指定签底并抽签：指定[xxx]签，在 `resource/fortune_setting.json` 内手动配置；

   ⚠️ 未修复

4. [群管或群主或超管] 配置抽签主题：

   - 设置[sp/原神/pcr/ba/方舟]签：设置群抽签主题；

   - 重置（抽签）主题：设置群抽签主题为随机；

5. 抽签设置：查看当前群抽签主题的配置；

6. 今日运势帮助：显示插件帮助文案；

7. 查看（抽签）主题：显示当前已启用主题；

## 效果

测试效果出自群聊。

![display](./display.jpg)

## 本插件改自

[opqqq-plugin](https://github.com/opq-osc/opqqq-plugin)

## 抽签图片及文案资源

1. [opqqq-plugin](https://github.com/opq-osc/opqqq-plugin)：原神、PCR、Hololive抽签主题；

2. 感谢江樂丝提供东方签底；

3. 东方归言录(Touhou Lostword)：[KafCoppelia](https://github.com/KafCoppelia)；

4. [FloatTech-zbpdata/Fortune](https://github.com/FloatTech/zbpdata)：其余主题签；

5. 战舰少女R(Warship Girls R)：[veadex](https://github.com/veadex)、[EsfahanMakarov](https://github.com/EsfahanMakarov)；

6. 运势文案：[KafCoppelia](https://github.com/KafCoppelia)。`copywriting.json` 整合了関係運、全体運、勉強運、金運、仕事運、恋愛運、総合運、大吉、中吉、小吉、吉、半吉、末吉、末小吉、凶、小凶、半凶、末凶、大凶及700+条运势文案！来源于Hololive早安系列2019年第6.10～9.22期，有修改。

7. 库特往下的主题是自己画的，有其他gal需求的可以提Issues，上班帕鲁看心情弄。
