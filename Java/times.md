---
title: 检查一个字符串每个字符出现的次数
date: 2017-02-22 22:30:09
tags: 算法
---

```
var Str = "hellohellohello";
var newStr = Str.split("").sort();
function times(Str) {
	for (var i = 0; i < len; i = lastIndex+1) {
		var key = newStr[i];
		var lastIndex = newStr.join("").lastIndexOf(key);
        var count = lastIndex + 1 - i;
        console.log(key+"出现了"+ count +"次");
    }
}
times(Str);
```