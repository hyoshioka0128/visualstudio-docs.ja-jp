---
title: Modelbus を使用したモデルの統合
description: Visual Studio ModelBus では、モデルと他のツールとの間のリンクをモデルに作成する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f0c1d076edc09f7978dcc188b167ce953f631068
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99957414"
---
# <a name="integrate-models-by-using-visual-studio-modelbus"></a>Visual Studio Modelbus を使用してモデルを統合する

Visual Studio ModelBus には、モデルとその他のツールとの間のリンクをモデルに作成するためのメソッドが用意されています。 たとえば、ドメイン固有言語 (DSL) モデルと UML モデルをリンクできます。 DSL の統合セットを作成できます。

ModelBus により、モデルまたはモデル内の特定の要素への一意の参照を作成できます。 この参照は、たとえば、別のモデル内の要素など、モデルの外に保存できます。 後で何らかのツールにおいて要素へのアクセスを取得する必要が生じると、モデル バス インフラストラクチャは適切なモデルを読み込み、要素を返します。 必要があれば、モデルをユーザーに表示できます。 ファイルが以前の場所でアクセスできない場合、ModelBus はユーザーにファイルを見つけるように求めます。 ユーザーがファイルを見つけると、ModelBus はそのファイルへのすべての参照を解決します。

> [!NOTE]
> ModelBus の現在の Visual Studio の実装では、リンクされたモデルは同じ Visual Studio ソリューション内の項目である必要があります。

追加情報とサンプル コードについては、以下を参照してください。

- [方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)

- [Visual Studio のモデリング SDK](https://www.microsoft.com/download/details.aspx?id=48148)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="providing-access-to-a-dsl"></a><a name="provide"></a> DSL へのアクセスの提供
 モデルまたはその要素への ModelBus 参照を作成するには、DSL の ModelBusAdapter を定義しておく必要があります。 これを行う最も簡単な方法は、Visual Studio モデルバス拡張機能を使用することです。これにより、DSL デザイナーにコマンドが追加されます。

### <a name="to-expose-a-dsl-definition-to-model-bus"></a><a name="expose"></a> DSL 定義をモデルバスに公開するには

1. DSL 定義ファイルを開きます。 デザイン画面を右クリックし、[ **Modelbus の有効化**] をクリックします。

2. ダイアログボックスで、[ **この DSL を ModelBus に公開する**] を選択します。 この DSL のモデルを公開すると同時に他の DSL への参照を利用する場合は、両方のオプションを選択できます。

3. **[OK]** をクリックします。 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。

4. テキスト テンプレートから DSL にアクセスする場合、新しいプロジェクトで AdapterManager.tt を変更する必要があります。 コマンドやイベント ハンドラーなどの他のコードから DSL にアクセスする場合はこの手順を省略します。 詳細については、「 [テキストテンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

   1. AdapterManagerBase の基本クラスを [Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))に変更します。

   2. ファイルの終わり近くで、クラス AdapterManager の前に次の追加属性を挿入します。

       `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

   3. ModelBusAdapter プロジェクトの参照の中で、 **VisualStudio** を追加します。

      テキスト テンプレートと他のコードの両方から DSL にアクセスするには、変更したアダプターと変更していないアダプターの 2 つが必要です。

5. [ **すべてのテンプレートの変換**] をクリックします。

6. ソリューションをリビルドします。

   これで ModelBus がこの DSL のインスタンスを開くことができるようになります。

   フォルダー `ModelBusAdapters\bin\*` には、`Dsl` プロジェクトと `ModelBusAdapters` プロジェクトによりビルドされるアセンブリが含まれます。 この DSL を別の DSL から参照するには、これらのアセンブリをインポートする必要があります。

### <a name="ensure-that-elements-can-be-referenced"></a>要素が参照可能であることを確認する

Visual Studio ModelBus アダプターは、既定では、要素の guid を使用してそれを識別します。 したがって、これらの ID はモデル ファイル内に保持される必要があります。

要素 Id が永続化されるようにするには、次のようにします。

1. DslDefinition.dsl を開きます。

2. DSL エクスプローラーで、[ **Xml シリアル化の動作**]、[ **クラスデータ**] の順に展開します。

3. モデル バス参照を作成する各クラスについて、次の操作を実行します。

    [クラス] ノードをクリックし、[プロパティウィンドウで、[ **シリアル化 ID** ] がに設定されていることを確認し `true` ます。

   また、要素名を使用して Guid ではなく要素を識別する場合は、生成されたアダプターの部分をオーバーライドできます。 アダプター クラス内の次のメソッドをオーバーライドします。

- `GetElementId` をオーバーライドし、使用する ID を返します。 このメソッドは参照を作成するときに呼び出されます。

- `ResolveElementReference` をオーバーライドし、モデル バス参照から正しい要素を特定します。

## <a name="accessing-a-dsl-from-another-dsl"></a><a name="editRef"></a> 別の DSL から DSL にアクセスする

DSL のドメイン プロパティにモデル バス参照を保存し、それらを使用するカスタム コードを作成できます。 ユーザーがモデル ファイルとその中の要素を選択することにより、モデル バス参照を作成可能にすることもできます。

DSL が別の DSL への参照を使用できるようにするには、まずモデルバス参照の *コンシューマー* にする必要があります。

### <a name="to-enable-a-dsl-to-consume-references-to-an-exposed-dsl"></a>DSL が公開されている DSL への参照を利用可能にするには

1. DSL 定義図で、図のメイン部分を右クリックし、[ **Modelbus の有効化**] をクリックします。

2. ダイアログボックスで、[ **このモデルでモデルバス参照を使用できる** ようにする] を選択します。

3. 利用する DSL の Dsl プロジェクトで、次のアセンブリをプロジェクト参照に追加します。 これらのアセンブリ (.dll ファイル) は、公開されている DSL の ModelBusAdapter\bin * ディレクトリにあります \\ 。

    - たとえば、公開されている DSL アセンブリ **Fabrikam.FamilyTree.Dsl.dll**

    - 公開されているモデルバスアダプターアセンブリ。例 **Fabrikam.FamilyTree.ModelBusAdapter.dll**

4. 次の .NET アセンブリを利用する DSL プロジェクトのプロジェクト参照に追加します。

    1. **Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**

    2. **Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0.dll**

### <a name="to-store-a-model-bus-reference-in-a-domain-property"></a>モデル バス参照をドメイン プロパティに保存するには

1. 利用する DSL の DSL 定義で、ドメイン クラスにドメイン プロパティを追加し、その名前を設定します。

2. [プロパティウィンドウで、[ドメイン] プロパティを選択し、[ **種類** ] をに設定 `ModelBusReference` します。

   この段階で、プログラム コードはプロパティ値を設定できますが、[プロパティ] ウィンドウでは読み取り専用です。

   ユーザーが特殊な ModelBus 参照エディターを使用してプロパティを設定可能にすることができます。 このエディターまたはピッカーには2つのバージョンがあり *ます。* 1 つはユーザーがモデルファイルを選択できるようにし、もう1つはユーザーがモデルファイルとモデル内の要素を選択できるようにします。

### <a name="to-allow-the-user-to-set-a-model-bus-reference-in-a-domain-property"></a>ユーザーがモデル バス参照をドメイン プロパティに設定可能にするには

1. ドメインプロパティを右クリックし、[ **ModelBusReference 固有のプロパティの編集**] をクリックします。 ダイアログ ボックスが開きます。 これは、 *モデルバスピッカー* です。

2. モデルまたはモデル内の要素に対して、適切な **種類の ModelBusReference** を選択します。

3. ファイル ダイアログ フィルター文字列に、`Family Tree files |*.ftree` のような文字列を入力します。 公開されている DSL のファイル拡張子を置き換えます。

4. モデル内の要素を参照する場合、ユーザーが選択可能な型の一覧を追加します (たとえば、Company.FamilyTree.Person)。

5. [ **OK**] をクリックし、**ソリューションエクスプローラー** ツールバーの [**すべてのテンプレートの変換**] をクリックします。

    > [!WARNING]
    > 有効なモデルまたはエンティティを選択しなかった場合、[OK] ボタンが有効のように見えても効果はありません。

6. Company.FamilyTree.Person などのターゲット型の一覧を指定した場合、DSL プロジェクトにアセンブリ参照を追加して、ターゲット DSL の DLL (たとえば、Company.FamilyTree.Dsl.dll) を参照する必要があります。

### <a name="to-test-a-model-bus-reference"></a>モデル バス参照をテストするには

1. 公開される DSL と利用する DSL の両方をビルドします。

2. F5 キーまたは CTRL+F5 キーを押して、DSL のいずれかを実験モードで実行します。

3. Visual Studio の実験用インスタンスのデバッグプロジェクトで、各 DSL のインスタンスであるファイルを追加します。

    > [!NOTE]
    > Visual Studio ModelBus は、同じ Visual Studio ソリューション内の項目であるモデルへの参照のみを解決できます。 たとえば、ファイル システムの別の部分にあるモデル ファイルへの参照は作成できません。

4. 公開される DSL のインスタンス内に要素とリンクを作成し、インスタンスを保存します。

5. 利用する DSL のインスタンスを開き、モデル バス参照プロパティを持つモデル要素を選択します。

6. [プロパティ] ウィンドウで、モデル バス参照プロパティをダブルクリックします。 ピッカー ダイアログが開きます。

7. [ **参照** ] をクリックし、公開されている DSL のインスタンスを選択します。

     モデル バス参照の要素固有の種類を指定した場合、ピッカーではモデル内の項目を選択することもできます。

## <a name="creating-references-in-program-code"></a>プログラム コード中の参照の作成

モデルまたは要素への参照をモデル内に保存する場合、`ModelBusReference` を作成します。 `ModelBusReference` にはモデル参照と要素参照の 2 種類があります。

モデル参照を作成するには、モデルがインスタンスである DSL の AdapterManager と、モデルのファイル名または Visual Studio プロジェクト項目が必要です。

要素参照を作成するには、モデル ファイルと参照する要素のアダプターが必要です。

> [!NOTE]
> Visual Studio ModelBus を使用すると、同じ Visual Studio ソリューション内の項目への参照のみを作成できます。

### <a name="import-the-exposed-dsl-assemblies"></a>公開されている DSL アセンブリのインポート

利用するプロジェクトで、DSL へのプロジェクト参照と公開されている DSL の ModelBusAdapter アセンブリを追加します。

たとえば、ModelBus References を MusicLibrary DSL の要素に保存するとします。 ModelBus References は FamilyTree DSL の要素を参照します。 MusicLibrary ソリューションの `Dsl` プロジェクトで、References ノードに次のアセンブリへの参照を追加します。

- Fabrikam.FamilyTree.Dsl.dll - 公開されている DSL。

- Fabrikam.FamilyTree.ModelBusAdapters.dll - 公開されている DSL の ModelBus アダプター。

- Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0

- Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0

  これらのアセンブリは、公開されている DSL の `ModelBusAdapters` プロジェクトの `bin\*` の下にあります。

  参照を作成するコード ファイルで、通常、次の名前空間をインポートする必要があります。

```csharp
// The namespace of the DSL you want to reference:
using Fabrikam.FamilyTree;  // Exposed DSL
using Fabrikam.FamilyTree.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling.Integration;
using System.Linq;
...
```

### <a name="to-create-a-reference-to-a-model"></a>モデルへの参照を作成するには

モデル参照を作成するには、公開されている DSL の AdapterManager にアクセスし、それを使用してモデルへの参照を作成します。 ファイル パスまたは `EnvDTE.ProjectItem` のどちらかを指定できます。

AdapterManager から、Adapter を取得し、モデル内の個々の要素にアクセスできます。

> [!NOTE]
> 操作を終了したら、Adapter を破棄する必要があります。 そのための最も便利な方法は、`using` ステートメントの使用です。 次の例を使って説明します。

```csharp
// The file path of a model instance of the FamilyTree DSL:
string targetModelFile = "TudorFamilyTree.ftree";
// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Get an adapterManager for the target DSL:
FamilyTreeAdapterManager manager =
    (modelbus.GetAdapterManager(FamilyTreeAdapter.AdapterId)
     as FamilyTreeAdapterManager;
// or: (modelBus.FindAdapterManagers(targetModelFile).First())
// or could provide an EnvDTE.ProjectItem

// Create a reference to the target model:
// NOTE: the target model must be a file in this project.
ModelBusReference modelReference =
     manager.CreateReference(targetModelFile);
// or can use an EnvDTE.ProjectItem instead of the filename

// Get the root element of this model:
using (FamilyTreeAdapter adapter =
     modelBus.CreateAdapter(modelReference) as FamilyTreeAdapter)
{
  FamilyTree modelRoot = adapter.ModelRoot;
  // Access elements under the root in the usual way:
  foreach (Person p in modelRoot.Persons) {...}
  // You can create adapters for individual elements:
  ModelBusReference elementReference =
     adapter.GetElementReference(person);
  ...
} // Dispose adapter
```

後で `modelReference` を使用可能にする場合、外部型 `ModelBusReference` を持つドメイン プロパティに保存できます。

```csharp
using Transaction t = this.Store.TransactionManager
    .BeginTransaction("keep reference"))
{
  artist.FamilyTreeReference = modelReference;
  t.Commit();
}
```

ユーザーがこのドメイン プロパティを編集可能にするには、Editor 属性のパラメーターとして `ModelReferenceEditor` を使用します。 詳細については、「 [ユーザーによる参照の編集を許可](#editRef)する」を参照してください。

### <a name="to-create-a-reference-to-an-element"></a>要素への参照を作成するには

モデル用に作成したアダプターは参照の作成と解決のために使用できます。

```csharp
// person is an element in the FamilyTree model:
ModelBusReference personReference =
  adapter.GetElementReference(person);
```

後で `elementReference` を使用可能にする場合、外部型 `ModelBusReference` を持つドメイン プロパティに保存できます。 ユーザーがそれを編集可能にするには、Editor 属性のパラメーターとして `ModelElementReferenceEditor` を使用します。 詳細については、「 [ユーザーによる参照の編集を許可](#editRef)する」を参照してください。

### <a name="resolving-references"></a>参照の解決

`ModelBusReference` (MBR) がある場合、モデルまたはモデルが参照するモデル要素を取得できます。 要素が図またはその他の表示に示されている場合、表示を開き、要素を選択できます。

MBR からアダプターを作成できます。 アダプターから、モデルのルートを取得できます。 モデル内の特定の要素を参照する MBR を解決することもできます。

```csharp
using Microsoft.VisualStudio.Modeling.Integration; ...
ModelBusReference elementReference = ...;

// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Use a model reference or an element reference
// to obtain an adapter for the target model:
using (FamilyTreeAdapter adapter =
   modelBus.CreateAdapter(elementReference) as FamilyTreeAdapter)
   // or CreateAdapter(modelReference)
{
  // Get the root of the model:
  FamilyTree tree = adapter.ModelRoot;

  // Get a model element:
  MyDomainClass mel =
    adapter.ResolveElementReference<MyDomainClass>(elementReference);
  if (mel != null) {...}

  // Get the diagram or other view, if there is one:
  ModelBusView view = adapter.GetDefaultView();
  if (view != null)
  {
   view.Open();
   // Display the diagram:
   view.Show();
   // Attempt to select the shape that presents the element:
   view.SetSelection(elementReference);
  }
} // Dispose the adapter.
```

#### <a name="to-resolve-modelbus-references-in-a-text-template"></a>テキスト テンプレート内の ModelBus References を解決するには

1. アクセスする DSL には、テキスト テンプレートによるアクセスのために構成された ModelBus Adapter が含まれている必要があります。 詳細については、「 [DSL へのアクセスの提供](#provide)」を参照してください。

2. 通常、ソース DSL 内に保存されたモデル バス参照 (MBR) を使用してターゲット DSL にアクセスします。 したがって、テンプレートにはソース DSL のディレクティブに加えて、MBR を解決するためのコードが含まれています。 テキストテンプレートの詳細については、「 [Domain-Specific 言語からのコードの生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

   ```
   <#@ template debug="true" hostspecific="true"
   inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
   <#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
   <#@ output extension=".txt" #>
   <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
   <#@ assembly name = "System.Core" #>
   <#@ assembly name = "Company.CompartmentDragDrop.Dsl.dll" #>
   <#@ assembly name = "Company.CompartmentDragDrop.ModelBusAdapter.dll" #>
   <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
   <#@ import namespace="System.Linq" #>
   <#@ import namespace="Company.CompartmentDragDrop" #>
   <#@ import namespace="Company.CompartmentDragDrop.ModelBusAdapters" #>
   <# // Get source root from directive processor:
     ExampleModel source = this.ExampleModel;
     // This DSL has a MBR in its root:
   using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as ModelBusAdapter)
     {
     ModelBusAdapterManager manager = this.ModelBus.FindAdapterManagers(this.Host.ResolvePath("Sample.compDD1")).FirstOrDefault();
     ModelBusReference modelReference =
       manager.CreateReference(this.Host.ResolvePath("Sample.compDD1"));

     // Get the root element of this model:
     using (CompartmentDragDropAdapter adapter =
        this.ModelBus.CreateAdapter(modelReference) as CompartmentDragDropAdapter)
     {
       ModelRoot root = adapter.ModelRoot;
   #>
   [[<#= root.Name #>]]
   <#
     }
   #>
   ```

   詳細とチュートリアルについては、「[テキストテンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

## <a name="serializing-a-modelbusreference"></a>ModelBusReference のシリアル化

`ModelBusReference` (MBR) を文字列形式で保存する場合、次のようにシリアル化することができます。

```csharp
string serialized = modelBus.SerializeReference(elementReference);
// Store it anywhere, then get it back again:
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, null);
```

この方法でシリアル化される MBR はコンテキストに依存しません。 単純なファイルベースのモデル バス アダプターを使用している場合、MBR には絶対ファイル パスが含まれます。 これはインスタンス モデル ファイルが絶対に移動しない場合は十分です。 ただし、モデルファイルは通常、Visual Studio プロジェクトの項目です。 ユーザーはプロジェクト全体をファイル システムの異なる場所へ移動できると期待しています。 ユーザーはプロジェクトをソース管理の下に維持し、異なるコンピューターで開くこともできると期待しています。 したがって、パス名はファイルを含むプロジェクトの場所を基準とする相対値としてシリアル化する必要があります。

### <a name="serializing-relative-to-a-specified-file-path"></a>指定されたファイル パスを基準とする相対シリアル化

`ModelBusReference` には、相対シリアル化の基準となるファイル パスなどの情報を含めることが可能なディクショナリである `ReferenceContext` が含まれています。

パス相対シリアル化を実行するには、次の操作を実行します。

```csharp
elementReference.ReferenceContext.Add(
   ModelBusReferencePropertySerializer.FilePathSaveContextKey,
   currentProjectFilePath);
string serialized = modelBus.SerializeReference(elementReference);
```

次の文字列から参照を取得するには

```csharp
ReferenceContext context = new ReferenceContext();
context.Add(ModelBusReferencePropertySerializer.FilePathLoadContextKey,
    currentProjectFilePath);
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, context);
```

### <a name="modelbusreferences-created-by-other-adapters"></a>他のアダプターにより作成された ModelBusReferences
 独自のアダプターを作成する場合、次の情報が役立ちます。

 `ModelBusReference` (MBR) は、モデル バスにより逆シリアル化される MBR ヘッダーと特定のアダプター マネージャーにより処理されるアダプター固有部分の 2 つの部分で構成されます。 これにより、独自のアダプター シリアル化形式を提供できます。 たとえば、ファイルではなくデータベースを参照したり、アダプター参照に追加情報を保存したりすることできます。 独自のアダプターは `ReferenceContext` に追加情報を配置することもできます。

 MBR を逆シリアル化する場合、ReferenceContext を指定する必要があり、これは MBR オブジェクト内に保存されます。 MBR をシリアル化する場合、保存された ReferenceContext はアダプターが文字列の生成を助けるために使用されます。 逆シリアル化された文字列には ReferenceContext 内のすべての情報が含まるわけではありません。 たとえば、単純なファイルベースのアダプターで、ReferenceContext はルート ファイル パスを含みますが、これはシリアル化された MBR 文字列に保存されません。

 MBR は次の 2 つの段階で逆シリアル化されます。

- `ModelBusReferencePropertySerializer` は、MBR ヘッダーを扱う標準シリアライザーです。 これは標準の DSL `SerializationContext` プロパティ バッグを使用し、このプロパティ バッグは, キー `ReferenceContext` を使用する `ModelBusReferencePropertySerializer.ModelBusLoadContextKey` に保存されています。 特に、`SerializationContext` は `ModelBus` のインスタンスを含む必要があります。

- ModelBus Adapter は MBR のアダプター固有部分を処理します。 これは MBR の ReferenceContext に保存されている追加情報を使用できます。 単純なファイルベースのアダプターは、キーとを使用してルートファイルパスを保持し `FilePathLoadContextKey` `FilePathSaveContextKey` ます。

     モデル ファイル内のアダプター参照は使用されるときにのみ逆シリアル化されます。

## <a name="to-create-a-model"></a>モデルを作成するには

### <a name="creating-opening-and-editing-a-model"></a>モデルの作成、オープン、および編集
 次のフラグメントは、VMSDK web サイトのステートマシンのサンプルから抜粋したものです。 ここには、ModelBusReferences を使用した、モデルの作成とオープン、およびモデルに関連する図の取得が示されています。

 このサンプルで、ターゲット DSL の名前は StateMachine です。 そこから、モデル クラスの名前や ModelBusAdapter の名前など、いくつかの名前が派生しています。

```csharp
using Fabrikam.StateMachine.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Integration;
using Microsoft.VisualStudio.Modeling.Integration.Shell;
using Microsoft.VisualStudio.Modeling.Shell;
...
// Create a new model.
ModelBusReference modelReference =
   StateMachineAdapterManager    .CreateStateMachineModel(modelName, fileName);
//Keep reference of new model in this model.
using (Transaction t = ...)
{
  myModelElement.ReferenceProperty = modelReference;
  t.Commit();
}
// Get the ModelBus service from Visual Studio.
IModelBus modelBus = Microsoft.VisualStudio.Shell.Package.
    GetGlobalService(typeof(SModelBus)) as IModelBus;
// Get a modelbus adapter on the new model.
ModelBusAdapter modelBusAdapter;
modelBus.TryCreateAdapter(modelReference,
    this.ServiceProvider, out modelBusAdapter);
using (StateMachineAdapter adapter =
      modelBusAdapter as StateMachineAdapter)
{
    if (adapter != null)
    {
        // Obtain a Diagram from the adapter.
        Diagram targetDiagram =
           ((StandardVsModelingDiagramView)
                 adapter.GetDefaultView()
            ).Diagram;

        using (Transaction t =
             targetDiagram.Store.TransactionManager
                .BeginTransaction("Update diagram"))
        {
            DoUpdates(targetDiagram);
            t.Commit();
        }

        // Display the new diagram.
        adapter.GetDefaultView().Show();
    }
}
```

## <a name="validating-references"></a>参照の検証
 BrokenReferenceDetector は ModelBusReferences を保持可能な、Store 内のすべてのドメイン プロパティをテストします。 これはアクションが見つかった場所で指定されるアクションを呼び出します。 これは特に検証メソッドに便利です。 次の検証メソッドは、モデルの保存を試行するときにストアをテストし、壊れている参照をエラー ウィンドウに報告します。

```csharp
[ValidationMethod(ValidationCategories.Save)]
public void ValidateModelBusReferences(ValidationContext context)
{
  BrokenReferenceDetector.DetectBrokenReferences(this.Store,
    delegate(ModelElement element, // parent of property
             DomainPropertyInfo property, // identifies property
             ModelBusReference reference) // invalid reference
    {
      context.LogError(string.Format(INVALID_REF_FORMAT,
             property.Name,
             referenceState.Name,
             new ModelBusReferenceTypeConverter().
                 ConvertToInvariantString(reference)),
         "Reference",
         element);
      });
}}
private const string INVALID_REF_FORMAT =
    "The '{0}' domain property of ths ReferenceState instance "
  + "named '{1}' contains reference value '{2}' which is invalid";
```

## <a name="actions-performed-by-the-modelbus-extension"></a>ModelBus 拡張機能により実行されるアクション

次の情報は必須ではありませんが、ModelBus を広く使用する場合に有用な場合があります。

ModelBus 拡張機能は DSL ソリューションで次の変更を加えます。

DSL 定義図を右クリックし、[ **Modelbus の有効化**] をクリックして、[ **この Dsl で Modelbus を使用できるよう** にする] を選択します。

- DSL プロジェクトでは、への参照が追加され **Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**

- DSL 定義に、外部型参照 `Microsoft.VisualStudio.Modeling.Integration.ModelBusReference` が追加されます。

   **DSL エクスプローラー** で、[**ドメインの種類**] の下に参照が表示されます。 外部型参照を手動で追加するには、ルート ノードを右クリックします。

- 新しいテンプレートファイルが追加されます。これは、作成された **コード \ Modelbus.**

ドメインプロパティの type を ModelBusReference に設定し、プロパティを右クリックして、[ **modelbusreference 固有のプロパティを有効に** する] をクリックします。

- ドメイン プロパティにいくつかの CLR 属性が追加されます。 それらはプロパティ ウィンドウの Custom Attributes フィールドで確認できます。 **Dslfrom** を使用すると、プロパティ宣言の属性を確認できます。

  ```csharp
  [System.ComponentModel.TypeConverter(typeof(
  Microsoft.VisualStudio.Modeling.Integration.ModelBusReferenceTypeConverter))]
  [System.ComponentModel.Editor(typeof(
    Microsoft.VisualStudio.Modeling.Integration.Picker
    .ModelReferenceEditor // or ModelElementReferenceEditor
    ), typeof(System.Drawing.Design.UITypeEditor))]
  [Microsoft.VisualStudio.Modeling.Integration.Picker
    .SupplyFileBasedBrowserConfiguration
    ("Choose a model file", "Target model|*.target")]
  ```

DSL 定義図を右クリックし、[ **ModelBus の有効化**] をクリックして、[ **この Dsl を Modelbus に公開** する] を選択します。

- ソリューションに新しいプロジェクト `ModelBusAdapter` が追加されます。

- `ModelBusAdapter` プロジェクトに `DslPackage` への参照が追加されます。 `ModelBusAdapter` プロジェクトへの参照が含まれてい `Dsl` ます。

- **DslPackage\source.extention.tt** で `|ModelBusAdapter|` は、は MEF コンポーネントとして追加されます。

## <a name="see-also"></a>関連項目

- [方法: プログラム コード内のファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)
- [方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [テキスト テンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)
