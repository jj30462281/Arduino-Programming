# if判斷式 與 while for迴圈

### 注意：此篇章為前幾篇各種資料的綜合運用
#### 閱讀過後或了解了再來閱讀此篇內容

## 一、if 判斷式

`格式: if(布林值)`

簡單來說 就是 給予 if 的布林值 為 true 就執行

```C++
if(true) {
    Serial.println("hey hey!"); //因為給予 if 的布林值為 true 因此會執行到此行
}
```

與 if 匹配的還有 else 若 if 不符合 將會執行到 else

```C++
if(false) {
    Serial.println("hey hey!"); //給予 if 的布林值為 false 因此不會執行到此行
}
else {
    Serial.println("boy"); //給予匹配的 if 的布林值為 false 因此執行到此行
}
```

另外可以有更複雜的結構

```C++
if(false) {
    Serial.println("a"); //給予 if 的布林值為 false 因此不會執行到此行
}
else { //因此執行到這
    if(true) {
        Serial.println("b"); //給予 if 的布林值為 true 因此執行到此行
    }
    else {
        Serial.println("c"); //給予 if 的布林值為 true 因此不會執行到此行
    }
}
```

以上 Code 也可以簡化為

```C++
if(false) {
    Serial.println("a"); //給予 if 的布林值為 false 因此不會執行到此行
}
else if(true) {
    Serial.println("b"); //給予 if 的布林值為 true 因此執行到此行
}
else {
    Serial.println("c"); //給予 if 的布林值為 true 因此不會執行到此行
}
```

`補充: 大括弧的用意是創建出一個 Code Block 讓程式辨識出哪區塊的 Code 是到這 Block 該執行的`
`故如果只有一行 Code 是可以省略的`

```C++
if(false) Serial.println("a");  //給予 if 的布林值為 false 因此不會執行到此行
else if(true) Serial.println("b"); //給予 if 的布林值為 true 因此執行到此行
else Serial.println("c"); //給予 if 的布林值為 true 因此不會執行到此行
```

不過寫成這樣的話 Code 很難看

可以的話盡量寫成比較容易讀懂的樣子

## 二、while 迴圈

`格式: while(布林值)`

如果給予 while 的布林值為 true

就執行下面的 Code Block 或是 程式

```C++
while(true) {
    Serial.println("a"); //因為給予的布林值為 true 且不會改變 因此會重複循環印出 a
}
```

且迴圈也可跟 其他結構 如 if 結合

```C++
while(true) {
    if(false) {
        Serial.println("a"); //給予if的布林值為 false 因此永遠不會執行到此行
    }
}
```

另外也可加入變數運算

```C++
bool b = false;
while(true) { //無窮迴圈
    if(b) {
        Serial.println("a"); //如果 b 為 true 執行此行
    }
    else {
        Serial.println("b"); //如果 b 為 false 執行此行
    }

    b = !b; //使 b 為 NOT b

    //因 b 會一直與 NOT b 做切換
    //因此每執行完一次 while 迴圈 b 就會 NOT 一次
    //會變成 false, true, false, true, false, true, f........
    //這樣無限循環下去
    //因此印出的內容就會是 a, b, a, b, a, b, a, b.......
    //這樣子做切換
}
```

與上面敘述的 Code Block 一樣

如 Code 只有一行 也可以不用使用大括弧

```C++
int n = 10;
while(n) n--; //每執行一次while n 就遞減
//直到 n == 0 停止
//0 => false

Serial.println(n); //印出 0
```

# 三、for 迴圈

for 與 while 同為迴圈 但架構有些許不同

`格式: for(起始函式 ; 布林值 ; 結束函式)`

起始函式 - 在整個 for 迴圈只會被執行一次

布林值 - 每次 for 迴圈執行完時都會再次判斷 如true 則繼續迴圈 否則離開

結束函式 - 每次 for 迴圈執行完都會執行結束函式 之後才是判斷布林值

```C++
for(int i = 0 ; i < 20 ; i++) {
    //起始函式 - 執行定義 i = 0
    //布林值   - i < 20
    //結束函式 - i 遞增 1

    Serial.println(i); //印出 i

    //因此執行結果就是
    //1, 2, 3, 4, 5........19
    //接著就是結束這個迴圈
}
```

當然 給予 for 迴圈的參數也可不填 將會是個無窮迴圈 

```C++
for(;;) {
    Serial.println("a"); //無窮迴圈 印出 a
}
```

## 四、for 與 while 迴圈的 break 與 continue

break 與 continue 是只能用在迴圈裡的物件

break 的用處為 跳出整個迴圈

continue 的用處為 停止此次執行 直接執行下一次迴圈

因此可衍伸出以下用法

```C++
for(int i = 0 ; i < 20 ; i++) {
    if(i == 5) continue;

    Serial.println(i);

    //在 i == 5 時 執行了 continue 一次
    //在 continue 以下的 code 都會執行不到
    //因此執行結果為
    //1, 2, 3, 4, 6 ....... 20
}
```

```C++
for(int i = 0 ; i < 20 ; i++) {
    if(i == 5) break;

    Serial.println(i);
    
    //在 i == 5 時執行了 break 一次
    //在 break 之後就會停止此次並且直接跳出迴圈 
    //因此執行結果為
    //1, 2, 3, 4
    //因為 i == 5 而 break 而跳出了 for 迴圈
}
```

## 五、延伸閱讀

[一次看懂遞迴(Recursion) 的思維模式（一） - Medium](https://medium.com/appworks-school/%E9%80%B2%E5%85%A5%E9%81%9E%E8%BF%B4-recursion-%E7%9A%84%E4%B8%96%E7%95%8C-%E4%B8%80-59fa4b394ef6)

`我不寫迴圈拉！！！！ JOJO`

## 六、本篇重點節錄

![meme](https://pbs.twimg.com/media/DyiD_yYWkAYJ3Bi?format=jpg)

拜託 IG 別再推薦給我這種爛到爆的程式笑話了