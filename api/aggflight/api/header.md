# base request

| 名称 | 类型 | 是否必填 | 描述 |
| ---: | :--- | :---: | :--- |
| providers | List&lt;String&gt; | Y | 1G，1V等 |
| apiType | Enum | Y | 目前为Trp |
| targetBranch | String | Y | PCC |

# base response

| 名称 | 类型 | 是否必填 | 描述 |
| ---: | :--- | :---: | :--- |
| code | String | Y | 代码。0：表示从成功；1：表示需要轮训。其他表示各种错误。 |
| message | String | Y | 消息 |
| apiType | Enum | Y | api类型，目前为Trp。 |
| apiData | T | Y | api返回的数据，例如：Trp使用LowFareSearchRsp来反序列化。 |

