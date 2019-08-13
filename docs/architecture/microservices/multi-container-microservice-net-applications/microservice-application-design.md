---
title: 設計微服務導向應用程式
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解微服務導向應用程式的優點和缺點，讓您能夠採取明智的決策。
ms.date: 10/02/2018
ms.openlocfilehash: dfb1619bab68814bd14224e5b50a75d99525a802
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675965"
---
# <a name="designing-a-microservice-oriented-application"></a>設計微服務導向應用程式

本節旨在開發假設的伺服器端企業應用程式。

## <a name="application-specifications"></a>應用程式規格

假設的應用程式處理要求的方式是執行商務邏輯、存取資料庫，然後傳回 HTML、JSON 或 XML 回應。 假設應用程式必須支援各種用戶端，包括執行單頁應用程式 (SPA)、傳統 Web 應用程式、Mobile Web 應用程式和原生行動應用程式的桌面瀏覽器。 應用程式也可能會公開 API 給第三方取用。 它也應該能夠以非同步方式來整合其微服務或外部應用程式，此方法有助於在發生部分失敗時復原微服務。

應用程式會包含下列類型的元件：

- 展示元件。 這些元件會負責處理 UI 及取用遠端服務。

- 領域或商務邏輯。 這是應用程式的領域邏輯。

- 資料庫存取邏輯。 這包含負責存取資料庫 (SQL 或 NoSQL) 的資料存取元件。

- 應用程式整合邏輯。 這包含傳訊通道，主要是以訊息代理程式為基礎。

此應用程式需要高延展性，同時允許其垂直子系統自主擴充，因為某些子系統需要比其他子系統更多的延展性。

應用程式必須能夠部署在多個基礎結構環境中 (多個公用雲端和內部部署)，而且在理想情況下應該可跨平台，能夠輕鬆地從 Linux 移至 Windows (反之亦然)。

## <a name="development-team-context"></a>開發小組內容

我們對應用程式的開發程序還有以下假設：

- 您有多個開發小組，著重於應用程式的不同商務區域。

- 新的小組成員必須更快提高生產力，而且應用程式必須容易了解和修改。

- 應用程式會長期開發並有不斷改變的商務規則。

- 您需要能夠適當的長期維護，也就是彈性地在未來實作新變更，同時能夠在對其他子系統影響最低的情況下更新多個子系統。

- 您想要練習應用程式的持續整合與持續部署。

- 您想要在開發應用程式時利用新興技術 (架構、程式設計語言等)。 您不想要在移至新技術時完整移轉應用程式，因為這會導致高成本並影響應用程式的可預測性和穩定性。

## <a name="choosing-an-architecture"></a>選擇架構

應用程式部署架構應該為何？ 應用程式的規格 (以及開發內容) 強烈建議，您應該將應用程式分解成微服務和容器共同作業形式的自發子系統來架構應用程式，其中微服務就是容器。

在此方法中，每個服務 (容器) 會實作一組內聚且密切相關的功能。 例如，應用程式可能包含多個服務，例如目錄服務、訂購服務、購物籃服務、使用者設定檔服務等等。

微服務會盡可能使用 HTTP (REST) 等通訊協定但以非同步方式 (例如使用 AMQP) 通訊，特別是使用整合事件傳播更新時。

微服務會當做彼此獨立的容器進行開發和部署。 這表示開發小組可以開發及部署特定微服務，而不會影響其他子系統。

每個微服務都有自己的資料庫，因此可與其他微服務完全分離。 必要時，請使用應用程式層級整合事件 (透過邏輯事件匯流排)，來達成不同微服務的資料庫之間的一致性，如同命令與查詢職責分離 (Command and Query Responsibility Segregation，CQRS) 中的處理方式。 因此，商務限制式必須在多個微服務與相關資料庫之間採用最終一致性。

### <a name="eshoponcontainers-a-reference-application-for-net-core-and-microservices-deployed-using-containers"></a>eShopOnContainers：.NET Core 及使用容器部署之微服務的參考應用程式

您可以專注於架構和技術，相對於考慮使用您可能不知道的假設公司領域，我們選取了已知的公司領域，也就是呈現產品目錄、從客戶取得訂單、確認庫存及執行其他商務功能的簡化電子商務 (電子商店) 應用程式。 此容器應用程式原始程式碼位於 [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) GitHub 存放庫中。

此應用程式包含多個子系統，包括數個存放區 UI 前端 (Web 應用程式和原生行動應用程式)，以及用來執行所有必要伺服器端作業的後端微服務和容器 (使用數個 API 閘道作為內部微服務的合併進入點)。 圖 6-1 顯示參考應用程式的架構。

![行動和 SPA 用戶端會與單一 API 閘道端點通訊，而該閘道端點接著可與微服務通訊。 傳統的 Web 用戶端會與 MVC 微服務通訊，而該微服務可與其他微服務通訊](./media/image1.png)

**圖 6-1**. 開發環境的 eShopOnContainers 參考應用程式架構

**裝載環境**。 在圖 6-1 中，您會看到部署在單一 Docker 主機內的數個容器。 使用 docker-compose up 命令部署至單一 Docker 主機時，就是這種情況。 不過，如果您使用協調器或容器叢集，每個容器可能會在不同的主機 (節點) 中執行，而且任何節點可能會執行任何數目的容器，如稍早的＜架構＞一節中所述。

**通訊架構**。 eShopOnContainers 應用程式使用兩種通訊類型，視功能動作的類型而定 (查詢相對於更新和交易)：

- 用戶端與微服務透過 API 閘道的 HTTP 通訊。 這適用於查詢，以及接受來自用戶端應用程式的更新或交易式命令時。 使用 API 閘道的方法會在稍後的章節中詳細說明。

- 非同步事件型通訊。 這會透過事件匯流排來進行，以在微服務之間傳播更新或與外部應用程式整合。 事件匯流排可以使用任何傳訊代理程式基礎結構技術 (例如 RabbitMQ)，或使用高階 (抽象層級) 服務匯流排 (例如 Azure 服務匯流排、NServiceBus、MassTransit 或 Brighter) 來實作。

應用程式會部署為一組容器形式的微服務。 用戶端應用程式可以透過 API 閘道發佈的公用 URL，與這些執行為容器的微服務進行通訊。

### <a name="data-sovereignty-per-microservice"></a>每個微服務的資料自主性

在範例應用程式中，雖然所有 SQL Server 資料庫會部署為單一容器，但每個微服務都擁有自己的資料庫或資料來源。 此設計決策的制定只是為了方便開發人員從 GitHub 取得程式碼、將它複製，並在 Visual Studio 或 Visual Studio Code 中將它開啟。 或者，您可以輕鬆地使用 .NET Core CLI 和 the Docker CLI 來編譯自訂 Docker 映像，然後在 Docker 開發環境中部署及執行映像。 不論使用哪種方法，針對資料來源使用容器可讓開發人員在幾分鐘內建置及部署，而不需要佈建外部資料庫或在基礎結構 (雲端或內部部署) 上有硬式相依性的任何其他資料來源。

在實際生產環境中，若要取得高可用性和延展性，資料庫應該以雲端或內部部署 (而不是容器) 中的資料庫伺服器為基礎。

因此，微服務 (甚至是此應用程式中的資料庫) 的部署單位是 Docker 容器，而且參考應用程式是採用微服務原則的多容器應用程式。

### <a name="additional-resources"></a>其他資源

- **eShopOnContainers GitHub 存放庫：參考應用程式的原始程式碼**\
    <https://aka.ms/eShopOnContainers/>

## <a name="benefits-of-a-microservice-based-solution"></a>微服務架構解決方案的優點

這類微服務架構解決方案具有許多優點：

**每個微服務相對較小，因此管理和開發都很容易**。 尤其是：

- 開發人員輕鬆就能了解及快速開始使用，因此可提高生產力。

- 容器啟動速度很快，因此可提高開發人員的生產力。

- Visual Studio 之類的 IDE 可快速載入較小的專案，因此可提高開發人員的生產力。

- 每個微服務可以與其他微服務分開設計、開發及部署，由於更容易頻繁地部署新版微服務，因此更具彈性。

**可擴充應用程式的個別區域**。 例如，目錄服務或購物籃服務可能需要擴充，但訂購處理序則否。 微服務基礎結構對於處理擴充時所使用的資源，會比整合型架構更有效率。

**您可以在多個小組之間分配開發工作**。 每個服務可以由單一開發小組所擁有。 每個小組都可以與其他小組分開管理、開發、部署及擴充其服務。

**問題更具隔離性**。 如果某個服務有問題，一開始只會影響該服務 (除非是使用微服務之間有直接相依性的錯誤設計時)，而其他服務則可以繼續處理要求。 相較之下，整合型部署架構中的一個故障元件可能會讓整個系統故障，特別是當它涉及資源時，例如記憶體流失。 此外，當微服務中的問題解決之後，您可以只部署受影響的微服務，而不影響應用程式的其餘部分。

**您可以使用最新技術**。 因為您可以獨立開始開發及並排執行服務 (由於容器和 .NET Core)，所以可以輕鬆開始使用最新技術和架構，而不是整個應用程式卡在較舊的堆疊或架構中。

## <a name="downsides-of-a-microservice-based-solution"></a>微服務架構解決方案的缺點

這類微服務架構解決方案也有一些缺點：

**分散式應用程式**。 散發應用程式會增加開發人員設計和建置服務時的複雜度。 例如，開發人員必須使用 HTTP 或 AMPQ 等通訊協定來實作服務間的通訊，這會增加測試和例外狀況處理的複雜度， 也會增加系統的延遲。

**部署複雜度**。 應用程式若有數十種微服務類型並需要高延展性 (必須能夠針對每個服務建立許多執行個體，並在許多主機之間平衡這些服務)，則表示 IT 作業和管理的部署複雜度很高。 如果您未使用微服務導向基礎結構 (例如協調器和排程器)，額外的複雜性可能需要遠比商務應用程式本身更多的開發工作。

**不可部分完成交易**。 多個微服務之間的不可部分完成交易通常不可行。 商務需求必須在多個微服務之間採用最終一致性。

**增加的全域資源需求** (所有伺服器或主機的總記憶體、磁碟機和網路資源)。 在許多情況下，當您以微服務方法取代整合型應用程式時，新微服務架構應用程式所需之初始全域資源量會大於原始整合型應用程式的基礎結構需求。 這是因為資料粒度和分散式服務的程度越高，就需要越多的全域資源。 不過，由於相較於開發整合型應用程式時的長期執行成本，資源成本一般很低，而且具有能夠只擴充應用程式特定區域的優點，因此增加資源使用量通常會比長期執行的大型應用程式效果更佳。

**用戶端與微服務直接通訊的問題**。 當應用程式很大時 (具有數十個微服務)，如果應用程式需要用戶端與微服務直接通訊，則會帶來挑戰和限制。 一個問題是用戶端與每個微服務所公開之 API 的需求之間可能不符。 在某些情況下，用戶端應用程式可能需要提出許多個別要求來撰寫 UI，而透過網際網路的效能可能不佳，且不適合透過行動網路。 因此，您應該減少從用戶端應用程式對後端系統提出的要求。

用戶端與微服務直接通訊的另一個問題是，某些微服務可能會使用不支援 Web 的通訊協定。 一個服務可能會使用二進位通訊協定，而另一個服務可能會使用 AMQP 傳訊。 這些通訊協定不支援防火牆，因此最好在內部使用。 通常，應用程式應該使用 HTTP 和 WebSocket 等通訊協定，在防火牆外部進行通訊。

這種用戶端與微服務直接方法還有一個缺點，那就是很難重構這些微服務的合約。 過了一段時間，開發人員可能會想要變更系統分割成服務的方式。 例如，他們可能會合併兩個服務，或將一個服務分割成兩個或多個服務。 不過，如果用戶端會直接與服務通訊，執行這種重構可能會中斷與用戶端應用程式的相容性。

如＜架構＞一節中所述，設計及建置以微服務為基礎的複雜應用程式時，您可以考慮使用多個更精細的 API 閘道，而不是更簡單的用戶端與微服務直接通訊方法。

**分割微服務**。 最後，不論您對微服務架構採取哪種方法，另一項挑戰是決定如何將端對端應用程式分割成多個微服務。 如本指南的＜架構＞一節中所述，您可以採取數種技術和方法。 基本上，您需要識別與其他區域分離並具有較少硬式相依性的應用程式區域。 在許多情況下，這與依使用案例分割服務一致。 例如，在我們的電子商店應用程式中，我們有一個訂購服務，負責與訂購流程相關的所有商務邏輯。 我們也有實作其他功能的目錄服務和購物籃服務。 在理想情況下，每個服務只應該有一小組職責。 這類似於套用至類別的單一功能原則 (Single Responsibility Principle，SRP)，其中指出類別應該只有一個改變的原因。 但在此情況下，它與微服務相關，因此範圍會大於單一類別。 特別是微服務必須完全自主、端對端且包含其專屬資料來源的職責。

## <a name="external-versus-internal-architecture-and-design-patterns"></a>外部與內部架構和設計模式

外部架構是由多個服務所組成的微服務架構，並遵循本指南的＜架構＞一節中所述的原則。 不過，根據每個微服務的本質 (與您選擇的高階微服務架構無關)，通常且有時候最好擁有不同的內部架構，且每個架構是以不同的模式為基礎並針對不同的微服務。 這些微服務甚至可以使用不同的技術和程式設計語言。 圖 6-2 說明此多樣性。

![外部架構的差異：微服務模式、API 閘道、彈性通訊、pub/sub 等：內部架構：資料 動/CRUD、DDD 模式、相依性插入、多程式庫等。](./media/image2.png)

**圖 6-2**. 外部與內部架構和設計

例如，在我們的 *eShopOnContainers* 範例中，目錄、購物籃和使用者設定檔微服務很簡單 (基本上是 CRUD 子系統)。 因此，其內部架構和設計會很直接。 不過，您可能有其他微服務，例如訂購微服務，這些微服務更複雜，而且代表領域複雜度很高之不斷改變的商務規則。 在這些情況下，您可能會想要在特定微服務中實作更進階的模式 (例如以領域導向設計 (DDD) 方法定義的模式)，就像是我們在 *eShopOnContainers* 訂購微服務中一樣 (我們將在說明 *eShopOnContainers* 訂購微服務實作的稍後章節中檢閱這些 DDD 模式)。

您也可能會由於每個微服務的本質，而針對每個微服務使用不同的技術。 例如，您最好使用 F\# 等功能性程式設計語言，或甚至是 R 等語言 (如果您以 AI 和機器學習領域為目標)，而不是使用 C\# 等更物件導向的程式設計語言。

底線是每個微服務可以根據不同的設計模式擁有不同的內部架構。 並非所有微服務都應該使用進階 DDD 模式來實作，因為這會設計過當。 同樣地，具有不斷改變之商務邏輯的複雜微服務不應該實作為 CRUD 元件，否則您最後可能會有低品質的程式碼。

## <a name="the-new-world-multiple-architectural-patterns-and-polyglot-microservices"></a>新世界：多個架構模式和多種語言的微服務

軟體架構設計人員和開發人員使用的架構模式有許多種。 以下是其中一些 (混合架構樣式和架構模式)：

- 單一階層單層式的簡易 CRUD。

- [傳統 N 分層](https://docs.microsoft.com/previous-versions/msp-n-p/ee658109(v=pandp.10))。

- [領域導向設計 N 分層](https://blogs.msdn.microsoft.com/cesardelatorre/2011/07/03/published-first-alpha-version-of-domain-oriented-n-layered-architecture-v2-0/).

- [乾淨架構](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html) (可搭配 [eShopOnWeb](https://aka.ms/WebAppArchitecture) 使用)

- [命令與查詢職責分離](https://martinfowler.com/bliki/CQRS.html) (CQRS)。

- [事件驅動架構](https://en.wikipedia.org/wiki/Event-driven_architecture) (EDA)。

您也可以使用許多技術和語言來建置微服務，例如 ASP.NET Core Web API、NancyFx、ASP.NET Core SignalR (.NET Core 2 所提供)、F\#、Node.js、Python、Java、C++、GoLang 等等。

請注意，沒有特定架構模式或樣式，也沒有任何特定技術適合所有情況。 圖 6-3 顯示可用於不同微服務的一些方法和技術 (但不會依任何特定順序)。

![多個架構模式和多種語言的微服務，表示您可以根據每個微服務的需求混合搭配語言和技術，並仍然可以讓它們彼此通訊。](./media/image3.png)

**圖 6-3**. 多個架構模式和多種語言的微服務世界

如圖 6-3 所示，在由許多微服務 (以領域導向設計術語來說是限定內容，或只是作為自發微服務的「子系統」) 所組成的應用程式中，您可能會以不同方式來實作每個微服務。 根據應用程式的本質、商務需求和優先順序，每個微服務可能會有不同的架構模式，並使用不同的語言和資料庫。 在某些情況下，微服務可能很類似。 但並不一定總是如此，因為每個子系統的內容界限和需求通常不同。

例如，在簡易 CRUD 維護應用程式中，設計和實作 DDD 模式可能沒有任何意義。 但針對您的核心領域或核心商務，您可能需要套用更進階的模式，來處理不斷改變之商務規則的商務複雜度。

特別是當您處理由多個子系統所組成的大型應用程式時，您不應該根據單一架構模式來套用單一頂層架構。 例如，您不應該將 CQRS 套用為整個應用程式的頂層架構，但對特定一組服務而言可能有很用。

沒有適用於所有給定案例的靈丹或正確的架構模式。 您不可能會有「一個適用於所有案例的架構模式」。 根據每個微服務的優先順序，您必須針對每個微服務選擇不同的方法，如下列各節中所述。

>[!div class="step-by-step"]
>[上一頁](index.md)
>[下一頁](data-driven-crud-microservice.md)