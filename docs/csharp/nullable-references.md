---
title: 可為 Null 的參考型別
description: 本文提供可為 Null 參考型別的概觀，這種型別是在 C# 8 中新增的功能。 您會了解此功能如何為新及現有的專案，針對 Null 參考例外狀況提供安全。
ms.date: 02/19/2019
ms.openlocfilehash: 9ce9efb890f0eff5a6c6747f96c143a4d093dbfb
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725021"
---
# <a name="nullable-reference-types"></a><span data-ttu-id="fc196-104">可為 Null 的參考型別</span><span class="sxs-lookup"><span data-stu-id="fc196-104">Nullable reference types</span></span>

<span data-ttu-id="fc196-105">C# 8.0 引進**可為 Null 的參考型別**及**不可為 Null 的參考型別**，可讓您針對參考型別變數的屬性撰寫相關重要陳述式：</span><span class="sxs-lookup"><span data-stu-id="fc196-105">C# 8.0 introduces **nullable reference types** and **non-nullable reference types** that enable you to make important statements about the properties for reference type variables:</span></span>

- <span data-ttu-id="fc196-106">**參考不應為 Null**。</span><span class="sxs-lookup"><span data-stu-id="fc196-106">**A reference is not supposed to be null**.</span></span> <span data-ttu-id="fc196-107">當變數不應為 Null 時，編譯器會實施規則，確保對這些變數取值 (Dereference) 的過程是安全的，而不會事先檢查這些變數是不是 Null：</span><span class="sxs-lookup"><span data-stu-id="fc196-107">When variables aren't supposed to be null, the compiler enforces rules that ensure it is safe to dereference these variables without first checking that it isn't null:</span></span>
  - <span data-ttu-id="fc196-108">變數必須初始化為非 Null 值。</span><span class="sxs-lookup"><span data-stu-id="fc196-108">The variable must be initialized to a non-null value.</span></span>
  - <span data-ttu-id="fc196-109">變數永遠不可指派 `null` 值。</span><span class="sxs-lookup"><span data-stu-id="fc196-109">The variable can never be assigned the value `null`.</span></span>
- <span data-ttu-id="fc196-110">**參考可能為 Null**。</span><span class="sxs-lookup"><span data-stu-id="fc196-110">**A reference may be null**.</span></span> <span data-ttu-id="fc196-111">當變數可為 Null 時，編譯器會實施不同的規則，確保您已針對 Null 參考正確地進行檢查：</span><span class="sxs-lookup"><span data-stu-id="fc196-111">When variables may be null, the compiler enforces different rules to ensure that you've correctly checked for a null reference:</span></span>
  - <span data-ttu-id="fc196-112">只有在編譯器能保證該值並非為 Null 時，才能對該變數進行取值 (Dereference)。</span><span class="sxs-lookup"><span data-stu-id="fc196-112">The variable may only be dereferenced when the compiler can guarantee that the value isn't null.</span></span>
  - <span data-ttu-id="fc196-113">這些變數可使用預設的 `null` 值初始化，也可以在其他程式碼中指派 `null` 值。</span><span class="sxs-lookup"><span data-stu-id="fc196-113">These variables may be initialized with the default `null` value and may be assigned the value `null` in other code.</span></span>

<span data-ttu-id="fc196-114">相較於先前版本 C# 中處理參考變數的方式，這項新功能提供極大的好處，因為先前版本中無法從變數宣告判斷設計意圖。</span><span class="sxs-lookup"><span data-stu-id="fc196-114">This new feature provides significant benefits over the handling of reference variables in earlier versions of C# where the design intent couldn't be determined from the variable declaration.</span></span> <span data-ttu-id="fc196-115">編譯器不針對參考型別的 Null 參考例外狀況提供安全：</span><span class="sxs-lookup"><span data-stu-id="fc196-115">The compiler didn't provide safety against null reference exceptions for reference types:</span></span>

- <span data-ttu-id="fc196-116">**參考可為 Null**。</span><span class="sxs-lookup"><span data-stu-id="fc196-116">**A reference can be null**.</span></span> <span data-ttu-id="fc196-117">不會在參考型別初始化為 Null，或是稍後指派為 Null 時發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-117">No warnings are issued when a reference type is initialized to null, or later assigned to null.</span></span>
- <span data-ttu-id="fc196-118">**參考已假設為並非 Null**。</span><span class="sxs-lookup"><span data-stu-id="fc196-118">**A reference is assumed to be not null**.</span></span> <span data-ttu-id="fc196-119">編譯器不會在對參考型別進行取值 (Dereference) 時發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-119">The compiler doesn't issue any warnings when reference types are dereferenced.</span></span> <span data-ttu-id="fc196-120">(使用可為 Null 參考，編譯器會在您對可能為 Null 的變數進行取值 (Dereference) 時發出警告)。</span><span class="sxs-lookup"><span data-stu-id="fc196-120">(With nullable references,  the compiler issues warnings whenever you dereference a variable that may be null).</span></span>

<span data-ttu-id="fc196-121">透過新增的可為 Null 參考型別，您可以更清楚地宣告您的意圖。</span><span class="sxs-lookup"><span data-stu-id="fc196-121">With the addition of nullable reference types, you can declare your intent more clearly.</span></span> <span data-ttu-id="fc196-122">`null` 值是表示變數並非指向某個值的正確方式。</span><span class="sxs-lookup"><span data-stu-id="fc196-122">The `null` value is the correct way to represent that a variable doesn't refer to a value.</span></span> <span data-ttu-id="fc196-123">請不要使用這項功能來從您的程式碼中移除所有 `null` 值。</span><span class="sxs-lookup"><span data-stu-id="fc196-123">Don't use this feature to remove all `null` values from your code.</span></span> <span data-ttu-id="fc196-124">相反地，您應該對編譯器及其他閱讀您程式碼之開發人員宣告您的意圖。</span><span class="sxs-lookup"><span data-stu-id="fc196-124">Rather, you should declare your intent to the compiler and other developers that read your code.</span></span> <span data-ttu-id="fc196-125">藉由宣告您的意圖，編譯器會在您撰寫的程式碼與該意圖不一致時通知您。</span><span class="sxs-lookup"><span data-stu-id="fc196-125">By declaring your intent, the compiler informs you when you write code that is inconsistent with that intent.</span></span>

<span data-ttu-id="fc196-126">**可為 Null 參考型別**的語法與[可為 Null 實值型別](programming-guide/nullable-types/index.md)語法相同：將 `?` 附加至變數的型別。</span><span class="sxs-lookup"><span data-stu-id="fc196-126">A **nullable reference type** is noted using the same syntax as [nullable value types](programming-guide/nullable-types/index.md): a `?` is appended to the type of the variable.</span></span> <span data-ttu-id="fc196-127">例如，下列變數宣告代表可為 Null 字串變數，`name`：</span><span class="sxs-lookup"><span data-stu-id="fc196-127">For example, the following variable declaration represents a nullable string variable, `name`:</span></span>

```csharp
string? name;
```

<span data-ttu-id="fc196-128">任何沒有在型別名稱附加 `?` 的變數都是**不可為 Null 參考型別**。</span><span class="sxs-lookup"><span data-stu-id="fc196-128">Any variable where the `?` is not appended to the type name is a **non-nullable reference type**.</span></span> <span data-ttu-id="fc196-129">這包含您啟用此功能時現有程式碼中所有的參考型別變數。</span><span class="sxs-lookup"><span data-stu-id="fc196-129">That includes all reference type variables in existing code when you have enabled this feature.</span></span>

<span data-ttu-id="fc196-130">編譯器會使用靜態分析來判斷可為 Null 參考是否已知並非為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-130">The compiler uses static analysis to determine if a nullable reference is known to be non-null.</span></span> <span data-ttu-id="fc196-131">若您在可為 Null 參考可能為 Null 時對其進行取值 (Dereference)，編譯器會警告您。</span><span class="sxs-lookup"><span data-stu-id="fc196-131">The compiler warns you if you dereference a nullable reference when it may be null.</span></span> <span data-ttu-id="fc196-132">您可以在變數名稱後使用 **Null 容許運算子** (`!`) 來覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="fc196-132">You can override this behavior by using the **null-forgiving operator** (`!`) following a variable name.</span></span> <span data-ttu-id="fc196-133">例如，若您知道 `name` 變數並非為 Null，但編譯器卻發出警告，您可以撰寫下列程式碼來覆寫編譯器的分析：</span><span class="sxs-lookup"><span data-stu-id="fc196-133">For example, if you know the `name` variable isn't null but the compiler issues a warning, you can write the following code to override the compiler's analysis:</span></span>

```csharp
name!.Length;
```

<span data-ttu-id="fc196-134">您可以在 GitHub 上的 [draft nullable reference types](../../_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator) (草稿可為 Null 參考型別) 規格提案中閱讀此運算子的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fc196-134">You can read details about this operator in the [draft nullable reference types](../../_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator) specification proposal on GitHub.</span></span>

## <a name="nullability-of-types"></a><span data-ttu-id="fc196-135">型別的可 NULL 性</span><span class="sxs-lookup"><span data-stu-id="fc196-135">Nullability of types</span></span>

<span data-ttu-id="fc196-136">任何參考型別都可擁有四種「可 NULL 性」中的其中一種，其描述警告產生的時機：</span><span class="sxs-lookup"><span data-stu-id="fc196-136">Any reference type can have one of four *nullabilities*, which describes when warnings are generated:</span></span>

- <span data-ttu-id="fc196-137">*不可為 Null*：不可將 Null 指派給此型別的變數。</span><span class="sxs-lookup"><span data-stu-id="fc196-137">*Nonnullable*: Null can't be assigned to variables of this type.</span></span> <span data-ttu-id="fc196-138">此型別的變數不需進行 Null 檢查即可進行取值 (Dereference)。</span><span class="sxs-lookup"><span data-stu-id="fc196-138">Variables of this type don't need to be null-checked before dereferencing.</span></span>
- <span data-ttu-id="fc196-139">*可為 Null*：可將 Null 指派給此型別的變數。</span><span class="sxs-lookup"><span data-stu-id="fc196-139">*Nullable*: Null can be assigned to variables of this type.</span></span> <span data-ttu-id="fc196-140">若沒有事先檢查是否為 `null` 即對此型別的變數進行取值 (Dereference)，即會產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-140">Dereferencing variables of this type without first checking for `null` causes a warning.</span></span>
- <span data-ttu-id="fc196-141">*遺忘*：此為 C# 8 之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="fc196-141">*Oblivious*: This is the pre-C# 8 state.</span></span> <span data-ttu-id="fc196-142">此型別的變數可進行取值或指派，且皆不會產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-142">Variables of this type can be dereferenced or assigned without warnings.</span></span>
- <span data-ttu-id="fc196-143">*未知*：這通常是針對限制式並未告知編譯器型別必須是「可為 Null」或「不可為 Null」的型別參數。</span><span class="sxs-lookup"><span data-stu-id="fc196-143">*Unknown*: This is generally for type parameters where constraints don't tell the compiler that the type must be *nullable* or *nonnullable*.</span></span>

<span data-ttu-id="fc196-144">變數宣告中型別的可 NULL 性會由宣告該變數的「可為 Null 內容」控制。</span><span class="sxs-lookup"><span data-stu-id="fc196-144">The nullability of a type in a variable declaration is controlled by the *nullable context* in which the variable is declared.</span></span>

## <a name="nullable-contexts"></a><span data-ttu-id="fc196-145">可為 Null 內容</span><span class="sxs-lookup"><span data-stu-id="fc196-145">Nullable contexts</span></span>

<span data-ttu-id="fc196-146">可為 Null 內容可讓您對編譯器解譯參考型別變數的方式進行細部控制。</span><span class="sxs-lookup"><span data-stu-id="fc196-146">Nullable contexts enable fine-grained control for how the compiler interprets reference type variables.</span></span> <span data-ttu-id="fc196-147">任何指定來源行的**可為 Null 註釋內容**都是 `enabled` 或 `disabled`。</span><span class="sxs-lookup"><span data-stu-id="fc196-147">The **nullable annotation context** of any given source line is `enabled` or `disabled`.</span></span> <span data-ttu-id="fc196-148">您可以將 C# 8 之前的編譯器想成是將您所有程式碼編譯在一個 `disabled` 可為 Null 內容中：任何參考型別都可能為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-148">You can think of the pre-C# 8 compiler as compiling all your code in a `disabled` nullable context: Any reference type may be null.</span></span> <span data-ttu-id="fc196-149">**可為 Null 警告內容** 可設為 `enabled`、`disabled` 或 `safeonly`。</span><span class="sxs-lookup"><span data-stu-id="fc196-149">The **nullable warnings context** may be set to `enabled`, `disabled`, or `safeonly`.</span></span> <span data-ttu-id="fc196-150">可為 Null 警告內容會指定編譯器使用其流程分析所產生的警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-150">The nullable warnings context specifies the warnings generated by the compiler using its flow analysis.</span></span>

<span data-ttu-id="fc196-151">可為 Null 註釋內容和可為 Null 警告內容都可在您的 `csproj` 檔案中使用 `NullableContextOptions` 項目來為專案設定。</span><span class="sxs-lookup"><span data-stu-id="fc196-151">The nullable annotation context and nullable warning context can be set for a project using the `NullableContextOptions` element in your `csproj` file.</span></span> <span data-ttu-id="fc196-152">此項目會設定編譯器解譯型別可 NULL 性的方式及所產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-152">This element configures how the compiler interprets the nullability of types and what warnings are generated.</span></span> <span data-ttu-id="fc196-153">有效的設定如下：</span><span class="sxs-lookup"><span data-stu-id="fc196-153">Valid settings are:</span></span>

- <span data-ttu-id="fc196-154">`enable`：可為 Null 註釋內容為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-154">`enable`: The nullable annotation context is **enabled**.</span></span> <span data-ttu-id="fc196-155">可為 Null 警告內容為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-155">The nullable warning context is **enabled**.</span></span>
  - <span data-ttu-id="fc196-156">參考型別變數 (例如 `string`) 不可為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-156">Variables of a reference type, `string` for example, are non-nullable.</span></span>  <span data-ttu-id="fc196-157">啟用所有可 NULL 性警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-157">All nullability warnings are enabled.</span></span>
- <span data-ttu-id="fc196-158">`disable`：可為 Null 註釋內容為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-158">`disable`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="fc196-159">可為 Null 警告內容為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-159">The nullable warning context is **disabled**.</span></span>
  - <span data-ttu-id="fc196-160">參考型別變數為遺忘式，與先前版本的 C# 相似。</span><span class="sxs-lookup"><span data-stu-id="fc196-160">Variables of a reference type are oblivious, just like earlier versions of C#.</span></span> <span data-ttu-id="fc196-161">停用所有可 NULL 性警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-161">All nullability warnings are disabled.</span></span>
- <span data-ttu-id="fc196-162">`safeonly`：可為 Null 註釋內容為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-162">`safeonly`: The nullable annotation context is **enabled**.</span></span> <span data-ttu-id="fc196-163">可為 Null 警告內容為**僅限安全**。</span><span class="sxs-lookup"><span data-stu-id="fc196-163">The nullable warning context is **safeonly**.</span></span>
  - <span data-ttu-id="fc196-164">參考型別變數不可為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-164">Variables of a reference type are nonnullable.</span></span> <span data-ttu-id="fc196-165">啟用所有安全可 NULL 性警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-165">All safety nullability warnings are enabled.</span></span>
- <span data-ttu-id="fc196-166">`warnings`：可為 Null 註釋內容為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-166">`warnings`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="fc196-167">可為 Null 警告內容為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-167">The nullable warning context is **enabled**.</span></span>
  - <span data-ttu-id="fc196-168">參考型別變數為遺忘式。</span><span class="sxs-lookup"><span data-stu-id="fc196-168">Variables of a reference type are oblivious.</span></span> <span data-ttu-id="fc196-169">啟用所有可 NULL 性警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-169">All nullability warnings are enabled.</span></span>
- <span data-ttu-id="fc196-170">`safeonlywarnings`：可為 Null 註釋內容為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-170">`safeonlywarnings`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="fc196-171">可為 Null 警告內容為**僅限安全**。</span><span class="sxs-lookup"><span data-stu-id="fc196-171">The nullable warning context is **safeonly**.</span></span>
  - <span data-ttu-id="fc196-172">參考型別變數為遺忘式。</span><span class="sxs-lookup"><span data-stu-id="fc196-172">Variables of a reference type are oblivious.</span></span> <span data-ttu-id="fc196-173">啟用所有安全可 NULL 性警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-173">All safety nullability warnings are enabled.</span></span>

<span data-ttu-id="fc196-174">您也可以使用指示詞，在您專案中的任何位置設定相同內容：</span><span class="sxs-lookup"><span data-stu-id="fc196-174">You can also use directives to set these same contexts anywhere in your project:</span></span>

- <span data-ttu-id="fc196-175">`#nullable enable`：將可為 Null 註釋內容及可為 Null 警告內容設為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-175">`#nullable enable`: Sets the nullable annotation context and nullable warning context to **enabled**.</span></span>
- <span data-ttu-id="fc196-176">`#nullable disable`：將可為 Null 註釋內容及可為 Null 警告內容設為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-176">`#nullable disable`: Sets the nullable annotation context and nullable warning context to **disabled**.</span></span>
- <span data-ttu-id="fc196-177">`#nullable safeonly`：將可為 Null 註釋內容設為**啟用**，將警告內容設為**僅限安全**。</span><span class="sxs-lookup"><span data-stu-id="fc196-177">`#nullable safeonly`: Set the nullable annotation context to **enabled**, and the warning context to **safeonly**.</span></span>
- <span data-ttu-id="fc196-178">`#nullable restore`：將可為 Null 註釋內容和可為 Null 警告內容還原至專案設定。</span><span class="sxs-lookup"><span data-stu-id="fc196-178">`#nullable restore`: Restores the nullable annotation context and nullable warning context to the project settings.</span></span>
- <span data-ttu-id="fc196-179">`#pragma warning disable nullable`：將可為 Null 警告內容設為**停用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-179">`#pragma warning disable nullable`: Set the nullable warning context to **disabled**.</span></span>
- <span data-ttu-id="fc196-180">`#pragma warning enable nullable`：將可為 Null 警告內容設為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="fc196-180">`#pragma warning enable nullable`: Set the nullable warning context to **enabled**.</span></span>
- <span data-ttu-id="fc196-181">`#pragma warning restore nullable`：將可為 Null 警告內容還原至專案設定。</span><span class="sxs-lookup"><span data-stu-id="fc196-181">`#pragma warning restore nullable`: Restores the nullable warning context to the project settings.</span></span>
- <span data-ttu-id="fc196-182">`#pragma warning safeonly nullable`：將可為 Null 警告內容設為**僅限安全**。</span><span class="sxs-lookup"><span data-stu-id="fc196-182">`#pragma warning safeonly nullable`: Sets the nullable warning context to **safeonly**.</span></span>

<span data-ttu-id="fc196-183">預設的可為 Null 註釋及警告內容為 `disabled`。</span><span class="sxs-lookup"><span data-stu-id="fc196-183">The default nullable annotation and warning contexts are `disabled`.</span></span> <span data-ttu-id="fc196-184">該決策表示您現有的程式碼會編譯且不會進行任何變更，也不會產生任何新的警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-184">That decision means that your existing code compiles without changes and without generating any new warnings.</span></span>

<span data-ttu-id="fc196-185">`enabled` 和 `safeonly` 差異點在於可為 Null 警告內容是將可為 Null 參考指派給不可為 Null 參考時的警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-185">The differences between the `enabled` and `safeonly` nullable warning contexts are warnings for assigning a nullable reference to a non-nullable reference.</span></span> <span data-ttu-id="fc196-186">下列指派會在一個 `enabled` 警告內容中產生警告，但不會在 `safeonly` 警告內容中產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-186">The following assignment generates a warning in an `enabled` warning context, but not a `safeonly` warning context.</span></span> <span data-ttu-id="fc196-187">但是，第二行 (對 `s` 進行取值 (Dereference)) 會在一個 `safeonly` 內容中產生警告：</span><span class="sxs-lookup"><span data-stu-id="fc196-187">However, the second line, where `s` is dereferenced, generates a warning in a `safeonly` context:</span></span>

```csharp
string s = null; // warning when nullable warning context is enabled.
var txt = s.ToString(); // warning when nullable warnings context is safeonly, or enabled.
```

### <a name="nullable-annotation-context"></a><span data-ttu-id="fc196-188">可為 Null 註釋內容</span><span class="sxs-lookup"><span data-stu-id="fc196-188">Nullable annotation context</span></span>

<span data-ttu-id="fc196-189">編譯器會在停用的可為 Null 註釋內容中使用下列規則：</span><span class="sxs-lookup"><span data-stu-id="fc196-189">The compiler uses the following rules in a disabled nullable annotation context:</span></span>

- <span data-ttu-id="fc196-190">您無法在停用的內容中宣告可為 Null 參考。</span><span class="sxs-lookup"><span data-stu-id="fc196-190">You can't declare nullable references in a disabled context.</span></span>
- <span data-ttu-id="fc196-191">所有參考變數都可指派為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-191">All reference variables may be assigned to null.</span></span>
- <span data-ttu-id="fc196-192">當對參考型別的變數進行取值 (Dereference) 時，不會產生任何警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-192">No warnings are generated when a variable of a reference type is dereferenced.</span></span>
- <span data-ttu-id="fc196-193">Null 容許運算子不可用於停用內容中。</span><span class="sxs-lookup"><span data-stu-id="fc196-193">The null-forgiving operator may not be used in a disabled context.</span></span>

<span data-ttu-id="fc196-194">行為與先前版本的 C# 相同。</span><span class="sxs-lookup"><span data-stu-id="fc196-194">The behavior is the same as previous versions of C#.</span></span>

<span data-ttu-id="fc196-195">編譯器會在啟用的可為 Null 註釋內容中使用下列規則：</span><span class="sxs-lookup"><span data-stu-id="fc196-195">The compiler uses the following rules in an enabled nullable annotation context:</span></span>

- <span data-ttu-id="fc196-196">參考型別的任何變數都是**不可為 Null 參考**。</span><span class="sxs-lookup"><span data-stu-id="fc196-196">Any variable of a reference type is a **non-nullable reference**.</span></span>
- <span data-ttu-id="fc196-197">任何不可為 Null 參考都可安全地進行取值 (Dereference)。</span><span class="sxs-lookup"><span data-stu-id="fc196-197">Any non-nullable reference may be dereferenced safely.</span></span>
- <span data-ttu-id="fc196-198">任何可為 Null 參考型別 (在變數宣告中的型別後方標註 `?`) 都可為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-198">Any nullable reference type (noted by `?` after the type in the variable declaration) may be null.</span></span> <span data-ttu-id="fc196-199">靜態分析會在對其進行取值 (Dereference) 時判斷該值是否已知並非為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-199">Static analysis determines if the value is known to be non-null when it is dereferenced.</span></span> <span data-ttu-id="fc196-200">若否，則編譯器會警告您。</span><span class="sxs-lookup"><span data-stu-id="fc196-200">If not, the compiler warns you.</span></span>
- <span data-ttu-id="fc196-201">您可以使用 Null 容許運算子來宣告可為 Null 參考並非為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-201">You can use the null-forgiving operator to declare that a nullable reference isn't null.</span></span>

<span data-ttu-id="fc196-202">在啟用的可為 Null 註釋內容中，`?` 字元會附加至宣告**可為 Null 參考型別**的參考型別。</span><span class="sxs-lookup"><span data-stu-id="fc196-202">In an enabled nullable annotation context, the `?` character appended to a reference type declares a **nullable reference type**.</span></span> <span data-ttu-id="fc196-203">**Null 容許運算子** (`!`) 可附加至運算式，來宣告運算式並非為 Null。</span><span class="sxs-lookup"><span data-stu-id="fc196-203">The **null forgiveness operator** (`!`) may be appended to an expression to declare that the expression isn't null.</span></span>

## <a name="nullable-warning-context"></a><span data-ttu-id="fc196-204">可為 Null 警告內容</span><span class="sxs-lookup"><span data-stu-id="fc196-204">Nullable warning context</span></span>

<span data-ttu-id="fc196-205">可為 Null 警告內容與可為 Null 註釋內容不同。</span><span class="sxs-lookup"><span data-stu-id="fc196-205">The nullable warning context is distinct from the nullable annotation context.</span></span> <span data-ttu-id="fc196-206">即使停用新的註釋，仍可啟用警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-206">Warnings can be enabled even when the new annotations are disabled.</span></span> <span data-ttu-id="fc196-207">編譯器會使用靜態分析來判斷任何參考的 **Null 狀態**。</span><span class="sxs-lookup"><span data-stu-id="fc196-207">The compiler uses static flow analysis to determine the **null state** of any reference.</span></span> <span data-ttu-id="fc196-208">當並未「停用」*可為 Null 警告內容*時，Null 狀態不是**並非為 Null**，就是**可能為 Null**。</span><span class="sxs-lookup"><span data-stu-id="fc196-208">The null state is either **not null** or **maybe null** when the *nullable warning context* isn't **disabled**.</span></span> <span data-ttu-id="fc196-209">若您在編譯器已判斷其**可能為 Null** 時對參考進行取值 (Dereference)，則編譯器會警告您。</span><span class="sxs-lookup"><span data-stu-id="fc196-209">If you dereference a reference when the compiler has determined it's **maybe null**, the compiler warns you.</span></span> <span data-ttu-id="fc196-210">除非編譯器可判斷下列兩個狀況的其中一種狀況，否則參考的狀態就會是**可能為 Null**：</span><span class="sxs-lookup"><span data-stu-id="fc196-210">The state of a reference is **maybe null** unless the compiler can determine one of two conditions:</span></span>

1. <span data-ttu-id="fc196-211">變數已確定指派為並非 Null 的值。</span><span class="sxs-lookup"><span data-stu-id="fc196-211">The variable has been definitely assigned to a non-null value.</span></span>
1. <span data-ttu-id="fc196-212">變數或運算式已在取值 (Dereference) 之前針對 Null 進行檢查。</span><span class="sxs-lookup"><span data-stu-id="fc196-212">The variable or expression has been checked against null before de-referencing it.</span></span>

<span data-ttu-id="fc196-213">當可為 Null 警告內容是 `enabled` 或 `safeonly` 時，編譯器會在您對處於**可能為 Null** 狀態的變數或運算式進行取值 (Dereference) 時產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-213">The compiler generates warnings whenever you dereference a variable or expression in a **maybe null** state when the nullable warning context is `enabled` or `safeonly`.</span></span> <span data-ttu-id="fc196-214">此外，當可為 Null 註釋內容是 `enabled`，且**可能為 Null** 的變數或運算式指派給不可為 Null 的參考型別時，也會產生警告。</span><span class="sxs-lookup"><span data-stu-id="fc196-214">Furthermore, warnings are generated when a **maybe null** variable or expression is assigned to a nonnullable reference type when the nullable annotation context is `enabled`.</span></span>

## <a name="learn-more"></a><span data-ttu-id="fc196-215">進一步了解</span><span class="sxs-lookup"><span data-stu-id="fc196-215">Learn more</span></span>

- <span data-ttu-id="fc196-216">[Draft Nullable reference specification](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md) (草稿可為 Null 參考規格)</span><span class="sxs-lookup"><span data-stu-id="fc196-216">[Draft Nullable reference specification](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md)</span></span>
- [<span data-ttu-id="fc196-217">可為 Null 參考教學課程簡介</span><span class="sxs-lookup"><span data-stu-id="fc196-217">Intro to nullable references tutorial</span></span>](tutorials/nullable-reference-types.md)
- [<span data-ttu-id="fc196-218">將現有的程式碼基底遷移至可為 Null 參考</span><span class="sxs-lookup"><span data-stu-id="fc196-218">Migrate an existing codebase to nullable references</span></span>](tutorials/upgrade-to-nullable-references.md)