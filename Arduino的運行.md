# Arduino 的運行

#### 提醒： 牽扯到的延伸內容太多 略...(絕對不是我懶)
#### 閱讀過後或了解了再來閱讀此篇內容

## 一、Arduino 執行的必要項目

Arduino 首先必要的就是先有兩個基礎函式

分別是 setup, loop

因此 一開始的Arduino 將會是

```C++
void setup() {

}

void loop() {

}

//此 Code 不會執行任何東西
//但可以通過 Arduino 刷入 Arduino
```

兩個函式的執行時機也如名稱

setup (只有開啟時初始化一次)

loop (無限迴圈運行)

因此基本上 Arudino 的執行會是

```C++
void setup() {

}

void loop() {
    
}

void main() {
    setup(); //setup 只執行一次
    while(true) {
        loop(); //無限迴圈執行 loop
    }
}
```

## 二、ino 是什麼？

ino 就是專給 Arduino 的程式檔

一個 sketch 中可能包含 ino

那要怎麼看你的ino呢？

就在 Editor 的上方

![ino](https://i.imgur.com/OoV8LIP.png)

當將程式碼傳入 ino 時

所有 ino 的程式都會被合併

若
```C++
//a.ino

int foo() {
    return 2;
}
```

```C++
//b.ino

void setup() {
    int a = foo();
    Serial.begin(9600);
    Serial.println(a); //印出 2
}

void loop() {

}
```

這是個有效的 Code

故如果 a.ino 與 b.ino 都有相同的變數或函式等

程式就會報錯 因為會相互衝突

## 三、變數的宣告 與 Code Block

在寫 Arduino 的時候，你或許遇過這樣的情形

```C++
void setup() {
    Serial.begin(9600);

    int a = 0;
}

void loop() {
    Serial.println(a) // error......;
}

//程式錯誤 無法上傳
```

因為變數的宣告 是只能在宣告範圍以下的 Code Block 進行使用的

在上面的敘述中 loop 與 setup 兩個 Code Block 並無相互關聯的關係

故 a 無法在 loop 中運行

因此變數必須這樣使用

```C++
int a = 0;

void setup() {
    Serial.begin(9600);
    
    a = 1;
}

void loop() {
    Serial.println(a); //印出 1
}
```

因為 setup 與 loop 的 Code Block 都在 a 之下

因此兩者都能夠存取到 a

當然 在相同層或更下層也可以

```C++
void setup() {
    Serial.begin(9600);

    int a = 0;
    Serial.println(a); //印出 0;

    if(!a) {
        Serial.println(a); //印出 0
    }
}

void loop() {

}
```

但 當然無法在宣告之前就使用變數

```C++
void setup() {
    Serial.begin(9600);

    Serial.println(a);
    int a = 0;
}

//在 a 被宣告之前就嘗試印出 a 絕對出錯
```

## 四、Arduino 的基本函式

請注意 **大寫要大寫 小寫要小寫** 別打錯

`digitalWrite(Pin, Mode)` 在指定 Pin 口寫入 Mode 狀態

Pin 為刻在板子上面的那些端口 Mode 為 HIGH or LOW (高電位或低電位)

`digitalRead(Pin)` 指定 Pin 口 為高電位還是低電位 (可檢測電路是否通路)

`analogWrite(Pin, val)` 在指定 Pin 口寫入指定數值(0 ~ 1023) 代表輸出的電壓大小 (Pin 口需為類比腳位)

`analogRead(Pin)` 讀取指定 Pin 口的類比數值

`delay(ms)` 程式暫停 ms毫秒

其餘內容請參照 [Arduino Reference](https://www.arduino.cc/reference/en/)

現在，你們會了以上內容，該是自己寫出自己的 Arduino 專案的時候了！！！

## 五、小試身手

現在 你目前在 Arudino 上的 Pin 4 上面裝了一個按鈕

按鈕未按下去為斷路

按下去後則為通路

請寫出一程式

在通路的時候 印出 "Pin 4!!!"

私訊我LINE詢問答案是否正確 ^^

## 六、延伸閱讀

[基礎但不簡單：變數命名規則 - Medium](https://medium.com/%E7%A8%8B%E5%BC%8F%E6%84%9B%E5%A5%BD%E8%80%85/%E8%AE%8A%E6%95%B8%E5%91%BD%E5%90%8D-f53cd1115076)

## 七、本篇重點節錄

![meme](https://pbs.twimg.com/media/ElOY5IaXUAUQOFF?format=jpg)

Arduino 刷不上去一定都是因為信仰問題！！！

LuoLuo對吧？