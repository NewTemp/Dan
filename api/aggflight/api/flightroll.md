* [ ] # flightRoll

## 1.1 入参

| 名称 | 类型 | 是否必填 | 描述 |
| ---: | :--- | :---: | :--- |
| requestKey | String | Y | 轮询Redis的Key。 |

## 1.2 出参

| 名称 | 类型 | 是否必填 | 描述 |
| ---: | :--- | :---: | :--- |
| requestKey | String | Y | 轮询Redis的Key。 |
| code | String | Y | 代码。0：表示从Redis获取数据成功；1：表示Redis没有数据，需要轮训。其他表示各种错误。 |
| message | String | Y | 消息 |
| apiType | Enum | Y | api类型，目前为Trp。 |
| apiData | Object | Y | api返回的数据，Trp使用LowFareSearchRsp来反序列化。 |

## 1.3 API逻辑

* 根据requestKey从Redis中查询
* 如果有，则直接返回0；
* 如果没有，则返回1;
* 如果Error，返回其他Code。



