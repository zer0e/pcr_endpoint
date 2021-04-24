# pcr_endpoint
**持续施工中...**

## 登录相关

### 获取维护信息 
`/source_ini/get_maintenance_status?format=json`  
无加密，意在获取manifest版本存放至header中的MANIFEST-VER，否则无法进行后续操作。

### 登录 
`/tool/sdk_login`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| uid | String | 用户uid |
| access_key| String | 从平台登录获取 |
| channel | String | 固定为1 |
| platform | String | 固定为2 |

### 检查协议
`/check/check_agreement`

### 游戏前检查
`/check/game_start`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| apptype | int | 固定为0 |
| campaign_data| String | 固定为空字符串 |
| campaign_user | int | 0-99999 随机数 |


----------
**后续大部分操作需要登陆并进行游戏检查！！！**
## 用户信息相关

### 获取个人游戏所有信息
`/load/index`  
该接口可在检查之前  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| carrier | String | 为手机品牌 可为空|

### 获取主页信息
`/home/index`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| message_id | int | 固定为1 |
| tips_id_list | List | 固定为空列表 |
| is_first | int | 0或1 0代表数据已缓存到本地数据库，服务器不返回 |
| gold_history | int | 固定为0 |

### 获取指定用户简介信息
`/profile/get_profile`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| target_viewer_id | int | 查询用户的id |

