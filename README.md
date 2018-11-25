# RollToolsApi
一个提供开发中常用数据的一个稳定聚合Api接口源，运行于独立服务器，免费，且长期维护，会持续添加新的接口！

如果在使用过程中有什么问题，或者有什么好的意见或者建议，都可以与我联系，mxnzp_life@163.com，联系我请注明您的来意！

-----

## 目录

 * [通用](#通用)
 * [接口列表](#接口列表)
     * [一、福彩-双色球接口](#一福彩-双色球接口)
          * [<strong>指定期号中奖号码</strong>](#指定期号中奖号码)
          * [<strong>最新中奖号码信息</strong>](#最新中奖号码信息)
          * [<strong>获取双色球中奖信息列表</strong>](#获取双色球中奖信息列表)
     * [二、节假日及万年历](#二节假日及万年历)
          * [<strong>指定日期的节假日及万年历信息</strong>](#指定日期的节假日及万年历信息)
          * [<strong>指定多个日期的节假日及万年历信息</strong>](#指定多个日期的节假日及万年历信息)
          * [<strong>指定月份所有的节假日及万年历信息</strong>](#指定月份所有的节假日及万年历信息)
          * [<strong>指定年份所有的节假日及万年历信息</strong>](#指定年份所有的节假日及万年历信息)
     * [三、全国城市列表（全国地级市API，数据来源国家统计局）](#三全国城市列表全国地级市api数据来源国家统计局)
          * [<strong>全国城市列表</strong>](#全国城市列表)
          * [<strong>搜索全国城市列表</strong>](#搜索全国城市列表)
     * [四、IP地址信息](#四ip地址信息)
          * [<strong>获取访问者的ip地址信息</strong>](#获取访问者的ip地址信息)
          * [<strong>获取指定ip的ip地址信息</strong>](#获取指定ip的ip地址信息)
     * [五、其他小工具](#五其他小工具)
          * [<strong>获取不重复长ID</strong>](#获取不重复长id)
          * [<strong>获取不重复短ID</strong>](#获取不重复短id)

----

## 通用

+ **HOST地址：** http://119.27.186.22:8091

+ **说明：** 所有的接口都会返回如下格式的数据，具体数据包装在data中，需要根据状态来确定请求是否成功。

+ **请求方法：** 所有的请求都是GET请求

+ **数据返回格式：**

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": null
  }
  ```

+ **数据返回格式说明（下面所有接口中的数据返回都是基于data的，不再介绍code和msg，请知悉）：**
  + **code：** 状态码 1 返回成功 0 返回失败 此时，请关注msg错误信息
  + **msg：** 提示信息，当code返回0的时候包含错误提示信息
  + **data：** 主要信息，不同接口返回的东西不一样

----

## 接口列表

### 一、福彩-双色球接口

#### **指定期号中奖号码** 

+ **接口说明：** 获取指定期号的双色球获奖号码信息

+ **接口地址：** [HOST]/lottery/ssq/aim_lottery?expect=2018135

+ **参数说明：** expect：彩票期号（七位）必传

+ **返回数据：** 
  + **openCode：** 本期中奖号码
  + **code：** 彩票编号标识（双色球是ssq）
  + **expect：** 彩票期号
  + **name：** 彩票名称
  + **time：** 发布时间

+ **数据样例：**

  ```java
  {
      "openCode": "01,03,06,10,11,29+16",
      "code": "ssq",
      "expect": "2018135",
      "name": "双色球",
      "time": "2018-11-18 21:18:20"
  }
  ```

#### **最新中奖号码信息** 

+ **接口说明：** 获取最新双色球中奖号码信息

+ **接口地址：** [HOST]/lottery/ssq/latest

+ **参数说明：** 无

+ **返回数据：** 

  - **openCode：** 本期中奖号码
  - **code：** 彩票编号标识（双色球是ssq）
  - **expect：** 彩票期号
  - **name：** 彩票名称
  - **time：** 发布时间

+ **数据样例：** 

  ```java
  {
      "openCode": "10,12,15,25,26,27+14",
      "code": "ssq",
      "expect": "2018136",
      "name": "双色球",
      "time": "2018-11-20 21:18:20"
  }
  ```

#### **获取双色球中奖信息列表**

- **接口说明：** 获取最新双色球中奖号码信息

- **接口地址：** [HOST]/lottery/ssq/lottery_list?page=1

- **参数说明：** page 页号

- **返回数据：** 

  + **page：** 当前页数
  + **totalCount：** 总数量

  - **totalPage：** 总页数
  - **limit：** 每页数量
  - **list：** 每页具体数据
    + **openCode：** 本期中奖号码
    + **code：** 彩票编号标识（双色球是ssq）
    + **expect：** 彩票期号
    + **name：** 彩票名称
    + **time：** 发布时间

- **数据样例：** 

  ```java
  {
      "page": 1,
      "totalCount": 903,
      "totalPage": 91,
      "limit": 10,
      "list": [
          {
              "openCode": "10,12,15,25,26,27+14",
              "code": "ssq",
              "expect": "2018136",
              "name": "双色球",
              "time": "2018-11-20 21:18:20"
          },
          {
              "openCode": "01,03,06,10,11,29+16",
              "code": "ssq",
              "expect": "2018135",
              "name": "双色球",
              "time": "2018-11-18 21:18:20"
          }
      ]
  }
  ```

### 二、节假日及万年历

#### **指定日期的节假日及万年历信息**

- **接口说明：** 获取指定日期的节假日及万年历信息

- **接口地址：** [HOST]/holiday/single/{date}  【例如： [HOST]/holiday/single/20181121】

- **参数说明：** date 日期 格式 yyyyMMdd 

- **返回数据：** 

  - **date：** 当前日期
  - **weekDay：** 当前周第几天 1-周一 2-周二 ... 7-周日

  - **yearTips：** 天干地支纪年法描述 例如：戊戌
  - **type：** 类型 0 工作日 1 假日 2 节假日
  - **date：** 当前日期
  - **chineseZodiac：** 属相 例如：狗
  - **solarTerms：** 节气描述 例如：小雪
  - **lunarCalendar：** 农历日期
  - **suit：** 宜事项
  - **dayOfYear：** 这一年的第几天
  - **weekOfYear：** 这一年的第几周

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": {
          "date": "2018-11-25",
          "weekDay": 7,
          "yearTips": "戊戌",
          "type": 1,
          "chineseZodiac": "狗",
          "solarTerms": "小雪后",
          "avoid": "移徙.入宅.安门.作梁.安葬",
          "lunarCalendar": "10-18",
          "suit": "祭祀.祈福.求嗣.斋醮.沐浴.冠笄.出行.理发.拆卸.解除.起基.动土.定磉.安碓硙.开池.掘井.扫舍.除服.成服.移柩.启攒.立碑.谢土",
          "dayOfYear": 329,
          "weekOfYear": 47
      }
  }
  ```

#### **指定多个日期的节假日及万年历信息**

- **接口说明：** 获取指定多个日期的节假日及万年历信息

- **接口地址：** [HOST]/holiday/multi/{dates}  【例如： [HOST]/holiday/multi/20180101,20181010,20181011】

- **参数说明：** dates 日期组 格式 yyyyMMdd,yyyyMMdd,yyyyMMdd （中间用英文逗号隔开） 

- **返回数据：** 

  - **date：** 当前日期
  - **weekDay：** 当前周第几天 1-周一 2-周二 ... 7-周日
  - **yearTips：** 天干地支纪年法描述 例如：戊戌
  - **type：** 类型 0 工作日 1 假日 2 节假日
  - **date：** 当前日期
  - **chineseZodiac：** 属相 例如：狗
  - **solarTerms：** 节气描述 例如：小雪
  - **lunarCalendar：** 农历日期
  - **suit：** 宜事项
  - **dayOfYear：** 这一年的第几天
  - **weekOfYear：** 这一年的第几周

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": [
          {
              "date": "2018-01-01",
              "weekDay": 1,
              "yearTips": "丁酉",
              "type": 2,
              "chineseZodiac": "鸡",
              "solarTerms": "冬至后",
              "avoid": "出行.安葬.修坟.开市",
              "lunarCalendar": "11-15",
              "suit": "祭祀.塑绘.开光.裁衣.冠笄.嫁娶.纳采.拆卸.修造.动土.竖柱.上梁.安床.移徙.入宅.安香.结网.捕捉.畋猎.伐木.进人口.放水",
              "dayOfYear": 1,
              "weekOfYear": 1
          },
          {
              "date": "2018-10-10",
              "weekDay": 3,
              "yearTips": "戊戌",
              "type": 0,
              "chineseZodiac": "狗",
              "solarTerms": "寒露后",
              "avoid": "造庙.嫁娶.掘井.栽种.造桥.作灶.动土",
              "lunarCalendar": "9-2",
              "suit": "祭祀.开光.出行.解除.伐木.作梁.出火.拆卸.入宅.移徙.安床.修造.造畜椆栖.扫舍",
              "dayOfYear": 283,
              "weekOfYear": 41
          },
          {
              "date": "2018-10-11",
              "weekDay": 4,
              "yearTips": "戊戌",
              "type": 0,
              "chineseZodiac": "狗",
              "solarTerms": "寒露后",
              "avoid": "入宅.上梁.斋醮.出火.谢土",
              "lunarCalendar": "9-3",
              "suit": "纳采.订盟.开市.交易.立券.会亲友.纳畜.牧养.问名.移徙.解除.作厕.入学.起基.安床.开仓.出货财.安葬.启攒.入殓.除服.成服",
              "dayOfYear": 284,
              "weekOfYear": 41
          }
      ]
  }
  ```

#### **指定月份所有的节假日及万年历信息**

- **接口说明：** 获取指定月份的节假日及万年历信息

- **接口地址：** [HOST]/holiday/list/month/{date}  【例如： [HOST]/holiday/list/month/201802】

- **参数说明：** date 查询的月份 格式 yyyyMM （只有年月） 

- **返回数据：** 

  - **date：** 当前日期
  - **weekDay：** 当前周第几天 1-周一 2-周二 ... 7-周日
  - **yearTips：** 天干地支纪年法描述 例如：戊戌
  - **type：** 类型 0 工作日 1 假日 2 节假日
  - **date：** 当前日期
  - **chineseZodiac：** 属相 例如：狗
  - **solarTerms：** 节气描述 例如：小雪
  - **lunarCalendar：** 农历日期
  - **suit：** 宜事项
  - **dayOfYear：** 这一年的第几天
  - **weekOfYear：** 这一年的第几周

- **数据样例：** 

  ```java
  {
  
      "code": 1,
      "msg": "数据返回成功",
      "data": [
          {
              "date": "2018-02-01",
              "weekDay": 4,
              "yearTips": "丁酉",
              "type": 0,
              "chineseZodiac": "鸡",
              "solarTerms": "大寒后",
              "avoid": "开仓.嫁娶.移徙.入宅",
              "lunarCalendar": "12-16",
              "suit": "祭祀.沐浴.祈福.斋醮.订盟.纳采.裁衣.拆卸.起基.竖柱.上梁.安床.入殓.除服.成服.移柩.启攒.挂匾.求嗣.出行.合帐.造畜椆栖",
              "dayOfYear": 32,
              "weekOfYear": 5
          },
          ...中间隐藏了"2018-02-02"~"2018-02-27"的数据
          {
              "date": "2018-02-28",
              "weekDay": 3,
              "yearTips": "戊戌",
              "type": 0,
              "chineseZodiac": "狗",
              "solarTerms": "雨水后",
              "avoid": "掘井",
              "lunarCalendar": "1-13",
              "suit": "祭祀.斋醮.裁衣.合帐.冠笄.订盟.纳采.嫁娶.入宅.安香.谢土.入殓.移柩.破土.立碑.安香.会亲友.出行.祈福.求嗣.立碑.上梁.放水",
              "dayOfYear": 59,
              "weekOfYear": 9
          }
      ]
  
  }
  ```

#### **指定年份所有的节假日及万年历信息**

- **接口说明：** 获取指定年份的节假日及万年历信息

- **接口地址：** [HOST]/holiday//list/year/{date}  【例如： [HOST]/holiday/list/year/2018】

- **参数说明：** date 查询的年份 格式 yyyy （只有年份） 

- **返回数据：** 

  - **date：** 当前日期
  - **weekDay：** 当前周第几天 1-周一 2-周二 ... 7-周日
  - **yearTips：** 天干地支纪年法描述 例如：戊戌
  - **type：** 类型 0 工作日 1 假日 2 节假日
  - **date：** 当前日期
  - **chineseZodiac：** 属相 例如：狗
  - **solarTerms：** 节气描述 例如：小雪
  - **lunarCalendar：** 农历日期
  - **suit：** 宜事项
  - **dayOfYear：** 这一年的第几天
  - **weekOfYear：** 这一年的第几周

- **数据样例：** 

  ```java
  
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": [
          {
              "month": 1,
              "days": [
                  {
                      "date": "2018-01-01",
                      "weekDay": 1,
                      "yearTips": "丁酉",
                      "type": 2,
                      "chineseZodiac": "鸡",
                      "solarTerms": "冬至后",
                      "avoid": "出行.安葬.修坟.开市",
                      "lunarCalendar": "11-15",
                      "suit": "祭祀.塑绘.开光.裁衣.冠笄.嫁娶.纳采.拆卸.修造.动土.竖柱.上梁.安床.移徙.入宅.安香.结网.捕捉.畋猎.伐木.进人口.放水",
                      "dayOfYear": 1,
                      "weekOfYear": 1
                  },
                  ...中间隐藏了"2018-01-02"~"2018-01-30"的数据
                  {
                      "date": "2018-01-31",
                      "weekDay": 3,
                      "yearTips": "丁酉",
                      "type": 0,
                      "chineseZodiac": "鸡",
                      "solarTerms": "大寒后",
                      "avoid": "嫁娶.入殓.安葬.出行",
                      "lunarCalendar": "12-15",
                      "suit": "塑绘.开光.沐浴.冠笄.会亲友.作灶.放水.造畜椆栖",
                      "dayOfYear": 31,
                      "weekOfYear": 5
                  }
              ]
          },
          ...中间隐藏了02月到11月的数据
          {
              "month": 12,
              "days": [
                  {
                      "date": "2018-12-01",
                      "weekDay": 6,
                      "yearTips": "戊戌",
                      "type": 1,
                      "chineseZodiac": "狗",
                      "solarTerms": "小雪后",
                      "avoid": "作灶.治病",
                      "lunarCalendar": "10-24",
                      "suit": "祭祀.祈福.订盟.纳采.裁衣.拆卸.修造.动土.起基.安床.移徙.入宅.安香.入殓.移柩.安葬.谢土.赴任.进人口.会亲友",
                      "dayOfYear": 335,
                      "weekOfYear": 48
                  },
                  ...中间隐藏了"2018-12-02"~"2018-12-30"的数据
                  {
                      "date": "2018-12-31",
                      "weekDay": 1,
                      "yearTips": "戊戌",
                      "type": 0,
                      "chineseZodiac": "狗",
                      "solarTerms": "冬至后",
                      "avoid": "开市.破土",
                      "lunarCalendar": "10-25",
                      "suit": "祭祀.沐浴.安床.纳财.畋猎.捕捉",
                      "dayOfYear": 365,
                      "weekOfYear": 1
                  }
              ]
          }
      ]
  }
  ```

### 三、全国城市列表（全国地级市API，数据来源国家统计局）

#### **全国城市列表**

- **接口说明：** 获取全国城市列表信息

- **接口地址：** [HOST]/address/list 

- **参数说明：** 无参

- **返回数据：** 

  - **code：** 省/市/区编号
  - **name：** 省/市/区名称
  - **pchilds：** 市列表
  - **cchilds：** 区列表

- **数据样例：** 

  ```java
  {
      "code":1,
      "msg":"数据返回成功",
      "data":[
          {
              "code":"130000",
              "name":"河北省",
              "pchilds":[
                  {
                      "code":"130100",
                      "name":"石家庄市",
                      "cchilds":[
                          {
                              "code":"130101",
                              "name":"市辖区"
                          },
                          {
                              "code":"130102",
                              "name":"长安区"
                          },
                          ...这里只显示了两个区...
                      ]
                  },
                  {
                      "code":"130200",
                      "name":"唐山市",
                      "cchilds":[
                          {
                              "code":"130201",
                              "name":"市辖区"
                          },
                          {
                              "code":"130202",
                              "name":"路南区"
                          },
                          ...这里只显示了两个区...
                      ]
                  },
                  ...这里只显示了两个市...
              ]
          }
          ...这里只显示了一个省...
      ]
  }
  ```

#### **搜索全国城市列表**

- **接口说明：** 搜索全国城市列表信息

- **接口地址：** [HOST]/address/search 【例如： [HOST]/address/search?type=1&value=深圳】

- **参数说明：** 

  + **type：** 类型 0-查询省份 1-查询城市
  + **value：** 被查询的省份或者城市名称

- **返回数据：** 

  - **code：** 省/市/区编号
  - **name：** 省/市/区名称
  - **pchilds：** 市列表
  - **cchilds：** 区列表

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": [
          {
              "code": "440000",
              "name": "广东省",
              "pchilds": [
                  {
                      "code": "440300",
                      "name": "深圳市",
                      "cchilds": [
                          {
                              "code": "440301",
                              "name": "市辖区"
                          },
                          {
                              "code": "440303",
                              "name": "罗湖区"
                          },
                          ...这里只显示了两个区...
                      ]
                  }
              ]
          }
      ]
  }
  ```

### 四、IP地址信息

#### **获取访问者的ip地址信息**

- **接口说明：** 获取访问者的ip地址信息，先获取您的ip地址，再进行解析

- **接口地址：** [HOST]/ip/self

- **参数说明：** 无参

- **返回数据：** 

  - **ip：** 访问者的ip地址
  - **province：** 省份
  - **provinceId：** 省份id
  - **city：** 城市
  - **cityId：** 城市id
  - **isp：** 网络服务商名称 例如 电信
  - **desc：** 拼接好的描述信息

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": {
          "ip": "119.123.72.166",
          "province": "广东省",
          "provinceId": 440000,
          "city": "深圳市",
          "cityId": 440300,
          "isp": "电信",
          "desc": "广东省深圳市 电信"
      }
  }
  ```

#### **获取指定ip的ip地址信息**

- **接口说明：** 获取指定ip的ip地址信息

- **接口地址：** [HOST]/ip/aim_ip?ip=?  【例如： [HOST]/ip/aim_ip?ip=119.123.72.166】

- **参数说明：** ip 被查询的ip地址 需保证是正确的ip地址格式

- **返回数据：** 

  - **ip：** 访问者的ip地址
  - **province：** 省份
  - **provinceId：** 省份id
  - **city：** 城市
  - **cityId：** 城市id
  - **isp：** 网络服务商名称 例如 电信
  - **desc：** 拼接好的描述信息

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": {
          "ip": "119.123.72.166",
          "province": "广东省",
          "provinceId": 440000,
          "city": "深圳市",
          "cityId": 440300,
          "isp": "电信",
          "desc": "广东省深圳市 电信"
      }
  }
  ```

### 五、其他小工具

#### **获取不重复长ID**

- **接口说明：** 获取不重复长ID信息

- **接口地址：** [HOST]/tools/no_repeat_id/long 

- **参数说明：** 无参

- **返回数据：** 

  - **id：** 不重复16位字符id

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": {
          "id": "8a2a789976e64a1c9455ebd90853d4c6"
      }
  }
  ```


#### **获取不重复短ID**

- **接口说明：** 获取不重复短ID信息

- **接口地址：** [HOST]/tools/no_repeat_id/short

- **参数说明：** 无参

- **返回数据：** 

  - **id：** 不重复8位字符id

- **数据样例：** 

  ```java
  {
      "code": 1,
      "msg": "数据返回成功",
      "data": {
          "id": "jlazntmtjrvcrpnb"
      }
  }
  ```


