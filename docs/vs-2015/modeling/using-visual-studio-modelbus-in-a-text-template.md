---
title: テキストテンプレートで ModelBus を使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 5ed3e5c2-f60f-43c7-8ef4-754f511339c5
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a0d18103d2990b2734e4db1d1e7dc4261e08e7a7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301365"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>テキスト テンプレートでの Visual Studio ModelBus の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus 参照を含むモデルを読み取るテキストテンプレートを作成する場合は、ターゲットモデルにアクセスするための参照を解決することができます。 その場合は、テキスト テンプレートと参照先のドメイン固有言語 (Dsl) を調整する必要があります。

- 参照の対象となっている DSL には、テキスト テンプレートからのアクセス用に構成された ModelBus Adapter が必要です。 他のコードから DSL にアクセスすることも、再構成されたアダプターが、標準の ModelBus アダプターだけでなく必要です。

     アダプターマネージャーは[Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))から継承する必要があり、属性 `[HostSpecific(HostName)]`を持つ必要があります。

- このテンプレートは、 [Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))から継承する必要があります。

> [!NOTE]
> ModelBus references を含まない DSL モデルを確認するには、DSL プロジェクトで生成されたディレクティブ プロセッサを使用することができます。 詳細については、「[テキストテンプレートからのモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」を参照してください。

 テキストテンプレートの詳細については、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。

## <a name="creating-a-model-bus-adapter-for-access-from-text-templates"></a>テキスト テンプレートからアクセスするため、モデル バス アダプターを作成します。
 テキスト テンプレート内の ModelBus 参照を解決するには、ターゲット DSL の互換性のあるアダプターが必要です。 テキストテンプレートは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ドキュメントエディターとは別の AppDomain で実行されるため、アダプターは DTE 経由でアクセスするのではなく、モデルを読み込む必要があります。

#### <a name="to-create-a-modelbus-adapter-that-is-compatible-with-text-templates"></a>テキスト テンプレートと互換性がある ModelBus アダプターを作成するには

1. ターゲット DSL ソリューションに**Modelbusadapter**プロジェクトがない場合は、Modelbus 拡張機能ウィザードを使用して作成します。

    1. まだ行っていない場合は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus 拡張機能をダウンロードしてインストールします。 詳細については、「[視覚化とモデリング SDK](https://go.microsoft.com/fwlink/?LinkID=185579)」を参照してください。

    2. DSL 定義ファイルを開きます。 デザイン画面を右クリックし、 **[Modelbus の有効化]** をクリックします。

    3. ダイアログボックスで、 **[この DSL を ModelBus に公開する]** を選択します。 この DSL モデルを公開して、他の Dsl への参照を使用する場合は、両方のオプションを選択できます。

    4. **[OK]** をクリックすると、 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。

    5. **[すべてのテンプレートの変換]** をクリックします。

    6. ソリューションをリビルドします。

2. テキストテンプレートと、コマンドなどの他のコードから DSL にアクセスする場合は、 **Modelbusadapter**プロジェクトを複製します。

    1. Windows エクスプローラーで、 **Modelbusadapter .csproj**を含むフォルダーをコピーして貼り付けます。

    2. プロジェクトファイルの名前を変更します (たとえば、 **T4ModelBusAdapter**)。

    3. **ソリューションエクスプローラー**で、ソリューションノードを右クリックして **[追加]** をポイントし、 **[既存のプロジェクト]** をクリックします。 新しいアダプタープロジェクト**T4ModelBusAdapter**を探します。

    4. 新しいプロジェクトの各 `*.tt` ファイルで、名前空間を変更します。

    5. ソリューション エクスプ ローラーで新しいプロジェクトを右クリックし、[プロパティ] をクリックします。 プロパティ エディターで生成されるアセンブリと既定の名前空間の名前を変更します。

    6. DslPackage プロジェクト内には、両方のアダプターへの参照を新しいアダプター プロジェクトへの参照を追加します。

    7. DslPackage\source.extension.tt では、新しいアダプター プロジェクトを参照する行を追加します。

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **すべてのテンプレートを変換**し、ソリューションをリビルドします。 ビルド エラーは発生しません。

3. 新しいアダプター プロジェクトの場合、次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.TextTemplating.11.0

         Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4. で AdapterManager.tt:

    - AdapterManagerBase の宣言を変更して、 [Vstexttemplatingmodeの adaptermanager](/previous-versions/ee844317(v=vs.140))から継承されるようにしてください。

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - ファイルの最後に、近くには、クラス AdapterManager の前に HostSpecific 属性を置き換えます。 次の行を削除します。

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         次の行を挿入します。

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         この属性は、アダプターの modelbus コンシューマーを検索するときに使用できるアダプターのセットをフィルター処理します。

5. **すべてのテンプレートを変換**し、ソリューションをリビルドします。 ビルド エラーは発生しません。

## <a name="writing-a-text-template-that-can-resolve-modelbus-references"></a>ModelBus References を解決できるテキスト テンプレートの作成
 通常、読み込み、"source"DSL からファイルを生成するテンプレートを使用して開始します。 このテンプレートは、ソース DSL プロジェクトで生成されたディレクティブを使用して、「[テキストテンプレートからのモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」で説明されている方法でソースモデルファイルを読み取ります。 ただし、ソース DSL には、「ターゲット」DSL への ModelBus 参照が含まれています。 テンプレート コードでの参照を解決し、ターゲット DSL にアクセスできるようにするため。 次の手順に従って、テンプレートを調整する必要がありますので。

- テンプレートの基本クラスを[Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))に変更します。

- テンプレートディレクティブに `hostspecific="true"` を含めます。

- ModelBus を有効にして、ターゲット DSL およびそのアダプターでは、アセンブリ参照を追加します。

- ターゲット DSL の一部として生成されるディレクティブを使用する必要はありません。

```
<#@ template debug="true" hostspecific="true" language="C#"
inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
<#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
<#@ output extension=".txt" #>
<#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
<#@ assembly name = "Company.TargetDsl.Dsl.dll" #>
<#@ assembly name = "Company.TargetDsl.T4ModelBusAdapter.dll" #>
<#@ assembly name = "System.Core" #>
<#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
<#@ import namespace="Company.TargetDsl" #>
<#@ import namespace="Company.TargetDsl.T4ModelBusAdapters" #>
<#@ import namespace="System.Linq" #>
<#
  SourceModelRoot source = this.ModelRoot; // Usual access to source model.
  // In the source DSL Definition, the root element has a model reference:
  using (TargetAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as TargetAdapter)
  {if (adapter != null)
   {
      // Get the root of the target model:
      TargetRoot target = adapter.ModelRoot;
    // The source DSL Definition has a class "SourceElement" embedded under the root.
    // (Let’s assume they’re all in the same model file):
    foreach (SourceElement sourceElement in source.Elements)
    {
      // In the source DSL Definition, each SourceElement has a MBR property:
      ModelBusReference elementReference = sourceElement.ReferenceToTarget;
      // Resolve the target model element:
      TargetElement element = adapter.ResolveElementReference<TargetElement>(elementReference);
#>
     The source <#= sourceElement.Name #> is linked to: <#= element.Name #> in target model: <#= target.Name #>.
<#
    }
  }}
  // Other useful code: this.Host.ResolvePath(filename) gets an absolute filename
  // from a path that is relative to the text template.
#>

```

 このテキストテンプレートを実行すると、`SourceDsl` ディレクティブによって `Sample.source`ファイルが読み込まれます。 このテンプレートは、`this.ModelRoot`から開始して、そのモデルの要素にアクセスできます。 コードには、ドメイン クラスとその DSL のプロパティを使用できます。

 さらに、テンプレートでは、ModelBus References を解決できます。 参照がターゲットモデルを指す場合、アセンブリディレクティブを使用すると、コードはそのモデルの DSL のドメインクラスとプロパティを使用できます。

- DSL プロジェクトによって生成されるディレクティブを使用しない場合は、次の必要があります。

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- `this.ModelBus` を使用して、ModelBus へのアクセス権を取得します。

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>チュートリアル: ModelBus を使用するテキスト テンプレートのテスト
 このチュートリアルでは、次の手順に従います。

1. 2 つの Dsl を作成します。 1つの DSL (*コンシューマー*) には、他の Dsl (*プロバイダー*) を参照できる `ModelBusReference` プロパティがあります。

2. プロバイダーの 2 つの ModelBus アダプターを作成します。 他の通常のコード、テキスト テンプレートによるアクセスのいずれか。

3. 1 つの実験的なプロジェクトで、Dsl のインスタンス モデルを作成します。

4. その他のモデルをポイントする 1 つのモデルには、ドメイン プロパティを設定します。

5. 指すモデルを開く をダブルクリック ハンドラーを記述します。

6. 最初のモデルを読み込み、以下の他のモデルへの参照およびその他のモデルを読み取ることができます、テキスト テンプレートを記述します。

#### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>DSL を ModelBus にアクセスできるコンス トラクター

1. 新しい DSL ソリューションを作成します。 この例では、Task Flow ソリューション テンプレートを選択します。 [言語名] を `MBProvider` に設定し、ファイル名拡張子を "..." に設定します。

2. DSL 定義図で、上部にない図の空白部分を右クリックし、 **[Modelbus の有効化]** をクリックします。

   - [ **Modelbus を有効に**する] が表示されない場合は、VMSDK modelbus 拡張機能をダウンロードしてインストールする必要があります。 VMSDK サイトの[視覚化およびモデリング SDK](https://go.microsoft.com/fwlink/?LinkID=185579)で検索します。

3. **[Modelbus の有効化]** ダイアログボックスで、 **[この DSL を Modelbus に公開する]** を選択し、 **[OK]** をクリックします。

    新しいプロジェクト `ModelBusAdapter`がソリューションに追加されます。

   DSL を ModelBus を使用してテキスト テンプレートからアクセスできるようになりましたがあります。 コマンド、イベント ハンドラー、または規則、モデル ファイル エディターの AppDomain で動作するすべてのコードへの参照を解決できます。 ただし、テキスト テンプレートでは、別の AppDomain で実行され、編集されているときに、モデルにアクセスできません。 テキスト テンプレートからこの DSL を ModelBus references をアクセスする場合は、個別の ModelBusAdapter が必要です。

#### <a name="to-create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>テキスト テンプレート用に構成された ModelBus アダプターを作成するには

1. Windows エクスプ ローラーでコピーして、ModelBusAdapter.csproj を含むフォルダーを貼り付けます。

    T4ModelBusAdapter フォルダーの名前を付けます。

    T4ModelBusAdapter.csproj プロジェクト ファイルの名前を変更します。

2. ソリューション エクスプ ローラーで T4ModelBusAdapter を MBProvider ソリューションに追加します。 ソリューションノードを右クリックして **[追加]** をポイントし、 **[既存のプロジェクト]** をクリックします。

3. T4ModelBusAdapter プロジェクト ノードを右クリックし、し、[プロパティ] をクリックします。 プロジェクトのプロパティウィンドウで、**アセンブリ名**と既定の**名前空間**を `Company.MBProvider.T4ModelBusAdapters`に変更します。

4. T4ModelBusAdapter で各 *.tt ファイルには、行は、次のようにするため、名前空間の最後の部分に"T4"を挿入します。

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. `DslPackage` プロジェクトで、`T4ModelBusAdapter`へのプロジェクト参照を追加します。

6. DslPackage\source.extension.tt で、[`<Content>`] の下に次の行を追加します。

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. `T4ModelBusAdapter` プロジェクトで、への参照を追加します。 **VisualStudio です**。

8. T4ModelBusAdapter\AdapterManager.tt を開きます。

   1. AdapterManagerBase の基本クラスを[Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))に変更します。 ファイルのこの部分が、次のようになります。

       ```
       namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters
       {
           /// <summary>
           /// Adapter manager base class (double derived pattern) for the <#= dslName #> Designer
           /// </summary>
           public partial class <#= dslName #>AdapterManagerBase
           : Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager
           {

       ```

   2. ファイルの最後に、近くには、クラス AdapterManager の前に、次の追加の属性を挿入します。

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        結果では、次の項目に似ています。

       ```
       /// <summary>
       /// ModelBus modeling adapter manager for a <#= dslName #>Adapter model adapter
       /// </summary>
       [Mef::Export(typeof(DslIntegration::ModelBusAdapterManager))]
       [Mef::ExportMetadata(DslIntegration::CompositionAttributes.AdapterIdKey,<#= dslName #>Adapter.AdapterId)]
       [DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]
       [Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]
       public partial class <#= dslName #>AdapterManager : <#= dslName #>AdapterManagerBase
       {
       }

       ```

9. ソリューションエクスプローラーのタイトルバーで **[すべてのテンプレートの変換]** をクリックします。

10. ソリューションをリビルドします。 F5 キーをクリックします。

11. F5 キーを押して、DSL が動作していることを確認します。 実験用プロジェクトで `Sample.provider`を開きます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスを閉じます。

    テキスト テンプレートと通常のコードで、この DSL を ModelBus References を解決ようになりましたことができます。

#### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>ModelBus 参照ドメインのプロパティを使用して、DSL を作成します。

1. 最小言語ソリューション テンプレートを使用して、新しい DSL を作成します。 MBConsumer 言語の名前を指定し、".consume"にファイル名拡張子を設定します。

2. DSL プロジェクトでは、MBProvider DSL アセンブリへの参照を追加します。 `MBConsumer\Dsl\References` を右クリックし、 **[参照の追加]** をクリックします。 **参照** タブで、`MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll` を見つけます。

    これにより、他の DSL を使用するコードを作成することができます。 いくつかの Dsl への参照を作成する場合も追加します。

3. DSL 定義図で図を右クリックし、 **[ModelBus の有効化]** をクリックします。 ダイアログボックスで、 **[この DSL で ModelBus を使用できるようにする]** をオンにします。

4. クラス `ExampleElement`で、新しいドメインプロパティ `MBR`を追加し、プロパティウィンドウでその型を `ModelBusReference`に設定します。

5. ダイアグラムの ドメイン プロパティを右クリックし、 **ModelBusReference 固有のプロパティの編集** をクリックします。 ダイアログボックスで、**モデル要素**を選択します。

    次に、ファイル ダイアログ フィルターを設定します。

    `Provider File|*.provide`

    後の部分文字列"&#124;"はファイルの選択 ダイアログ ボックスのフィルターです。 \* を使用してすべてのファイルを許可するように設定できます。\*

    **[モデル要素の種類]** ボックスの一覧で、プロバイダー DSL 内の1つ以上のドメインクラスの名前を入力します (たとえば、「Company」と入力します)。 抽象クラスがあります。 一覧を空白のままにした場合、ユーザーは任意の要素への参照を設定できます。

6. ダイアログを閉じて、**すべてのテンプレートを変換**します。

   別の DSL 内の要素への参照を含むことのできる DSL を作成しました。

#### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>ソリューション内の別のファイルへの ModelBus 参照を作成します。

1. MBConsumer ソリューションでは、ctrl キーを押しながら f5 キーを押します。 **MBConsumer\Debugging**プロジェクトで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスが開きます。

2. サンプルのコピーを追加します。 **MBConsumer\Debugging**プロジェクトにを指定します。 これは、機能は、ModelBus 参照する必要があります、同じソリューション内のファイルを参照しているため必要です。

   1. デバッグプロジェクトを右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。

   2. **[項目の追加]** ダイアログボックスで、[**すべてのファイル (\*\*)** ] にフィルターを設定します。

   3. `MBProvider\Debugging\Sample.provide` に移動し、 **[追加]** をクリックします。

3. `Sample.consume` を開きます。

4. 1つの例の図形をクリックし、プロパティウィンドウで、MBR プロパティの [ **...]** をクリックします。 ダイアログボックスで **[参照]** をクリックし、[`Sample.provide`] を選択します。 要素のウィンドウでタスクの種類を展開し、要素の 1 つを選択します。

5. ファイルを保存します。

    ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の実験用インスタンスはまだ閉じていません)。

   別のモデル内の要素への ModelBus 参照を含むモデルを作成しました。

#### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>テキスト テンプレート内の ModelBus 参照を解決するには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の実験用インスタンスで、サンプルテキストテンプレートファイルを開きます。 その内容を次の手順に設定します。

    ```
    <#@ template debug="true" hostspecific="true" language="C#"
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
    <#@ MBConsumer processor="MBConsumerDirectiveProcessor" requires="fileName='Sample.consume'" #>
    <#@ output extension=".txt" #>
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
    <#@ assembly name = "Company.MBProvider.Dsl.dll" #>
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
    <#@ import namespace="Company.MBProvider" #>
    <#
      // Property provided by the Consumer directive processor:
      ExampleModel consumerModel = this.ExampleModel;
      // Iterate through Consumer model, listing the elements:
      foreach (ExampleElement element in consumerModel.Elements)
      {
    #>
       <#= element.Name #>
    <#
        if (element.MBR != null)
      using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(element.MBR))
      {
              // If we allowed multiple types or DSLs in the MBR, discover type here.
        Task task = adapter.ResolveElementReference<Task>(element.MBR);
    #>
            <#= element.Name #> is linked to Task: <#= task==null ? "(null)" : task.Name #>
    <#
          }
      }
    #>

    ```

     次の点にも注意します。

    1. `template` ディレクティブの `hostSpecific` 属性と `inherits` 属性を設定する必要があります。

    2. コンシューマー モデルは、その DSL で生成されたディレクティブ プロセッサを通常の方法でアクセスします。

    3. アセンブリとインポート ディレクティブは、ModelBus および DSL プロバイダーの種類にアクセスできる必要があります。

    4. Mbr を多くが、同じモデルにリンクされている場合は、1 回だけ CreateAdapter を呼び出すことをお勧めします。

2. テンプレートを保存します。 生成されたテキスト ファイルが、次のようになっていることを確認します。

    ```

    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2

    ```

#### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>ジェスチャ ハンドラーの ModelBus 参照を解決するには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の実験用インスタンスを閉じます (実行中の場合)。

2. MBConsumer\Dsl\Custom.cs という名前で、次にそのコンテンツを設定したファイルを追加します。

    ```

    namespace Company.MB2Consume
    {
      using Microsoft.VisualStudio.Modeling.Integration;
      using Company.MB3Provider;

      public partial class ExampleShape
      {
        public override void OnDoubleClick(Microsoft.VisualStudio.Modeling.Diagrams.DiagramPointEventArgs e)
        {
          base.OnDoubleClick(e);
          ExampleElement element = this.ModelElement as ExampleElement;
          if (element.MBR != null)
          {
            IModelBus modelbus = this.Store.GetService(typeof(SModelBus)) as IModelBus;
            using (ModelBusAdapter adapter = modelbus.CreateAdapter(element.MBR))
            {
              Task task = adapter.ResolveElementReference<Task>(element.MBR);
              // Open a window on this model:
              ModelBusView view = adapter.GetDefaultView();
              view.Show();
              view.SetSelection(element.MBR);
            }
          }
        }
      }
    }

    ```

3. Ctrl キーを押しながら F5 キーを押します。

4. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の実験用インスタンスで、`Debugging\Sample.consume`を開きます。

5. 1 つの図形をダブルクリックします。

     その要素で MBR を設定した場合は、参照先のモデルが表示されますされ、参照先の要素が選択されます。

## <a name="see-also"></a>関連項目
 [Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md) [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)を使用したモデルの統合
