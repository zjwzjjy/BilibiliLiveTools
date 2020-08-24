# BilibiliLiveTools

Bilibili直播工具。自动登录并获取推流地址，可以用于电脑、树莓派等设备无人值守直播。

#### 注意
因为B站随时在更新API，所以工具有随时挂掉的风险。当发现工具非配置原因导致不可用时，请提交issue。API也是本人参考github其他项目来的，未深入了解过B站APP，所以在未来遇到无法解决问题且无人接收情况下，此项目将会被废弃。

#### 致谢
Bilibili登录API以及部分工具类从项目[BilibiliAfk](https://github.com/wwh1004/BilibiliAfk "BilibiliAfk") Fork而来。本项目也是在项目[BilibiliAfk](https://github.com/wwh1004/BilibiliAfk "BilibiliAfk")基础上开发。

#### 前提条件
（1）.首先要有一个连接了摄像头的Linux系统。并能够访问网络。  
（2）.在Bilibili中通过实名认证，并开通了直播间。[点击连接](https://link.bilibili.com/p/center/index "点击连接")开通直播间（很简单的，实名认证通过后直接就可以开通了）  
（3）.FFmpeg。推流默认使用FFmpeg，树莓派官方系统默认安装了的，我就不再赘述，其它系统请自行安装。  

#### 项目说明
（1）Bilibili  
Bilibili Api，包括登陆、开启直播之类的操作都封装在里面，直接调用即可。  
（2）BilibiliLiveCategoryList  
直播分区获取获取工具，可以通过此工具获取直播分区。  
（3）BilibiliLiveTools  
一键开启直播工具。  
[![Demo](https://github.com/withsalt/BilibiliLiveTools/blob/master/doc/demo.jpg "Demo")](https://github.com/withsalt/BilibiliLiveTools/blob/master/doc/demo.jpg "Demo")

#### 如何使用（树莓派）
1. 获取程序  
```shell
wget https://github.com/withsalt/BilibiliLiveTools/releases/download/1.5.0/BilibiliLiveTools_Linux_ARM32.zip
```

2. 解压并授权
```shell
unzip BilibiliLiveTools_Linux_ARM32.zip && chmod -R 775  BilibiliLiveTools_Linux_ARM32 && chmod +x BilibiliLiveTools_Linux_ARM32/BilibiliLiveTools
```

3. 编辑配置文件  
编辑用户配置文件User.json  
```shell
cd BilibiliLiveTools_Linux_ARM32
nano Settings/Users.json  #输入用户名和密码
```
编辑直播配置文件  

```shell
nano Settings/LiveSetting.json
```


```json
{
  "LiveCategory": "28",                     //直播间分类
  "LiveRoomName": "【24H】小金鱼啦~",        //直播间名称
  "CmdString": "ffmpeg -thread_queue_size 1024 -f video4linux2 -s 1280*720 -i \"/dev/video0\" -stream_loop -1 -i \"therain.m4a\" -vcodec h264_omx -pix_fmt yuv420p -r 30 -s 1280*720 -g 60 -b:v 10M -bufsize 10M -acodec aac -ac 2 -ar 44100 -ab 128k -f flv [[URL]]",    //推流命令
  "AutoRestart": true                       //推流命令异常结束后是否自动重新开始
}
```

由于推流方式不同以及FFmpeg配置的问题，这里采用直接填写推流命令的方式。建议填写之前先测试推流命令能否正确执行。

推流命令（CmdString）中的“[[URL]]”，是一个配置符号，将在程序中被替换为获取到的Bilibili推流地址，所以一定要在最终命令中，把测试文件或者地址修改为 “[[URL]]”（URL大写） ，否则程序将抛出错误。

4. 跑起来
```shell
sudo ./BilibiliLiveTools
```

详情可以查看：https://www.quarkbook.com/?p=733

#### 直播分区
开播时需要将ID填写到LiveSetting.json中的LiveCategory中。

|  ID | 分类名称  | 分区名称  |
| :------------ | :------------ | :------------ |
 | 86 | 英雄联盟 | 网游 | 
 | 252 | 逃离塔科夫 | 网游 | 
 | 260 | lol云顶之弈 | 网游 | 
 | 80 | 绝地求生 | 网游 | 
 | 87 | 守望先锋 | 网游 | 
 | 89 | CS:GO | 网游 | 
 | 102 | 最终幻想14 | 网游 | 
 | 84 | 300英雄 | 网游 | 
 | 91 | 炉石传说 | 网游 | 
 | 92 | DOTA2 | 网游 | 
 | 82 | 剑网3 | 网游 | 
 | 78 | DNF | 网游 | 
 | 181 | 魔兽争霸3 | 网游 | 
 | 83 | 魔兽世界 | 网游 | 
 | 240 | APEX英雄 | 网游 | 
 | 88 | 穿越火线 | 网游 | 
 | 249 | 星际战甲 | 网游 | 
 | 115 | 坦克世界 | 网游 | 
 | 248 | 战舰世界 | 网游 | 
 | 196 | 无限法则 | 网游 | 
 | 114 | 风暴英雄 | 网游 | 
 | 93 | 星际争霸2 | 网游 | 
 | 239 | 刀塔自走棋 | 网游 | 
 | 164 | 堡垒之夜 | 网游 | 
 | 251 | 枪神纪 | 网游 | 
 | 81 | 三国杀 | 网游 | 
 | 112 | 龙之谷 | 网游 | 
 | 173 | 古剑奇谭OL | 网游 | 
 | 176 | 幻想全明星 | 网游 | 
 | 300 | 封印者 | 网游 | 
 | 288 | 怀旧网游 | 网游 | 
 | 298 | 新游前瞻 | 网游 | 
 | 107 | 其他游戏 | 网游 | 
 | 35 | 王者荣耀 | 手游 | 
 | 256 | 和平精英 | 手游 | 
 | 163 | 第五人格 | 手游 | 
 | 255 | 明日方舟 | 手游 | 
 | 286 | 百闻牌 | 手游 | 
 | 307 | 风云岛行动 | 手游 | 
 | 293 | 战双帕弥什 | 手游 | 
 | 37 | Fate/GO | 手游 | 
 | 280 | 王者模拟战 | 手游 | 
 | 40 | 崩坏3 | 手游 | 
 | 290 | 双生视界 | 手游 | 
 | 140 | 决战！平安京 | 手游 | 
 | 36 | 阴阳师 | 手游 | 
 | 154 | QQ飞车 | 手游 | 
 | 292 | 火影忍者 | 手游 | 
 | 269 | 猫和老鼠 | 手游 | 
 | 113 | 碧蓝航线 | 手游 | 
 | 250 | 自走棋手游 | 手游 | 
 | 156 | 影之诗 | 手游 | 
 | 274 | 新游评测 | 手游 | 
 | 287 | Re:Zero INFINITY | 手游 | 
 | 206 | 剑网3指尖江湖 | 手游 | 
 | 297 | 梦幻西游三维版 | 手游 | 
 | 294 | 魂器学院 | 手游 | 
 | 305 | 我的勇者 | 手游 | 
 | 262 | 重装战姬 | 手游 | 
 | 41 | 狼人杀 | 手游 | 
 | 268 | 王牌战士 | 手游 | 
 | 253 | 一起来捉妖 | 手游 | 
 | 189 | 明日之后 | 手游 | 
 | 50 | 部落冲突:皇室战争 | 手游 | 
 | 141 | 荒野行动 | 手游 | 
 | 39 | 少女前线 | 手游 | 
 | 182 | 方舟指令 | 手游 | 
 | 42 | 解密游戏 | 手游 | 
 | 184 | 神都夜行录 | 手游 | 
 | 203 | 忍者必须死3 | 手游 | 
 | 178 | 梦幻模拟战 | 手游 | 
 | 258 | BanG Dream | 手游 | 
 | 279 | 长安幻世绘 | 手游 | 
 | 267 | 路人超能100 | 手游 | 
 | 212 | 非人学园 | 手游 | 
 | 215 | 月圆之夜 | 手游 | 
 | 238 | 约战:精灵再临 | 手游 | 
 | 242 | 命运歌姬 | 手游 | 
 | 214 | 雀姬 | 手游 | 
 | 263 | 辐射：避难所Online | 手游 | 
 | 264 | 苍蓝誓约 | 手游 | 
 | 265 | 跑跑卡丁车 | 手游 | 
 | 98 | 其他手游 | 手游 | 
 | 236 | 主机游戏 | 单机 | 
 | 313 | 仁王2 | 单机 | 
 | 217 | 怪物猎人:世界 | 单机 | 
 | 283 | 独立游戏 | 单机 | 
 | 282 | 使命召唤16 | 单机 | 
 | 216 | 我的世界 | 单机 | 
 | 237 | 怀旧游戏 | 单机 | 
 | 310 | 破坏领主 | 单机 | 
 | 277 | 命运2 | 单机 | 
 | 218 | 饥荒 | 单机 | 
 | 228 | 精灵宝可梦 | 单机 | 
 | 270 | 人类一败涂地 | 单机 | 
 | 247 | 拾遗记 | 单机 | 
 | 226 | 荒野大镖客2 | 单机 | 
 | 309 | 植物大战僵尸 | 单机 | 
 | 308 | 塞尔达传说 | 单机 | 
 | 295 | 方舟 | 单机 | 
 | 219 | 以撒 | 单机 | 
 | 229 | 古剑奇谭三 | 单机 | 
 | 304 | 三国志 | 单机 | 
 | 273 | 无主之地3 | 单机 | 
 | 284 | 死亡搁浅 | 单机 | 
 | 244 | 鬼泣5 | 单机 | 
 | 243 | 全境封锁2 | 单机 | 
 | 232 | 了不起的修仙模拟器 | 单机 | 
 | 224 | 太吾绘卷 | 单机 | 
 | 302 | FORZA 极限竞速 | 单机 | 
 | 275 | 幽灵行动:断点 | 单机 | 
 | 271 | 遗迹:灰烬重生 | 单机 | 
 | 266 | 火焰纹章：风花雪月 | 单机 | 
 | 272 | 一起开火车！ | 单机 | 
 | 261 | 马里奥制造2 | 单机 | 
 | 257 | 全面战争:三国 | 单机 | 
 | 221 | 战地5 | 单机 | 
 | 241 | 圣歌 | 单机 | 
 | 227 | 刺客信条:奥德赛 | 单机 | 
 | 230 | 任天堂明星大乱斗：特别版 | 单机 | 
 | 220 | 辐射76 | 单机 | 
 | 225 | 中国式家长 | 单机 | 
 | 222 | 超级马里奥奥德赛 | 单机 | 
 | 311 | 女神异闻录5 | 单机 | 
 | 235 | 其他单机 | 单机 | 
 | 21 | 视频唱见 | 娱乐 | 
 | 207 | 舞见 | 娱乐 | 
 | 145 | 视频聊天 | 娱乐 | 
 | 143 | 才艺 | 娱乐 | 
 | 199 | 虚拟主播 | 娱乐 | 
 | 136 | 美食 | 娱乐 | 
 | 123 | 户外 | 娱乐 | 
 | 25 | 手工 | 娱乐 | 
 | 28 | 萌宠 | 娱乐 | 
 | 312 | 宅现场 | 娱乐 | 
 | 27 | 学习 | 娱乐 | 
 | 33 | 映评馆 | 娱乐 | 
 | 34 | 音乐台 | 娱乐 | 
 | 190 | 唱见电台 | 电台 | 
 | 193 | 声优 | 电台 | 
 | 192 | 聊天电台 | 电台 | 
 | 94 | 同人绘画 | 绘画 | 
 | 51 | 原创绘画 | 绘画 | 
 | 95 | 临摹绘画 | 绘画 | 
 | 96 | 其他绘画 | 绘画 | 
 | 315 | 共抗疫情 | 战疫 | 
 
 ## Stargazers over time
[![Stargazers over time](https://starchart.cc/withsalt/BilibiliLiveTools.svg)](https://starchart.cc/withsalt/BilibiliLiveTools)
