# Drawjuliaset

## 一、	背景
使用 GCC、GAS、GDB 與 Code::Blocks，撰寫 ARM 組合語言程式，並在包含 ARM 處理器之電腦環境中驗證執行。

參考資料: 組合語言與嵌入式系統課程講義

https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/623180/

https://www.youtube.com/watch?v=07ATOG5wXPE

https://jasonblog.github.io/note/arm/101.html

## 二、	方法
以Code::Blocks環境另開Assembly專案，參考了課程講義和其它的網站及影片，完成分組名單印出及ID加總的要求，又利用debugging功能下的cpu register 、disassembly得到memory address 的位址及其變化等等，以此來完成這次組合語言與嵌入式系統的midterm project。

## 三、	結果
### (1)	程式說明：
將程式分成drawJuliaSet.s和main.c兩個部分，並和name.s、id.s四個檔案一起編譯。
#### name.s的功能為：
將環境及事先輸入的組員名字分行印出並結束。

#### id.s的功能為：
印出環境及讀入三位組員的id並讀入指令，以指令是否將id加總並結束。

#### drawJuliaSet.s的功能為：
將傳入的參數依造公式計算，將計算的結果填入frame的二維陣列，使螢幕產生不同變化的顏色。

#### main.c的功能為：
呼叫name、id和drawJuliaSet，在印出Happy New Year等字。

### (2)	設計重點說明：
#### name.s：
將事先需要的資料分行，並利用指令逐行印出。

#### id.s：
讀入所需資料，並加入判斷式判斷id加總，其餘等name.s。

#### drawJuliaSet.s：
因為這個函式需要傳入五個參數，但是可使用的暫存器只有r0-r3，所以第五個參數會被存到sp，所以當我們在備份使用到的暫存器之前，要先把sp裡面存的參數取出來。這次使用到的除法是利用反組譯，找到在v6指令中呼叫除法的方法。最後frame陣列是用算的，找到frame的起始位址後，因為一開始宣告是half word，所以是每一格是2個bytes，列式出來就是( y * width + x ) * 2，最後就能輸出圖形。

#### main.c：
先呼叫name，再呼叫id，最後呼叫drawJuliaSet，最後因為需要所有資料，因此將前述name.s和id.s內所需資訊設為全域，並在main中使用並印出，drawJuliaSet則是需要另外傳入參數。



