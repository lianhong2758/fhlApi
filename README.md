## fhlAPI

- 飞花令是中国从古流传至今的一项游戏,本API支持的玩法如下
    
- 梦笔生花：
    - 题目为单字或二字词，玩家轮流说出带有该字或词的诗句。
    - 对应modtype A
- 走马观花：
    - 题目为一句诗句（可选择 5—9 的字数），其中的字按顺序依次作为关键字，玩家轮流各自说出包含当前关键字的诗句。
    - 对应modtype B
- 天女散花：
    - 题目为一组固定字词与一组可消去字词（可选择“1 词 + 10 词”或“3 词 + 16 词”），玩家轮流从两组字词中各选择一个，说出同时含有两者的诗句。每个消去词只能被选择一次。
    - 对应modtype C
- 雾里看花：
    - 题目为两组字词（可选择每组 5—10 词）。玩家轮流从两组字词中各选择一个，说出同时含有两者的诗句。所有词都只能被选择一次。
    - 对应modtype D

## 接口如下
```
1. 获取题目
示例
GET localhost:8080/gettopic
{
    "modtype":"B", //游戏种类
    "size":5,
    "id":"test_1"//用户自己长传一个id作为标识
}

result
{
  "code": 200,
  "message": "OK", //err
  "data": {
    "modtype": "B",
    "size": 5,
    "id": "test_1",
    "subjectstring": "江花作意新/0" //题目
  }
}
```
```
2. 提交答案
示例
GET localhost:8080/answer
{
    "id":"test_1",// 获取题目上传的ID
    "text":"北风卷地百草折" //答案
}
注:默认假设为两人游戏,用返回值的user的值0/1区分,也可以根据history%2计算

result
{
  "code": 200,
  "message": "",
  "data": {
    "modtype": "B",
    "size": 5,
    "id": "test_1",
    "subjectstring": "江花作意新/0",//题目
    "text": "",     //回答的语句
    "update": "",   //特殊标识
    "history": [],  //历史正确回答
    "user": 0,
    "reason": "大文豪"//回答不合题意的原因
  }
}
```
- update字段解释: 
- "update": "",    // A: 没有更新
- "update": "1",   // B: 表示接下来轮到的玩家需要飞的字
- "update": "4",   // C: 用到的可消除字
- "update": "0,4", // D: 左边和右边用到的字

## 鸣谢:
- https://github.com/kuriko1023/fhl?tab=readme-ov-file