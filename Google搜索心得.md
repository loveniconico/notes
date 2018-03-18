# Google搜索心得
本文件将记录我对Google搜索的的心得
## 关于关闭安全搜索
以下方法测试于2017年7月15日12点08分
### 方法一
输入地址`https://www.google.com/ncr`,然后进入搜索设置将搜索语言设置为English  
然后设置搜索引擎为`https://www.google.com/#q=%s&safe=off`  
或者是在地址栏输入`https://www.google.com/#q=你要搜索的词&safe=off`  

```
如上方法会看似可行但是较为麻烦,也无法完全关闭安全搜索,只是将搜索安全调至[适中]
如果你是搜索文字内容倒是没关系(在文字搜索下安全搜索的[关闭]和[适中]为同等级即内容相同)
但是进行图片搜索时安全搜索的[关闭]和[适中]搜索内容差别较大,具体方法请看方法二
```

### 方法二
> 方法来自[一個屁股引發的Google搜索技術討論及解決](http://weibo.com/p/1001603902207178194293)
#### 步骤 
1. 输入地址`https://www.google.com/ncr`,然后进入搜索设置将搜索语言设置为English  
2. 重新进入搜索设置,选择`Search results`
3. 点F12 打开浏览器的 Developer Tools窗口选择Element定位到 Turn on/off SafeSearch 单选框
然后你会发现单选框的HTML标签语言下有一行如下代码`<input value="images" name="safeui" type="hidden">`
，将其中的value="images" 或 “on” 这一项改为 off 即可如``<input value="off" name="safeui" type="hidden">``。
4. 然后关闭 Developer Tools窗口,最后保存。

# TODO 待更新其他,欢迎指正和补充
