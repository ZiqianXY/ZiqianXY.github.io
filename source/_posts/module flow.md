---
title: OBD-Service module-flow
date: 2016-05-20
type: "tags"
tags:
- OBD
---

### 流程图

```flow
st=>start: 点火
init=>operation: 初始化
e=>end: 结束
op=>operation: 查询车辆实时信息
save=>inputoutput: 写入SD卡
update=>subroutine: 上传数据
cond=>condition: 熄火？
check=>condition: 有WIFI？

st->init->op->save(right)->check
check(no,right)->cond
check(yes)->update
update(right)->cond
cond(no)->op
cond(yes,down)->e
```
