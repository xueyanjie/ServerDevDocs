# Go语言学习笔记 qq:940358344

## 数据类型相关
### rune
byte与rune都属于别名类型。byte是uint8的别名类型，而rune是int32的别名类型。<br />
一个rune的类型值即可表示一个Unicode字符。一个Unicode代码点通常由"U+"和一个以十六进制表示法表示的整数表示，例如英文字母'A'的Unicode代码点为"U+0041"。<br/>
看如下示例程序
```GO
    str := "test 小薛" //默认utf-8编码，中文占用三字节
	line := fmt.Sprintf("length \"%s\" = %d", str, len(str))
	fmt.Println(line) //打印占用字节
	parts := []rune(str)
	for _, r := range parts {
		fmt.Print(string(r))
	}
	fmt.Println("")
	//rune的使用
	chr := 'a'
	fmt.Println(reflect.TypeOf(chr))
	
	//输出结果：
	/**
	    length "test 小薛" = 11
        test 小薛
        int32
	*/
```

### 数据类型转换

## Map应用
### 判断map中的元素是否存在

```GO
dict := map[string]int{}
if _, ok := map["key"]; !ok {
    //key不存在于map中
}
```
