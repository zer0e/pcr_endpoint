# pcr_endpoint
**持续施工中...**   
**本项目仅供学习交流使用，不得用于任何商业用途，使用本项目所产生的后果和责任与作者无关**


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
**后续大部分接口都存在viewer_id这个请求参数，故可能不会特意指出。**
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

### 生成简介卡
`/profile_maker/get_my_profile`


## 主页相关
### 获取付费物品列表 
`/payment/item_list`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| viewer_id | String | 可选 |

### 获取任务列表
`/mission/index`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|request_flag| Dict | 可选 意义不明|
| viewer_id | String | 可选 |

### 获取礼物箱列表
`/present/index`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|time_filter| int | 收取期限 -1全部 0无期限 1有期限|
| type_filter | int | 礼物种类 0全部 1宝石2碎片以此类推 |
| desc_flag | Boolean | False从旧到新 True从新到旧 |
| viewer_id | String | 可选 |


##角色相关
### 技能升级
`/skill/level_up`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|unit_id | int | 角色id |
|skill_levelup_list | List | 每个item由一个字典组成 例如{'location': 101, 'step': 1, 'current_level': 1}，location为101,201,202,301分别对应四个技能，step为提升等级数量|
| viewer_id | String | 可选 |

### 装备穿戴（有整件） 
`/unit/equip`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|unit_id| int | 角色id |
| equip_slot_num | int | 穿戴部位，顺序为从左到右，从上到下依次为1-6|
| viewer_id | String | 可选 |

### 装备穿戴（碎片合成）
`/unit/craft_equip`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|unit_id| int | 角色id |
| equip_slot_num | int | 穿戴部位，顺序为从左到右，从上到下依次为1-6|
| equip_recipe_list | List | 装备合成列表 例如[{'id': 115221, 'count': 35}]|
| viewer_id | String | 可选 |

### 装备强化
`/equipment/enhance`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| unit_id | int | 角色id |
| equip_slot_num | int | 穿戴部位，顺序为从左到右，从上到下依次为1-6|
| item_list | List | 使用的强化物品列表 例如[{'id': 22001, 'type': 2, 'count': 4}, {'id': 22002, 'type': 2, 'count': 2}] |
| current_enhancement_pt | int | 强化前装备经验值 |
| viewer_id | String | 可选 |


### rank提升
`/unit/multi_promotion`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| unit_id | int | 角色id |
| target_promotion_level | int | 目标rank |
| equip_recipe_list | List | 需要的装备物品列表 |
| item_list | List | 意义不明，猜测是使用物品提升rank? |
| viewer_id | String | 可选 |

### 等级提升
`/item/exp`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|unit_id| int | 角色id |
| item_list | List | 例如[{'item_id': 20001, 'item_num': 10, 'current_num': 503}] item_id为20001-2004，item_num为使用数量，current_num为使用前数量|
| viewer_id | String | 可选 |

### 星级提升
`/unit/evolution`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
|unit_id| int | 角色id |
|current_unit_rarity| int | 角色当前rank |
| viewer_id | String | 可选 |

### 专用武器装备
TODO


## 剧情相关

### 进入剧情
`/story/check`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| story_id | int | 剧情id |
| viewer_id | String | 可选 |


### 结束剧情
`/story/start`  
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| story_id | int | 剧情id |
| viewer_id | String | 可选 |


## 冒险相关

### 主线关卡战斗


### 探索关卡战斗


### 圣迹调查战斗


### 获取剧情活动主页
`/event/hatsune/top`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| event_id | int | 剧情活动id |
| viewer_id | String | 可选 |


### 获取剧情活动关卡信息
`/event/hatsune/quest_top`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| event_id | int | 剧情活动id |
| viewer_id | String | 可选 |

### 剧情活动扭蛋主页
`/event/hatsune/gacha_index`
| 参数    | 类型  | 说明      |
| ------- | ------ | ------- |
| event_id | int | 剧情活动id |
| gacha_id | int | 扭蛋id |
| viewer_id | String | 可选 |

### 剧情活动扭蛋操作

### 剧情关卡战斗

## 地下城相关

## 竞技场相关


## 公主竞技场相关


## 公会小屋相关


## 扭蛋相关

## 行会相关