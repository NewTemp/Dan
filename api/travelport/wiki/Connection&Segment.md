# Connection Segment Logic

---

如果在Low Fare Shopping/Air Availability的響應中返回了Connection/SegmentIndex，它表示兩個鍋多個航段之間的連接。在Pricing和Booking時，必須使用連接指示器以確保正確的銷售航班，並且不會銷售失敗。

連接邏輯適用於Air Pricing和Air Booking。連接段索引信息返回到Low Fare Shopping/Air Availability響應作為一組數據。

      &lt;air:Connection SegmentIndex="0" /&gt;

      &lt;air:Connection SegmentIndex="1" /&gt;

      &lt;air:Connection SegmentIndex="3" /&gt;

      &lt;air:Connection SegmentIndex="4" /&gt;

SegmentIndex顯示了連接指示器必須存在的航段。SegmentIndex的值等於航段列表中的AirSegment的位置，这是一个航空定价解决方案的一部分。例如，使用Low Fare Shopping返回上述航段列表：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SegmentIndex="0" would link to the air segment in the first position in the list.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SegmentIndex="1" would link to the air segment in the second position in the list.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SegmentIndex="3" would link to the air segment in the fourth position in the list.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SegmentIndex="4" would link to the air segment in the fifth position in the list.



