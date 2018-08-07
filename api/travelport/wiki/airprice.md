# Request

# **TypeInventoryRequest\(機票庫存查詢類型\)**

Seamless：将在预订尝试之前轮询参与1P无缝库存的运营商以确认库存。

DirectAccess：将在预订尝试之前轮询参与直接访问库存和Worldspan（1P）无缝库存的运营商以确认库存。

Basic：从本地可用性来源获取数据。最接近于不检查1P中的可用性。如果在Galileo（1G）或Apollo（1V）中选择了Basic，则不会检查库存。

# TypeEticketability\(電子機票類型\)

Yes：可以獲取通過電子票務發送的行程。

NO：行程不能用電子機票出票，僅返回具有Paper票證的行程。

Required：僅返回可以通過電子票務發送的行程。

Ticketless：票務不適用於此運營商/解決方案。

---

# Respone

## AirPricingSolution

* ### AirPricingInfo
* * #### PricingMethod

    對應傳參有以下種類：

    Auto , Manual , ManualFare , Guaranteed , Invalid , Restored , Ticketed , Unticketable , Reprice , Expired , AutoUsingPrivateFare , GuaranteedUsingAirlinePrivateFare , Airline , AgentAssisted , VerifyPrice , AltSegmentRemovedReprice , AuxiliarySegmentRemovedReprice , DuplicateSegmentRemovedReprice , Unknown , GuaranteedUsingAgencyPrivateFare , AutoRapidReprice

    #### PricingType

    #### FareInfo

    * PrivateFare
      對應的類型：UnknownType , PrivateFare , AgencyPrivateFare , AirlinePrivateFare



