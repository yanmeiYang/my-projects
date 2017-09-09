# API 说明

### ROSTER
| 请求方式 | API   | 说明 |
| --------  | -----:  | :----:  |
| GET     | api/roster/:id/offset/:offset/size/:size?rev=1   |   * id: roster的id, size: 最大为100, rev: 返回数据倒排，默认顺序新添加的专家在最后     |
| POST |   api/roster/:id   |   API说明   |