---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 剖析合約
{: #contract_parsing}

「元素分類」會傳回已剖析的合約，以及每個已識別元素的分析。

下列各節說明所傳回的 JSON 如何提供分析。

## Types
{: #contract_types}

`types` 陣列包括一些物件，每一個物件都包含 `nature` 和 `party` 索引鍵，其值可識別元素的聯體。

下列各表列出 `nature` 及 `party` 索引鍵的可能值。

| `nature`         |說明                                                       |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |此元素使條款、關係或類似項目更加明確。不需執行任何動作即可履行該元素，也不會有任何參與方受到影響。|
|`Disclaimer`      |此元素中的 `party` 沒有義務履行該元素所指定的條款，但不會禁止其履行。|
|`Exclusion`       |此元素中的 `party` 將不會履行該元素所指定的條款。|
|`Obligation`      |此元素中的 `party` 必須履行該元素所指定的條款。|
|`Right`           |此元素中的 `party` 保證會收到該元素所指定的條款。|

每個 `nature` 索引鍵都與一個 `party` 索引鍵配對，其包含適用於本質之參與方的名稱或角色（範例包括但不限於 `buyer`、`IBM` 或 `All Parties`）。請注意，針對 `Definition` 本質，參與方一律為 `None`。

## Parties
{: #contract_parties}

個別的 `parties` 陣列指定合約中列出的參與者。每個已識別的 `party` 物件會依名稱列出所識別的參與方，並與 `role` 相配，以將 `party` 物件的角色分類。針對合約可傳回的 `role` 值包括但不限於：

| `role`           |說明                                                       |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |負責支付合約中所列商品或服務的參與方。|
|`End User`        |將與所提供商品或服務互動的參與方，與 `Buyer` 明確有所區別。|
|`None`            |未識別元素的任何參與方。|
|`Supplier`        |負責提供合約中所列商品或服務的參與方。|

## Categories
{: #contract_categories}

`categories` 陣列定義句子的主題。目前支援的種類包括：

| `categories`     |說明                                                       |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |該元素指定在簽署合約之後的合約變更或標準合約變動。包括變更合約條款之條件的討論。|
|`Asset Use`       |該元素指出參與方可以或不可以使用另一方的資產。這特別適用於依據合約行使職責（包括之後的許可和限制）的過程中可以存取或使用另一方之資產（例如授權、設備、工具或人員）的參與方。這並未擴及參與方對於任何所購買商品、服務、授權等的義務或權利指定，因為這些是該參與方本身的資產，而非另一方的資產。|
|`Assignments`     |該元素說明將權利、義務或兩者轉移給第三方。|
|`Audits`          |該元素是指參與方檢查或檢閱合規性之權利，或參與方可供檢驗或進行合規性檢閱的需求。這包括對記錄保留（主要與檢驗的權利相關）的參照，以及可檢查之活動記錄的維護和保留。|
|`Business Continuity`|該元素是指其中一個參與方的完整業務出售時的結果。|
|`Communication`  |該元素是指溝通、回應、通知或提供通知、聯絡資訊或合約變更相關資訊等的需求。也包括對下列項目的參照：溝通方法、交換資訊的行動或過程，以及各方（含不一定為合約直接參與方的其他人）彼此交換資訊的可接受方式。|
|`Confidentiality` |該元素說明參與方可以或不可以使用在完成合約及繼續履行過程中所獲得的資訊。也包括必須保密之資訊的討論，例如維護商業機密或商業資訊的保密。|
|`Deliverables`    |該元素指定一個參與方依據合約條款而提供給另一方的項目（例如商品或服務），通常用於交換付款。包括準備交付項目的討論。|
|`Delivery`        |該元素指定將交付項目（物品，而不是個人服務）從一個參與方轉移給另一方的方法或模式。包括交付性質的討論，例如排程或位置。|
|`Dispute Resolution`|該元素討論解決合約參與方之間出現之任何爭議（例如，關於勞工、發票或計費）的條款。條款範例可能包括由已定義的程序（例如，仲裁小組）解決，這是一種取得禁制令、放棄審判權利或禁止尋求集體訴訟的處理程序。也包括合約之準據法或法律選擇的參照，例如特定國家或適用範圍。|
|`Force Majeure`   |該元素指出參與方無法掌控之非預期事件或破壞事件，使該參與方免於履行其合約責任。|
|`Indemnification` |該元素指定某些負債的補救，即合約的一個參與方因為在合約期間或因合約情況所引起的損失或損害而變成要負責補償另一方。也包括損失或損害之任何法律豁免的參照。|
|`Insurance`       |該元素指出一個參與方提供給另一方（包括給第三方，例如轉包商或其他人）的承保範圍或承保條款。包括各種保險（包括但不限於醫療保險）。|
|`Intellectual Property`|該元素討論對合約雙方之權利指派（例如，著作權、專利及商業機密）。包括專利、專利之權利、商標、商號、服務商標、網域名稱、著作權，以及對此等示意圖、產業模式、發明、著作權、專門技術、商業機密、電腦軟體程式和其他無形專屬資訊之一切應用和註冊的參照。也包括違反智慧財產權之結果的討論。|
|`Liability`       |該元素說明決定何時及如何將責任歸究於任一參與方的方法。範例可包括但不限於：關於責任限制、第三方理賠，以及對責任方要求之維修、更換或賠償的聲明。|
|`Payment Terms & Billing`|該元素詳述參與方如何及何時支付或獲得支付，以及參與方將支付或收費的項目或費用。包括付款模式或付款機制的參照。|
|`Pricing & Taxes` |該元素指出為滿足合約條款而交易之個別交付項目相關聯的具體金額或數字（例如，某項目的成本）。包括計算價格或稅額之具體數字或方法的參照。|
|`Privacy`         |該元素特別關注機密個人資訊的處理，通常是關於其保護（例如，為了符合 GDPR 之類的規定）。|
|`Responsibilities`|該元素討論從屬於合約且僅由一個參與方控制的任務，其特別著重在員工監督的討論。|
|`Safety and Security`|該元素指出人員、資料或系統的實體安全或網路安全保護。範例包括討論背景檢查、安全預防措施、工作場所安全、安全存取通訊協定，以及可能造成危險的產品瑕疵。|
|`Scope of Work`   |該元素定義合約中有哪些內容以及沒有哪些內容；從而定義承諾執行的事項。範例包括定義特定訂單或說明合約所概述之目標的聲明。|
|`Subcontracts`    |該元素指出雇用第三方依據合約執行特定義務，以及許可權、權利、限制和由此產生的後果。|
|`Term & Termination`|該元素指出合約有效天數、時程和合約終止條款，以及終止的任何後果，包括終止時或終止後所適用的任何義務。|
|`Warranties`      |該元素指出合約所做之持續承諾和義務，現在和未來均是如此。另有元素探討未能履行此等承諾或義務的後果，以及補救該狀況的權利（例如尋求賠償，但不限於此）。此種類不適用於純粹關注表述聲明（有關過去或現在事實的陳述）的元素，或提出關於過去所發生事項之假設的元素。|

## 屬性
{: #attributes}

`attributes` 陣列指定句子中識別的所有屬性。陣列中的每個物件包括三個索引鍵：`type`（下表中的屬性類型）、`text`（適用的文字），以及 `location`（輸入文件中屬性的 `begin` 和 `end` 索引）。目前支援的屬性包括：

| `attributes`     |說明                                                       |
|:----------------:|-----------------------------------------------------------|
|`Location`        |地理位置或地區。                                           |
|`DateTime`        |日期、時間、日期範圍或時間範圍。                           |
|`Currency`        |貨幣值和單位。                                             |

## 起源
{: #provenance}

`types` 及 `categories` 陣列中的每個物件都包含 `provenance_ids` 陣列。`provenance_ids` 陣列有一個以上的索引鍵。每個索引鍵是一個雜湊值，您可以將它傳送給 IBM 以提供意見或取得支援。
