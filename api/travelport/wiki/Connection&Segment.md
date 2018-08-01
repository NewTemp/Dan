# Connection Segment Logic

---

如果在Low Fare Shopping/Air Availability的響應中返回了Connection/SegmentIndex，它表示兩個鍋多個航段之間的連接。在Pricing和Booking時，必須使用連接指示器以確保正確的銷售航班，並且不會銷售失敗。

連接邏輯適用於Air Pricing和Air Booking。連接段索引信息返回到Low Fare Shopping/Air Availability響應作為一組數據。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;air:Connection SegmentIndex="0" /&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;air:Connection SegmentIndex="1" /&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;air:Connection SegmentIndex="3" /&gt;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;air:Connection SegmentIndex="4" /&gt;





