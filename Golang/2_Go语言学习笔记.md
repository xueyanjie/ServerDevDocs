# Go语言学习笔记 qq:940358344

## 数据类型转换

## Map应用
### 判断map中的元素是否存在

```GO
dict := map[string]int{}
if _, ok := map["key"]; !ok {
    //key不存在于map中
}
```
