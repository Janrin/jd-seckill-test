# Jd_Seckill

## 特别声明:

* 本仓库发布的`jd_seckill`项目中涉及的任何脚本，仅用于测试和学习研究，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断。

* 本项目内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。

* `huanghyw` 对任何脚本问题概不负责，包括但不限于由任何脚本错误导致的任何损失或损害.

* 间接使用脚本的任何用户，包括但不限于建立VPS或在某些行为违反国家/地区法律或相关法规的情况下进行传播, `huanghyw` 对于由此引起的任何隐私泄漏或其他后果概不负责。

* 请勿将`jd_seckill`项目的任何内容用于商业或非法目的，否则后果自负。

* 如果任何单位或个人认为该项目的脚本可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我们将在收到认证文件后删除相关脚本。

* 以任何方式查看此项目的人或直接或间接使用`jd_seckill`项目的任何脚本的使用者都应仔细阅读此声明。`huanghyw` 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何相关脚本或`jd_seckill`项目，则视为您已接受此免责声明。
  
* 您必须在下载后的24小时内从计算机或手机中完全删除以上内容。  
  
* 本项目遵循`GPL-3.0 License`协议，如果本特别声明与`GPL-3.0 License`协议有冲突之处，以本特别声明为准。

> ***您使用或者复制了本仓库且本人制作的任何代码或项目，则视为`已接受`此声明，请仔细阅读***  
> ***您在本声明未发出之时点使用或者复制了本仓库且本人制作的任何代码或项目且此时还在使用，则视为`已接受`此声明，请仔细阅读***

## 随便说两句
1.通过朋友的使用（2020-12-12至2020-12-17），证实这个脚本确实能抢到茅台。

2.最近jd修补部分访问参数，很多是陪跑状态，不要怀疑自己人品，图个乐趣。

3.`90016`和`90008`应该属于正常情况，曾经的在反馈此代码后还能抢购成功。

4.小白信用是否有用？不确定，朋友83.0抢了两次抢购成功，本人99.9抢购五六次才成功。应该还是看脸。
### 样例JSON
```json
{'errorMessage': '很遗憾没有抢到，再接再厉哦。', 'orderId': 0, 'resultCode': 90016, 'skuId': 0, 'success': False}
{'errorMessage': '很遗憾没有抢到，再接再厉哦。', 'orderId': 0, 'resultCode': 90008, 'skuId': 0, 'success': False}
```

## 主要功能
- 预约
  - 自动预约
- 抢购
  - 定时自动抢购

## 运行环境

- [Python 3](https://www.python.org/)

## 第三方库

- 需要使用到的库已经放在requirements.txt，使用pip安装的可以使用指令  
`pip install -r requirements.txt`
- 如果国内安装第三方库比较慢，可以使用以下指令进行清华源加速
`pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/`

## 使用教程  
#### 1. 推荐Chrome浏览器
#### 2. 网页扫码登录，或者账号密码登录
#### 3. 填写config.ini配置信息 
(1)`eid`和`fp`找个普通商品随便下单,然后抓包就能看到,这两个值可以填固定的 
> 现在已经支持自动获取，因为添加了一个新的三方库，需要在程序运行之前再执行一次安装第三方库的命令  
> 如果想手动获取，随便找一个商品下单，然后进入结算页面，打开浏览器的调试窗口，切换到控制台Tab页，在控制台中输入变量`_JdTdudfp`，即可从输出的Json中获取`eid`和`fp`。
> 现在已经可以自动获取代码在`jd_seckill/jd_spider_requests.py` ，通过进入购物车控制台中输入变量 `{eid:_JdEid,fp:_JdJrTdRiskFpInfo}` 即可从输出`eid`和`fp`。

(2)`sku_id`,`default_user_agent` 
> `sku_id`已经按照茅台的填好。
> `cookies_string` 现在已经不需要填写了
> `default_user_agent` 可以用默认的。谷歌浏览器也可以浏览器地址栏中输入about:version 查看`USER_AGENT`替换

(3)配置一下时间
> 现在不强制要求同步最新时间了，程序会自动同步京东时间
>> 但要是电脑时间快慢了好几个小时，最好还是同步一下吧

以上都是必须的.
> tips：
> 在程序开始运行后，会检测本地时间与京东服务器时间，输出的差值为本地时间-京东服务器时间，即-50为本地时间比京东服务器时间慢50ms。
> 本代码的执行的抢购时间以本地电脑/服务器时间为准

(4)修改抢购瓶数
> 代码中默认抢购瓶数为2，且无法在配置文件中修改
> 如果一个月内抢购过一瓶，最好修改抢购瓶数为1 
> 具体修改为：在`jd_spider_requests.py`文件中搜索`self.seckill_num = 2`，将`2`改为`1`

#### 4.运行main.py 
根据提示选择相应功能即可。如果出现请扫码登录的提示可查看项目目录下是否存在`qr_code.png`文件,若存在打开图片，并使用京东手机APP扫码登录即可。

- *Linux下命令行方式显示二维码（以Ubuntu为例）*

```bash
$ sudo apt-get install qrencode zbar-tools # 安装二维码解析和生成的工具，用于读取二维码并在命令行输出。
$ zbarimg qr_code.png > qrcode.txt && qrencode -r qrcode.txt -o - -t UTF8 # 解析二维码输出到命令行窗口。
```

#### 5.抢购结果确认 
抢购是否成功通常在程序开始的一分钟内可见分晓！  
搜索日志，出现“抢购成功，订单号xxxxx"，代表成功抢到了，务必半小时内支付订单！程序暂时不支持自动停止，需要手动STOP！  
若两分钟还未抢购成功，基本上就是没抢到！程序暂时不支持自动停止，需要手动STOP！  


## Docker 运行

> * 自行准备`docker`或`docker-compose`环境  
> * 修改`dockerfile`目录中的配置文件`docker.env`  
> * 目前支持直接使用`docker`的方式进行管理，也支持`docker-compose`的方式进行管理，根据自己的使用习惯进行选择  
> * 推荐使用`docker-compose`的方式，更方便一点  
> * 最新代码合并到主分之后，镜像服务器构建新的镜像会需要大概30分钟的时间，请分支合并后一小时再拉取最新镜像  

### 使用Docker-Compose进行容器管理（推荐）

#### 拉取镜像
```bash
# 如果不执行此步骤则启动容器时自动进行本地构建镜像
$ sudo docker-compose -f compose/docker-compose.yml pull 
```

#### 启动容器

```bash
# 如镜像不存在会自动本地构建一个镜像
$ sudo docker-compose -f compose/docker-compose.yml up 
```

> 注意：
> 1. 默认运行选项为秒杀  
> 1. 容器默认前端运行，如果需要停止容器连续按两次`Ctrl+C`。
> 1. 如果想后端运行，执行命令`sudo docker-compose -f compose/docker-compose.yml up -d`。
> 1. 如果存在名称为`jd-seckill`的非`docker-compose`创建的容器，需要执行`sudo docker rm -f jd-seckill`先进行删除。

#### 查看登录二维码
```bash
$ sudo docker-compose -f compose/docker-compose.yml exec jd-seckill qrcode
```

#### 停止容器

```bash
$ sudo docker-compose -f compose/docker-compose.yml down -t 0 
```

#### 滚动打印运行日志
```bash
$ sudo docker-compose -f compose/docker-compose.yml logs -f
```

#### 查看容器状态
```bash
$ sudo docker-compose -f compose/docker-compose.yml ps
```

### 使用Docker直接进行容器管理

#### 创建镜像
> 一共两种方式可以创建镜像，任选其一即可  
> 如果本地构建镜像失败，可以尝试拉取镜像的方式

```bash
# 第一种，直接从`DockerHub`仓库拉取镜像
$ sudo docker pull huanghyw/jd-seckill:latest

# 第二种，本地构建镜像
$ cd dockerfile
$ sudo docker build -t huanghyw/jd-seckill:latest .
```

#### 启动容器
```bash
$ cd dockerfile
$ sudo docker run -it --rm --env-file docker.env --name jd-seckill huanghyw/jd-seckill:latest
```

#### 查看登录二维码
```bash
$ sudo docker exec jd-seckill qrcode
```

#### 停止容器
```bash
$ sudo docker stop jd-seckill -t 0
```

#### 滚动打印运行日志
```bash
$ sudo docker logs jd-seckill -f
```

#### 查看容器状态
```bash
$ sudo docker ps -a
```

## 感谢
##### 非常感谢原作者 https://github.com/zhou-xiaojun/jd_mask 提供的代码
##### 也非常感谢 https://github.com/wlwwu/jd_maotai 进行的优化

## 希望
#####  希望大佬能进行优化