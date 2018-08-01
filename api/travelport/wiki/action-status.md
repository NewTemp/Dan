# Action Status\(活動狀態\)

---

##### 除了ACTIVE之外，用戶設置的所有狀態都可以在UR中修改

* **ACTIVE**

       在即使購買的情況下，將ACH\(_Airline Content Hub_\)請求設置為“ACTIVE”。

* **TAW**

  ```
    _Ticket At Will. _設置將PNR放在售票隊列上的時間，PNR不會自動出票，只是放在隊列中。
    注意：需要相應的_TicketDate_屬性。
  ```

* **TTL**

  ```
    Ticket Time Limit. 設置將PNR放在售票隊列上的時間，PNR不會自動出票，只是放在隊列中。通常，
    選擇“TTL”值，以便在出現問題或者
  不出票時自動取消PNR。
    注意：需要相應的TicketDate屬性。
  ```

* **TAU**

  ```
    _Arrange Ticketing Date. _相當於_Worldspan_中的TAX\(稅\)。
  ```

* **Unknown**

  ```
    默認的操作類型，如果在請求中未指定操作類型。等效于_Galileo_中的'T/'。
  ```

##### 无法修改的其他系统生成状态

* **TLCXL**

  ```
    _Canceled by TTL._表示PNR的TTL时间已到期，系统自动取消航段\(AirSegment\)。
  ```

* **ACTIVE**

  ```
    表示PNR處於活動狀態，表示PNR已被出票，現在是代理/代理商的責任，系統不會嘗試進行任何下一步
    的操作。
  ```

* **CXL**

  ```
   _ Canceled._收到了PNR的取消請求，不會採取進一步行動。
  ```

### NODE

状态码“ACTIVE”表示PNR是当前的并且在某种程度上是活动的。但是，单个状态代码并不能完全代表实际的票务状态。

比如：PNR可以包含几个乘客，每个乘客都有一个电子票据记录（ETR）。但是，如果PNR中的一名乘客的预订通过排除和重新登记，取消，交换，退款或其他修改而被修改，则PNR保持“活动”并且是活动的并且能够采取其他行动。然后，在'Active'PNR中的每个乘客的个人票务状态在**DocumentInfo**元素中表示。

客户端应用程序可以将“活动状态”更改回“TTL”或“TAW”（如果已重新销售分段，退还故障单或进行其他修改）。然后，系统将PNR视为先前自动取消或自动票证队列放置。
