# awk -- 学习笔记

*author: hsuh*

*creating time: 2020-12-11*

*finishing time: 2020-待定*

*modifying time: 暂无*

*reference:*

​	[awk 18个经典实战案例精讲 -- 骏马金龙](https://www.bilibili.com/video/BV1BJ411X7QN?from=search&seid=9023339601076451823)

---

## Cases

1、插入新字段 + 格式化空白

在"a b c d"的"b"后面插入3个字段"e  f g"

```shell
echo "a b c d" | awk '{ $2 = $2" e f g"; print }'
# a b e f g c d
```

修改字段或者`NF`，会根据`OFS`重建`$0`

例如，对`$2`使用原值赋值，会根据`OFS`（默认为" "，一个空格）重建`$0`。因此可以起格式化空白的作用

```shell
echo "a       b  c        d" | awk '{ $2 = $2; print }'
# a b c d
```

 移除每行的前缀、后缀空白，并将各部分左对齐：

```
            aaaa            bbb       ccc          
      bbb             aaa     ccc
 ddd            fff                 eee  gg   hh  ii  jj
```

代码如下，

```shell
awk 'BEGIN { OFS ="\t" } { $1 = $1; print }' case1_insert_format.txt
```

结果如下，

```
aaaa    bbb     ccc
bbb     aaa     ccc
ddd     fff     eee     gg      hh      ii      jj
```

2、





4、根据字段进行去重

去掉`case4_dedup_1.txt`中`uid=xxx`重复的行。

```
2019-01-13_12:00_index?uid=123
2019-01-13_13:00_index?uid=123
2019-01-13_14:00_index?uid=333
2019-01-13_15:00_index?uid=9710
2019-01-14_12:00_index?uid=123
2019-01-14_13:00_index?uid=123
2019-01-15_14:00_index?uid=333
2019-01-16_15:00_index?uid=9710
```

answer 1，

```shell
awk -F "?" '{ arr[$2] = arr[$2] + 1; if (arr[$2] == 1) { print } }' case4_dedup_1.txt
```

answer 2，

```shell
awk -F "?" '{ arr[$2]++; if (arr[$2] == 1) { print } }' case4_dedup_1.txt
```

anwser 3，

```shell
# 因为++放在后面
# 第一次出现，arr[$2]为1，但整个arr[$2]++返回0，取反为1，打印输出
# 后面出现，arr[$2]为2，但整个arr[$2]++返回1，取反为0，不打印输出
awk -F "?" '!arr[$2]++ { print }' case4_dedup_1.txt
```

5、指定数组遍历顺序

```
PROCINFO["sorted_in"]="@val_num_desc"
```

14、去掉`/**/`中间的注释

示例数据，

```
/*AAAAAAAAAA*/
1111
222

/*aaaaaaaaa*/
32323
12341234
12134 /*bbbbbbbbbb*/ 132412

14534122
/*
cccccccccc
*/
xxxxxx /*ddddddddddd
    cccccccccc
    eeeeeee
ddddd*/ yyyyyyyy
5642341
```

结果要求为，

```

1111
222


32323
12341234
12134  132412

14534122



xxxxxx 
    
    
 yyyyyyyy
5642341
```

代码如下，

```shell
##### 方法一，正则表达式寻找包含'/*'的行
# '/'和'*'均为元字符，放在'//'内作为正则表达式需要使用\进行转义
/\/\*/ {}

##### 方法二，使用index()进行查找
#  '/'和'*'均为元字符，但'/'放在'""'内作为正则表达式不需要使用\进行转义
index($0, "/*") {
    # 如果'*/'与'/*'在同一行
    if(index($0, "*/")) {
        # gensub(regexp, replacement, mode, string)
        # ^.*   .*开头
        # /*    匹配'/'和'*'
        # .*    匹配任意单个字符
        # */    匹配'*'和'/'
        # .*$   .*结尾
        # 两组()是进行分组捕获
        print gensub("^(.*)/\\*.*\\*/(.*)$", "\\1\\2", "g", $0)
    } else {
        # '*/'与'/*'不同行

        # 输出'/*'前面的内容
        print gensub("^(.*)/\\*.*", "\\1", "g", $0)
        
        # 继续读取，直到遇到'*/'结束符
        while((getline var) > 0) {
            if(index(var, "*/")) {
                print gensub("^.*\\*/(.*)", "\\1", "g", var)
                break
            }
        }
    }
}
# 不匹配'/*'的行直接输出
!index($0, "/*") {
    print
}
```

