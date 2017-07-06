---

title: try-with-resources
date: 2017-06-27 11:19:20
tags: I/O 流

---

>try-with-resources 是 Java7 加入的新特性，实际上就是一个语法糖，负责自动调用资源的 close() 函数

例如：

```
static String readFirstLineFromFile(String path) throws IOException {  
    try (BufferedReader br = new BufferedReader(new FileReader(path))) {  
        return br.readLine();  
    }  
} 
```

这种在try后面加个括号，再初始化对象的语法就叫try-with-resources

参考链接：

[http://blog.csdn.net/hengyunabc/article/details/18459463](http://blog.csdn.net/hengyunabc/article/details/18459463)

----------

在IDEA中使用 try-with-resource 时，遇到 java complier 过低不支持该语法糖的问题，解决方案就是进 setting 找到 java complier 选择卡，把项目的 java complier 调到 1.7 以上即可解决
