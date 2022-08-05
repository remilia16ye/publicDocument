# 开放平台对接帮助文档

[toc]

## 一 ， 对接说明

### 1.1 域名

- **接口URL：** <https://api-url.com>
请访问时拼接对应方法URL

### 1.2 调用方式

POST

### 1.3 传输方式

Content-Type: application/json

### 1.4 公共参数

- **系统级参数：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :----- | :----------- |
| appId         | String   | 是 | 分配的应用ID     |
| signMethod         | String   | 是 | 签名算法（目前仅支持MD5）     |
| timestamp         | String   | 是 | 当前时间戳     |
| body         | String   | 是 | 业务入参（Json序列化结果）     |
| sign         | String   | 是 | 签名，参考签名算法     |

- **响应参数：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| success         | Boolean   | 是 | 成功标志     |
| message         | String   | 是 | 消息     |
| code         | String   | 是 | 返回代码     |
| timestamp         | Long   | 是 | 时间戳     |
| result         | T   | 是 | 结果对象     |

### 1.5 签名算法

**appId+body+signMethod+timestamp+mySecret**
1.按appId，body，signMehtod，timestamp的顺序，拼接为“k1v1k2v2k3v3”这样的字符串；
2.在拼接的字符串末尾，拼接分配的secret；
3.计算出拼接好的签名字符串的MD5摘要值

### 1.6 请求示例

POST <https://url/address/getCity>
Content-Type: application/json

```json
{

  "appId": "4de67a45194f12345678968195fbc",

  "sign": "14E14141234567892C54704EB",

  "signMethod": "md5",

  "timestamp": "7888899531021",

  "body": "{\"cityId\":\"1234\"}"

}
```

## 二，API文档

### 1.地址相关

---

#### 1.1 查询一级地址

**接口地址：**

​/address​/getProvince

**接口说明：**

获取一级地址

**应用级参数Body：**

无

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| nation         | String   | 是 | 地址     | -     |
| nationId         | Integer   | 是 | 地址ID     | -     |

---

#### 1.2 查询二级地址

**接口地址：**

​/address​/getCity

**接口说明：**

获取二级地址

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |   -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| nation         | String   | 是 | 地址     | -     |
| nationId         | Integer   | 是 | 地址ID     | -     |

---

#### 1.3 查询三级地址

**接口地址：**

​/address​/getCounty

**接口说明：**

获取三级地址

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| cityId         | Integer   | 是 | 二级地址ID    |   -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| nation         | String   | 是 | 地址     |    -   |
| nationId         | Integer   | 是 | 地址ID     |  -    |

---

#### 1.4 查询四级地址

**接口地址：**

​/address​/getTown

**接口说明：**

获取四级地址

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- |:----------- |
| countyId         | Integer   | 是 | 三级地址ID    |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| nation         | String   | 是 | 地址     | -     |
| nationId         | Integer   | 是 | 地址ID     |  -   |

---

#### 1.5 检验地址有效性

**接口地址：**

​/address​/checkArea

**接口说明：**

检验地址有效性

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- |:----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |  -   |
| cityId         | Integer   | 是 | 二级地址ID    |  -  |
| countyId         | Integer   | 是 | 三级地址ID    | -   |
| townId         | Integer   | 是 | 四级地址ID    | -   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| success         | Boolean   | 是 | 有效性  |  true/false |

---

#### 1.6 详情地址转换四级地址编码

**接口地址：**

​/address​/getAddressCode

**接口说明：**

详情地址转换四级地址编码

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| address         | String   | 是 | 地址   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    | -   |
| province         | String   | 是 | 一级地址ID    |  -   |
| cityId         | Integer   | 是 | 二级地址ID    |  -   |
| city         | String   | 是 | 二级地址名称    |   -  |
| countyId         | Integer   | 是 | 三级地址ID    |  -   |
| county         | String   | 是 | 三级地址名称    |  -   |
| townId         | Integer   | 是 | 四级地址ID    |  -   |
| town         | String   | 是 | 四级地址名称    |  -   |

---

### 2.商品相关

---

#### 1.1 查询赠品信息

**接口地址：**

/goods/batchGetSkuGift

**接口说明：**

根据此接口批量查询主商品附带的赠品或者附件

- 购买主商品数量大于赠品要求最多购买数量，不加赠品
- 购买数量小于赠品要求最少购买数量，不加赠品
- 下单时间不在促销时间范围内，不加赠品

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Map< Long,SkuPromotionDTO >         | Map   | 是 | <商品ID:商品对应赠品信息>    |  -  |

SkuPromotionDTO:

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| maxNum         | Integer   | 是 | 赠品要求最多购买数量    |   -  |
| minNum         | Integer   | 是 | 赠品要求最少购买数量    |   -  |
| promoStartTime         | Long   | 是 | 促销开始时间    |  -   |
| promoEndTime         | Long   | 是 | 促销结束时间    |   -  |
| giftSkuList         | List< GiftSkuVo >   | 是 | 赠品附件列表    |   -    |

GiftSkuVo:

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Long   | 是 | 赠品商品编码    |  -   |
| num         | Integer   | 是 | 数量    |  -   |
| giftType         | Long   | 是 | 赠品类型    | 1：附件，2：赠品    |

---

#### 1.2 查询商品地域购买限制

**接口地址：**

/goods/checkAreaLimit

**接口说明：**

查询商品在特定区域是否可售

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuAreaList         | List< SkuAreaDTO >   | 是 | 购买限制实体    |  -  |

**skuAreaDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| isAreaRestrict         | Boolean   | 是 | 是否受限    |  true 或空值代表区域受限 false 区域不受限  |
| skuId         | skuId   | 是 | 商品id    |  -  |


#### 1.3 检验商品可售性

**接口地址：**

/goods/checkSku

**接口说明：**

查询商品可售性等影响销售的重要属性

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuSaleStateList         | List< skuSaleStateDTO >   | 是 | 购买限制实体    |  -  |

**skuSaleStateDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| saleState         | Boolean   | 是 | 是否可售    |  -  |
| skuId         | Long   | 是 | 商品id    |  -  |
| name         | String   | 是 | 商品名称    |  -  |

---

#### 1.4 下单前商品校验

**接口地址：**

​/goods​/checkSkuSaleStateAndStock

**接口说明：**

下单前实时校验商品是否可采购

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| goodsBaseList         | List< goodsBaseDTO >   | 是 | 校验参数实体   |  -  |

**goodsBaseDTO :**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Long   | 是 | 商品Id   |  - |
| num         | Integer   | 是 | 商品数量   |  - |
| price         | BigDecimal   | 是 | 商品价格   |  - |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Integer   | 是 | 商品id    |  - |
| canPurchase         | String   | 是 | 是否可采    |true 代表可采 false 代表不可采|
| messageList         | List< String >   | 是 | 不可采原因    |  - |

---

#### 1.5 查询分类信息

**接口地址：**

/goods/getCategory

**接口说明：**

根据分类id查询对应分类信息

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| cid         | String   | 是 | 分类id   | - |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| catId         | Integer   | 是 | 分类ID    | - |
| parentId         | String   | 是 | 父分类ID    | - |
| name         | Integer   | 是 | 分类名称    | - |
| catClass         | String   | 是 | 分类级别    | 0：一级分类；1：二级分类；2：三级分类 |
| state         | Integer   | 是 | 有效性    | - |

---

#### 1.6 查询单个商品详情

**接口地址：**

/goods/getDetail

**接口说明：**

查询单个商品的详细信息，不校验是否存在于商品池中。商品图片赠品及促销信息仅供参考

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Long   | 是 | 商品ID   | - |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| saleUnit         | Integer   | 是 | 售卖单位    | - |
| weight         | String   | 是 | 重量    | - |
| productArea         | Integer   | 是 | 产地    | - |
| wareQD         | String   | 是 | 包装清单    | - |
| imagePath         | Integer   | 是 | 主图    | - |
| param         | String   | 是 | 规格参数    | - |
| state         | Integer   | 是 | 上下架状态    | 1上架  0下架 |
| skuId         | String   | 是 | 商品编号    | - |
| brandName         | Integer   | 是 | 品牌名称    | - |
| category         | String   | 是 | 分类    | - |
| name         | Integer   | 是 | 商品名称    | - |
| introduction         | String   | 是 | 商品详情页大字段    | - |

---

#### 1.7 验证货到付款

**接口地址：**

/goods/getIsCod

**接口说明：**

验证商品在指定区域是否可使用货到付款

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Map<Long,boolean>         | Map   | 是 | 商品ID:ture/false    | - |

---

#### 1.8 查询商品库存

**接口地址：**

/goods/getNewStockById

**接口说明：**

查询在指定区域的库存信息

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| List< SkuStockParams >         | SkuStockParams   | 是 | 库存查询参数   |  -  |
| areId         | String   | 是 | 四级地址编码   |  13_1000_4277_0 (分别代表1、2、3、4级地址) |

**SkuStockParams：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Long  | skuId   | 是 | 商品Id   |  -  |
| num  | Integer   | 是 | 商品对应数量   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Long   | 是 | 商品ID    | -  |
| areId         | String   | 是 | 区域码    | -  |
| stockStateId         | String   | 是 | 库存状态编号    | -  |
| stockStateDesc         | String   | 是 | 库存状态描述    | -  |
| remainNum         | String   | 是 | 剩余数量    | -  |

---

#### 1.9 查询商品池编号

**接口地址：**

/goods/getPageNum

**接口说明：**

查询所有商品池编号，商品池编号将用于获取池内商品编号

**应用级参数Body：**

无

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| List< PageDTO >         | PageDTO   | 是 | 商品池    | -    |

**PageDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| name         | String   | 是 | 商品池名称    | -    |
| pageNum         | String   | 是 | 商品池编号    | -    |

---

#### 1.10 查询商品售卖价

**接口地址：**

/goods/getSellPrice

**接口说明：**

查询商品售卖价。查询在客户商品池中的商品价格

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| List< SkuPriceDTO >         | SkuPriceDTO   | 是 | 商品售价信息    |  -  |

**SkuPriceDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId        | Long   | 是 | 商品ID    |  -  |
| price         | BigDecimal   | 是 | 售价    |  -  |
| priceDesc         | String   | 是 | 价格描述    |  -  |
| tax         | BigDecimal   | 是 | 税率    |  -  |
| taxPrice         | BigDecimal   | 是 | 预估税额    |  -  |
| nakedPrice         | BigDecimal   | 是 | 未税价    |  -  |

---

#### 1.11 查询同类商品

**接口地址：**

/goods/getSimilarSku

**接口说明：**

查询被指定为同一类的商品

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| SkuId         | Long   | 是 | 商品id   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| dim         | Integer   | 是 | 维度    |  -  |
| saleName         | String   | 是 | 销售名称    |  -  |
| saleAttrList        | List< SaleAttrVo >   | 是 | 商品销售标签    |  -  |

**saleAttrVo：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| imagePath         | Integer   | 是 | 标签图片地址    |  -  |
| saleValue         | String   | 是 | 标签名称    |  -  |
| skuIds        | List< Long >   | 是 | 当前标签下的同类商品skuId    |  -  |

---

#### 1.12 查询商品图片

**接口地址：**

/goods/getSkuImage

**接口说明：**

查询单个商品的图片

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品Id集合   |  多件商品由','隔开  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Map\<String,List\<SkuImageDTO\>>         | map   | 是 | 一级地址ID    |  -  |

**SkuImageDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuId         | Long   | 是 | 商品编号    |  -  |
| path         | String   | 是 | 图片路径    |  -  |
| created         | String   | 是 | 创建日期    |  -  |
| modified         | String   | 是 | 更新时间    |  -  |
| state         | Integer   | 是 | 是否可用    |  0:不可用;1:可用  |
| isPrimary         | Integer   | 是 | 是否主图    |  1：是 0：否  |
| orderSort         | String   | 是 | 排序    |  -  |
| position         | String   | 是 | 位置    |  -  |
| type         | String   | 是 | 类型    |  -  |
| features         | String   | 是 | 特征    |  -  |

---

#### 1.13 查询商品上下架状态

**接口地址：**

/goods/getSkuState

**接口说明：**

查询商品的上下架状态

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   |  多件商品由','隔开  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| List\<SkuStateDTO>         | Integer   | 是 | 商品状态DTO    |

**SkuStateDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| state         | Integer   | 是 | 商品状态   |  0上架 1下架   |
| skuId         | Long   | 是 | 商品id   |  -   |

---

#### 1.14 查询商品延保

**接口地址：**

/goods/getYanbaoSku

**接口说明：**

根据此接口查询可随主商品一并购买的延保等服务商品

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| skuIds         | String   | 是 | 商品ID   | 多商品id由‘,’隔开|
| provinceId         | String   | 是 | 一级地址ID   |  -  |
| cityId         | String   | 是 | 二级地址ID   |  -  |
| countyId         | String   | 是 | 三级地址ID   |  -  |
| townId         | String   | 是 | 四级地址ID   |  -  |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Map\<Long,List\<SkuYanBaoDTO>>        | map   | 是 | 延保信息    | -   |

**SkuYanBaoDTO：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| mainSkuId        | Long   | 是 | 主商品的sku    | -   |
| imgUrl         | String   | 是 | 保障服务类别显示图标   |  -  |
| detailUrl         | String   | 是 | 库存状态编号   |  -  |
| displayNo         | Integer   | 是 | 保障服务类别显示排序   |  -  |
| categoryCode         | String   | 是 | 保障服务分类编码   |  -  |
| displayName         | String   | 是 | 保障服务类别名称   |  -  |
| YanBaoVoList         | List\<YanBaoVo>   | 是 | 保障服务商品详情列表   |  -  |

**YanBaoVo：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| bindSkuId        | Long   | 是 | 保障服务skuId    | -   |
| bindSkuName         | String   | 是 | 保障服务sku名称   |  -  |
| sortIndex         | Integer   | 是 | 显示排序   |  -  |
| price         | BigDecimal   | 是 | 保障服务sku价格   |  -  |
| tip         | String   | 是 | 保障服务说明提示语   |  -  |
| favor         | Boolean   | 是 | 是否是优惠保障服务   |  -  |

---

#### 1.15 查询商品池内商品编号

**接口地址：**

/goods/querySkuByPage

**接口说明：**

查询单个商品池下的商品列表

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| pageNum         | String   | 是 | 商品池编码   | -   |
| pageSize         | String   | 是 | 每页大小   | -   |
| offset         | String   | 是 | 偏移量   | -   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| remainPage         | Integer   | 是 | 剩余页数    | -   |
| skus         | List\<Long>   | 是 | skuId集合    | -   |
| offset         | Long   | 是 | 在下一次查询时使用    | -   |

---

#### 1.16 搜索商品

**接口地址：**

/goods/searchGoods

**接口说明：**

根据搜索条件查询符合要求的商品列表

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Keyword         | String   | 是 | 搜索关键字   | -   |
| catId         | String   | 是 | 分类Id,只支持三级类目Id   | -   |
| pageIndex         | Integer   | 是 | 当前第几页   | -   |
| pageSize         | Integer   | 是 | 当前页显示   | -   |
| Min         | String   | 是 | 价格区间搜索   | -   |
| Max         | String   | 是 | 价格区间搜索   | -   |
| Brands         | String   | 是 | 品牌搜索   |  多个品牌以逗号分隔，需要编码   |
| cid1         | String   | 是 | 一级分类   | -   |
| cid2         | String   | 是 | 二级分类   | -   |
| sortType         | String   | 是 | 排序方式   | 销量降序="sale_desc";
价格升序="price_asc";
价格降序="price_desc";
上架时间降序="winsdate_desc";
   |
| priceCol         | String   | 是 | 价格汇总    | -   |
| extAttrCol         | String   | 是 | 扩展属性汇总   | -   |
| mergeSku         | boolean   | 是 | 是否合并   | -   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| brandAggregate         | List\<BrandVo>   | 是 | 品牌汇总信息    | -   |
| categoryAggregate         | List\<CategoryVo>   | 是 | 相关分类汇总信息    | -   |
| goodsVos         | List\<GoodsVo>   | 是 | 商品汇总信息    | -   |
| resultCount         | String   | 是 | 搜索结果总记录数量    | -   |
| pageCount         | Integer   | 是 | 总页数    | -   |
| pageSize         | String   | 是 | 每页大小    | -   |
| pageIndex         | Integer   | 是 | 当前页    | -   |

**BrandVo：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| id         | Long   | 是 | 品牌id    | -   |
| name         | String   | 是 | 品牌名称    | -   |
| pinyin         | String   | 是 | 品牌首字母拼音    | -   |

**CategoryVo：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| catId         | Long   | 是 | 分类id    | -   |
| count         | String   | 是 | 分类下商品数量    | -   |
| name         | String   | 是 | 分类名称    | -   |
| weight         | String   | 是 | 分类权重    | -   |

**GoodsVo：**

| **字段**   | **类型**     | **必填** | **描述** | **备注** |
| :---------   | :-----   | :---- | :----------- | :----------- |
| Brand         | Long   | 是 | 分类id    | -   |
| imageUrl         | String   | 是 | 分类下商品数量    | -   |
| name         | String   | 是 | 分类名称    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |
| weight         | String   | 是 | 分类权重    | -   |

---

### 3.售后相关

---

#### 3.1 取消售后申请

**接口地址：**

/afterSale/cancelAfsApply

**接口说明：**

售后申请单取消

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 3.2 确认售后完成

**接口地址：**

/afterSale/confirmAfsOrder

**接口说明：**

确认售后完成

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 3.3 申请售后

**接口地址：**

/afterSale/createAfsApply

**接口说明：**

发起售后申请

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 3.4 查询售后申请单明细

**接口地址：**

/afterSale/getApplyDetailInfo

**接口说明：**

查询售后申请单明细

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 3.5 查询商品售后属性

**接口地址：**

/afterSale/getGoodsAttributes

**接口说明：**

查询订单下商品可售后数量、支持的售后类型

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 3.6 填写运单信息

**接口地址：**

/afterSale/updateSendInfo

**接口说明：**

填写发运信息

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

### 4.订单相关

---

#### 4.1 批量确认收货

**接口地址：**

/order/batchConfirmReceived

**接口说明：**

使用此接口确认收货并将订单置为完成状态

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| orderIds         | String   | 是 | 子单号，请以，(英文逗号)分割   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.2 取消未确认订单

**接口地址：**

/order/cancel

**接口说明：**

取消未确认订单接口

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.3 查询完成订单列表

**接口地址：**

/order/checkCompleteOrder

**接口说明：**

查询所有完成的订单列表。可用于核对订单。

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.4 查询妥投订单列表

**接口地址：**

/order/checkDlokOrder

**接口说明：**

查询所有妥投的订单列表。可用于核对订单

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.5 查询新建订单列表

**接口地址：**

/order/checkNewOrder

**接口说明：**

查询所有新建的订单列表。可用于核对订单

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.6 查询拒收订单列表

**接口地址：**

/order/checkRefuseOrder

**接口说明：**

查询所有拒收的订单列表。可用于核对订单

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.7 确认预占库存订单

**接口地址：**

/order/confirmOrder

**接口说明：**

确认预占库存订单接口

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.8 确认收货

**接口地址：**

/order/confirmReceived

**接口说明：**

可使用此接口确认收货并将订单置为完成状态

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.9 查询订单详情

**接口地址：**

/order/getDetail

**接口说明：**

查询订单信息接口

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.10 查询运费

**接口地址：**

/order/getFreight

**接口说明：**

查询准备提交的订单的运费

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.11 查询配送预计送达时间

**接口地址：**

/order/getPromiseTips

**接口说明：**

 查询商品配送预计送达时间

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.12 查询配送信息

**接口地址：**

/order/orderTrack

**接口说明：**

查询配送信息

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---

#### 4.13 提交订单

**接口地址：**

/order/submitOrder

**接口说明：**

提交订单信息,生产订单

**应用级参数Body：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| address         | String   | 是 | 地址   |

**响应参数result：**

| **字段**   | **类型**     | **必填** | **描述** |
| :---------   | :-----   | :---- | :----------- |
| provinceId         | Integer   | 是 | 一级地址ID    |
| province         | String   | 是 | 一级地址ID    |
| cityId         | Integer   | 是 | 二级地址ID    |
| city         | String   | 是 | 二级地址名称    |
| countyId         | Integer   | 是 | 三级地址ID    |
| county         | String   | 是 | 三级地址名称    |
| townId         | Integer   | 是 | 四级地址ID    |
| town         | String   | 是 | 四级地址名称    |

---
