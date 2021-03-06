# Azure 使用心得
## 概述
本人是國立台灣大學電機系的學生，由於修李宏毅老師的機器學習與及其深層與結構化(MLDS)課程，有幸使用到了Microsoft雲計算產品Azure (感謝Microsoft贊助本課程使用一定的金額)。

我在之前修過IoT的課程，當時課程有教如何使用Amazon的AWS，不過我主要是使用AWS的database服務，但也是可以與Azure做個簡單的對比，另外我也使用過阿里雲服務，但是阿里雲並沒有提供深度學習計算給學生，多數都是以架設服務器為主，但就比較一般計算雲服務的價格來說(差不多的配置)，阿里雲的價格還是相當吸引人的。

## 簡單的對比
**1.價格**
Azure在價格上沒有AWS來的實惠，不過兩者都有用多少付多少的功能，這個對於一般用戶來說還是很方便的。對於學生，可能更多的會在意價格。像是Azure的NC6主機，每小時就要NT$27.05, 所以200美金(贊助的額度)我每次差不多可以完成一次作業(平時都很節約的話)

我們算一下，現在市場上一台1080Ti(性能與NC6的Tesla差不多)顯卡售價約27萬新台幣。如果是一般的學生，那麼它使用1000個小時的Azure NC6主機(相當於41天)。這麼一算就很嚇人了，Azure一直開機41天就可以買一張1080Ti的顯卡了，那麼為什麼不直接買一張顯卡，我可以順心所欲的使用，等畢業了再轉手賣掉，這樣更加划算啊！！！

我個人覺得，微軟可以出個學生方案，或者與各大院校合作，為學生提供優惠的價格，其便利性還是可以吸引很多想我們這樣在學習深度學習的學生的。我們只需要一台輕量的小筆電就可以做很多事情了。

**2.操作介面**
Azure的操作介面我個人還是很喜歡的，使用起來簡單便捷，想要找什麼功能都能在左邊的功能欄裡找到。自己配置好的虛擬機也都在儀表盤上顯示出來。
![GitHub set up](https://github.com/RainyRen/azure_report/blob/master/image/aws.png)

相比之下，AWS的面板就有些簡陋，想找一些功能還要花點功夫才行啊
![GitHub set up](https://github.com/RainyRen/azure_report/blob/master/image/azure.png)

**3.連接方法**
Azure的可以選擇使用密碼或者ssh-key登錄，我們則一定選擇比較方便的密碼登錄。雖然最安全的一定是使用ssh-key，但是我們本來就不常開機，而且每次開機ip又都不一樣，只要把密碼設定複雜一點，已經足夠安全了。
AWS只允許使用ssh-key(至少去年我在使用的時候是這樣)，所以當我設定了一台電腦的pub-key後想要在用別的電腦連結就有些困難了。
這一點上，我還是很喜歡Azure的設定的。

## 我的使用感受
**以下都是針對Azure使用上面的一些感受**

### 環境
因為我本身就有在練習使用Ubuntu的command line，所以在配置Azure的工作環境(安裝CUDA，TensorFlow等)上面算是很順利。之後全部使用指令操作(從網址下載data，建立資料夾，刪除不需要的文件等)，有的時候會有小小的延遲，但是總體上來說還算是流暢。強烈建議在使用的時候使用screen，有的時候因為網路不好掉線的話，之前做的東西就全沒了，使用screen可以恢復先前的工作介面，還是可以開多個窗口，使用上非常方便。
*如已進入虛擬機，我會先下指令*：```screen```
*如果斷線了，那麼只需要執行*：


```
screen -ls # 列出screen在執行的窗口
screen -r <前面列出的編號> # 恢復對應的窗口
```

我也嘗試過在Azure上面安裝了輕量型的桌面環境(xfce4)，再利用mac自帶的VNC連接。速度非常的慢，非常不建議使用遠端桌面，要是想要玩好雲主機，還是好好學一下文字指令吧，你的工作效率也會提升很多。

如果你真的不熟悉配置環境，或者想要可以立即使用的話，可以選擇azure的*機器學習服務*，它都直接把環境幫你配置好，包括常用的各種深度學習庫，使用起來也是非常的便捷。時間就是金錢啊，免去配置環境的時間也相當於節約了很對錢呢～！

環境配置好了以後，你就可以本地編輯你的程序，之後再利用 ```scp``` 傳送到遠端虛擬機就可以，或者是直接在遠端利用vim編輯。不過我本人還是強烈建議在本地先寫好程序，做一些小的測試，最後沒有問題在丟到遠端虛擬機去跑。畢竟虛擬機開著就扣錢，不管你有沒有用到GPU(前面我也提到，Azure的價格讓你噴血啊～)，所以在本地寫程序的時候就關掉，只有在train的時候使用，這樣也會幫你省下很多錢。

其他的使用上和你使用ubuntu的終端機沒什麼大的區別，重要的就是熟悉那些常用的指令就好。

