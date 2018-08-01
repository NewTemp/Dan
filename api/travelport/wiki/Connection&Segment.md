# Connection Segment Logic

---

如果在Low Fare Shopping/Air Availability的響應中返回了Connection/SegmentIndex，它表示兩個或多個航段之間的連接（也就是中轉）。在Pricing和Booking時，必須使用連接指示器（中轉標誌）以確保正確的銷售航班，並且不會銷售失敗。

連接邏輯適用於Air Pricing和Air Booking。連接段索引信息返回到Low Fare Shopping/Air Availability響應作為一組數據。

```
  <air:Connection SegmentIndex="0">
  <air:Connection SegmentIndex="1">
  <air:Connection SegmentIndex="3">
  <air:Connection SegmentIndex="4">
```

SegmentIndex顯示了連接指示器必須存在的航段。SegmentIndex的值等於航段列表中的AirSegment的位置，这是一个航空定价解决方案的一部分。例如，使用Low Fare Shopping返回上述航段列表：

```
  SegmentIndex="0" 將連接到列表中的第1個位置的航段。
  SegmentIndex="1" 將連接到列表中的第2個位置的航段。
  SegmentIndex="3" 將連接到列表中的第4個位置的航段。
  SegmentIndex="4" 將連接到列表中的第5個位置的航段。
```

注意：只有顯示&lt;air:Connection SegmentIndex="\#"&gt;的元素才是連接。如果作為連接元素的一部分存在中途停留規範，它不認為是一種連接，而是旅程的終點。這意味著類似於&lt;air:Connection StopOver="true" SegmentIndex="3"/&gt;這樣的元素不是連接。



#### 示例

* 一個**Air Availability request**可能返回一個帶有連接指示器（中轉標誌）的航班。

下面這個例子中，AirItinerarySolution需要4個連接指示器，也就是4個中轉。

請注意AirItinerarySolution中的Connection / SegmentIndex指標。AirSegmentRef的key可用於查找確切的航班。

![](/assets/1.png)



