---
title: 載入資料
description: 載入資料檔案並將資料串流至 ML.NET
ms.date: 05/03/2019
ms.custom: mvc,how-to
ms.openlocfilehash: 6edcc92b610e2e1f5e21c371b9f0aefd0b216d31
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063655"
---
# <a name="load-data-from-file-and-in-memory-sources"></a><span data-ttu-id="04bcf-103">從檔案和記憶體內部來源載入資料</span><span class="sxs-lookup"><span data-stu-id="04bcf-103">Load data from file and in-memory sources</span></span>

<span data-ttu-id="04bcf-104">此操作說明教學會示範如何將資料載入 ML.NET 以進行處理和定型。</span><span class="sxs-lookup"><span data-stu-id="04bcf-104">This how-to shows you how to load data for processing and training into ML.NET.</span></span> <span data-ttu-id="04bcf-105">資料原本儲存在檔案中或即時/串流資料來源內。</span><span class="sxs-lookup"><span data-stu-id="04bcf-105">The data is originally stored in files or real-time / streaming data sources.</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="04bcf-106">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="04bcf-106">Create the data model</span></span>

<span data-ttu-id="04bcf-107">ML.NET 可讓您透過類別定義資料模型。</span><span class="sxs-lookup"><span data-stu-id="04bcf-107">ML.NET enables you to define data models via classes.</span></span> <span data-ttu-id="04bcf-108">例如，假設有下列的輸入資料：</span><span class="sxs-lookup"><span data-stu-id="04bcf-108">For example, given the following input data:</span></span>

```text
Size (Sq. ft.), HistoricalPrice1 ($), HistoricalPrice2 ($), HistoricalPrice3 ($), Current Price ($)
700, 100000, 3000000, 250000, 500000
1000, 600000, 400000, 650000, 700000
```

<span data-ttu-id="04bcf-109">建立資料模型以表示以下的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="04bcf-109">Create a data model that represents the snippet below:</span></span>

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }
 
    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

### <a name="annotating-the-data-model-with-column-attributes"></a><span data-ttu-id="04bcf-110">使用資料行屬性標註資料模型</span><span class="sxs-lookup"><span data-stu-id="04bcf-110">Annotating the data model with column attributes</span></span>

<span data-ttu-id="04bcf-111">屬性可提供 ML.NET 更多關於資料模型和資料來源的資訊。</span><span class="sxs-lookup"><span data-stu-id="04bcf-111">Attributes give ML.NET more information about the data model and the data source.</span></span>

<span data-ttu-id="04bcf-112">[`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) 屬性會指定您屬性的資料行索引。</span><span class="sxs-lookup"><span data-stu-id="04bcf-112">The [`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) attribute specifies your properties' column indices.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04bcf-113">[`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) 只有在從檔案載入資料時才需要。</span><span class="sxs-lookup"><span data-stu-id="04bcf-113">[`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) is only required when loading data from a file.</span></span>

<span data-ttu-id="04bcf-114">將資料行作為以下項目載入：</span><span class="sxs-lookup"><span data-stu-id="04bcf-114">Load columns as:</span></span> 
- <span data-ttu-id="04bcf-115">個別資料行，像是 `HousingData` 類別中的 `Size` 和 `CurrentPrices`。</span><span class="sxs-lookup"><span data-stu-id="04bcf-115">Individual columns like `Size` and `CurrentPrices` in the `HousingData` class.</span></span>
- <span data-ttu-id="04bcf-116">以類似 `HousingData` 類別中 `HistoricalPrices` 的向量形式，一次載入多個資料行。</span><span class="sxs-lookup"><span data-stu-id="04bcf-116">Multiple columns at a time in the form of a vector like `HistoricalPrices` in the `HousingData` class.</span></span>

<span data-ttu-id="04bcf-117">若您擁有向量屬性，請將 [`VectorType`](xref:Microsoft.ML.Data.VectorTypeAttribute) 屬性套用到您資料模型中的屬性。</span><span class="sxs-lookup"><span data-stu-id="04bcf-117">If you have a vector property, apply the [`VectorType`](xref:Microsoft.ML.Data.VectorTypeAttribute) attribute to the property in your data model.</span></span> <span data-ttu-id="04bcf-118">請務必注意，向量中的所有項目都必須是相同類型。</span><span class="sxs-lookup"><span data-stu-id="04bcf-118">It's important to note that all of the elements in the vector need to be the same type.</span></span>

<span data-ttu-id="04bcf-119">ML.NET 會透過資料行名稱運作。</span><span class="sxs-lookup"><span data-stu-id="04bcf-119">ML.NET Operates through column names.</span></span> <span data-ttu-id="04bcf-120">若您想要將資料行名稱變更為屬性名稱之外的名稱，請使用 [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) 屬性。</span><span class="sxs-lookup"><span data-stu-id="04bcf-120">If you want to change the name of a column to something other than the property name, use the [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) attribute.</span></span> <span data-ttu-id="04bcf-121">在建立記憶體內部物件時，您仍會使用屬性名稱建立物件。</span><span class="sxs-lookup"><span data-stu-id="04bcf-121">When creating in-memory objects, you still create objects using the property name.</span></span> <span data-ttu-id="04bcf-122">但是，針對資料處理和建置機器學習模型，ML.NET 會使用 [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) 屬性中提供的值來覆寫及參考屬性。</span><span class="sxs-lookup"><span data-stu-id="04bcf-122">However, for data processing and building machine learning models, ML.NET overrides and references the property with the value provided in the [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) attribute.</span></span>

## <a name="load-data-from-a-single-file"></a><span data-ttu-id="04bcf-123">從單一檔案載入資料</span><span class="sxs-lookup"><span data-stu-id="04bcf-123">Load data from a single file</span></span>

<span data-ttu-id="04bcf-124">若要從檔案載入資料，請搭配要載入其資料的資料模型使用 [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile*) 方法。</span><span class="sxs-lookup"><span data-stu-id="04bcf-124">To load data from a file use the [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile*) method along with the data model for the data to be loaded.</span></span> <span data-ttu-id="04bcf-125">因為 `separatorChar` 參數根據預設會以 Tab 鍵分隔，您可以視需要為您的資料檔案變更它。</span><span class="sxs-lookup"><span data-stu-id="04bcf-125">Since `separatorChar` parameter is tab-delimited by default, change it for your data file as needed.</span></span> <span data-ttu-id="04bcf-126">若您的檔案擁有標頭，請將 `hasHeader` 參數設為 `true` 來忽略檔案中的第一行，並從第二行開始載入資料。</span><span class="sxs-lookup"><span data-stu-id="04bcf-126">If your file has a header, set the `hasHeader` parameter to `true` to ignore the first line in the file and begin to load data from the second line.</span></span>

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

//Load Data
IDataView data = mlContext.Data.LoadFromTextFile<HousingData>("my-data-file.csv", separatorChar: ',', hasHeader: true);
```

## <a name="load-data-from-multiple-files"></a><span data-ttu-id="04bcf-127">從多個檔案載入資料</span><span class="sxs-lookup"><span data-stu-id="04bcf-127">Load data from multiple files</span></span>

<span data-ttu-id="04bcf-128">您的資料儲存在多個檔案，只要資料結構描述相同，ML.NET 可讓您將資料載入會在相同目錄中的多個檔案或多個目錄。</span><span class="sxs-lookup"><span data-stu-id="04bcf-128">In the event that your data is stored in multiple files, as long as the data schema is the same, ML.NET allows you to load data from multiple files that are either in the same directory or multiple directories.</span></span>

### <a name="load-from-files-in-a-single-directory"></a><span data-ttu-id="04bcf-129">從單一目錄中的檔案載入</span><span class="sxs-lookup"><span data-stu-id="04bcf-129">Load from files in a single directory</span></span>

<span data-ttu-id="04bcf-130">當您所有的資料檔案都位於相同目錄時，請在 [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile*) 方法中使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="04bcf-130">When all of your data files are in the same directory, use wildcards in the [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile*) method.</span></span>

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

//Load Data File
IDataView data = mlContext.Data.LoadFromTextFile<HousingData>("Data/*", separatorChar: ',', hasHeader: true);
```

### <a name="load-from-files-in-multiple-directories"></a><span data-ttu-id="04bcf-131">載入多個目錄中的檔案</span><span class="sxs-lookup"><span data-stu-id="04bcf-131">Load from files in multiple directories</span></span>

<span data-ttu-id="04bcf-132">若要從多個目錄載入資料，請使用 [`CreateTextLoader`](xref:Microsoft.ML.TextLoaderSaverCatalog.CreateTextLoader*) 方法來建立 [`TextLoader`](xref:Microsoft.ML.Data.TextLoader)。</span><span class="sxs-lookup"><span data-stu-id="04bcf-132">To load data from multiple directories, use the [`CreateTextLoader`](xref:Microsoft.ML.TextLoaderSaverCatalog.CreateTextLoader*) method to create a [`TextLoader`](xref:Microsoft.ML.Data.TextLoader).</span></span> <span data-ttu-id="04bcf-133">然後，請使用 [`TextLoader.Load`](xref:Microsoft.ML.DataLoaderExtensions.Load*) 方法並指定個別檔案路徑 (無法使用萬用字元)。</span><span class="sxs-lookup"><span data-stu-id="04bcf-133">Then, use the [`TextLoader.Load`](xref:Microsoft.ML.DataLoaderExtensions.Load*) method and specify the individual file paths (wildcards can't be used).</span></span>

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

// Create TextLoader
TextLoader textLoader = mlContext.Data.CreateTextLoader<HousingData>(separatorChar: ',', hasHeader: true);

// Load Data
IDataView data = textLoader.Load("DataFolder/SubFolder1/1.txt", "DataFolder/SubFolder2/1.txt");
```

## <a name="load-data-from-a-streaming-source"></a><span data-ttu-id="04bcf-134">從串流來源載入資料</span><span class="sxs-lookup"><span data-stu-id="04bcf-134">Load data from a streaming source</span></span>

<span data-ttu-id="04bcf-135">除了載入儲存在磁碟上的資料，ML.NET 支援從各種串流來源載入資料，其中包括但不限於：</span><span class="sxs-lookup"><span data-stu-id="04bcf-135">In addition to loading data stored on disk, ML.NET supports loading data from various streaming sources that include but are not limited to:</span></span>

- <span data-ttu-id="04bcf-136">記憶體內集合</span><span class="sxs-lookup"><span data-stu-id="04bcf-136">In-memory collections</span></span>
- <span data-ttu-id="04bcf-137">JSON/XML</span><span class="sxs-lookup"><span data-stu-id="04bcf-137">JSON/XML</span></span>
- <span data-ttu-id="04bcf-138">資料庫</span><span class="sxs-lookup"><span data-stu-id="04bcf-138">Databases</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04bcf-139">請注意，當使用串流來源時，ML.NET 預期輸入的形式為記憶體內部集合。</span><span class="sxs-lookup"><span data-stu-id="04bcf-139">Note that when working with streaming sources, ML.NET expects input to be in the form of an in-memory collection.</span></span> <span data-ttu-id="04bcf-140">因此，當使用像是 JSON/XML 等來源時，請務必將資料格式化成記憶體內部集合。</span><span class="sxs-lookup"><span data-stu-id="04bcf-140">Therefore, when working with sources like JSON/XML, make sure to format the data into an in-memory collection.</span></span>

<span data-ttu-id="04bcf-141">假設有下列記憶體內部集合：</span><span class="sxs-lookup"><span data-stu-id="04bcf-141">Given the following in-memory collection:</span></span>

```csharp
HousingData[] inMemoryCollection = new HousingData[]
{
    new HousingData
    {
        Size =700f,
        HistoricalPrices = new float[]
        {
            100000f, 3000000f, 250000f
        },
        CurrentPrice = 500000f
    },
    new HousingData
    {
        Size =1000f,
        HistoricalPrices = new float[]
        {
            600000f, 400000f, 650000f
        },
        CurrentPrice=700000f
    }
};
```

<span data-ttu-id="04bcf-142">請使用 [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable*) 方法將記憶體內部集合載入 [`IDataView`](xref:Microsoft.ML.IDataView)：</span><span class="sxs-lookup"><span data-stu-id="04bcf-142">Load the in-memory collection into an [`IDataView`](xref:Microsoft.ML.IDataView) with the [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable*) method:</span></span>

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

//Load Data
IDataView data = mlContext.Data.LoadFromEnumerable<HousingData>(inMemoryCollection);
```