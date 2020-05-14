---
title: ModelBus を使用して、テキスト テンプレートで
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: caadb1c7d97d377959f03bec559e18f445093d03
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76111500"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>テキスト テンプレートでの Visual Studio ModelBus の使用

Visual Studio ModelBus 参照を含むモデルを読み取るテキスト テンプレートを記述する場合は、ターゲットのモデルへのアクセスに参照を解決する可能性があります。 その場合は、テキスト テンプレートと参照先のドメイン固有言語 (Dsl) を調整する必要があります。

- 参照の対象となっている DSL には、テキスト テンプレートからのアクセス用に構成された ModelBus Adapter が必要です。 他のコードから DSL にアクセスすることも、再構成されたアダプターが、標準の ModelBus アダプターだけでなく必要です。

     アダプターマネージャーは[Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))から継承する必要があり、属性 `[HostSpecific(HostName)]`を持つ必要があります。

- このテンプレートは、 [Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))から継承する必要があります。

> [!NOTE]
> ModelBus references を含まない DSL モデルを確認するには、DSL プロジェクトで生成されたディレクティブ プロセッサを使用することができます。 詳細については、次を参照してください。[テキスト テンプレートからへのアクセス モデル](../modeling/accessing-models-from-text-templates.md)します。

テキスト テンプレートの詳細については、次を参照してください。 [T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)します。

## <a name="create-a-model-bus-adapter-for-access-from-text-templates"></a>テキストテンプレートからアクセスするためのモデルバスアダプターを作成する

テキスト テンプレート内の ModelBus 参照を解決するには、ターゲット DSL の互換性のあるアダプターが必要です。 テキスト テンプレートが Visual Studio のドキュメント エディターから別の AppDomain で実行し、アダプターの DTE を通じてアクセスすることではなく、モデルを読み込むためにします。

1. ターゲット DSL ソリューションがあるない場合、 **ModelBusAdapter**プロジェクト、Modelbus 拡張機能のウィザードを使用して 1 つを作成します。

    1. ダウンロードして Visual Studio ModelBus 拡張機能をインストールしていない場合。 詳細については、次を参照してください。 [Visualization and Modeling SDK](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)します。

    2. DSL 定義ファイルを開きます。 デザイン サーフェイスを右クリックし、をクリックし、 **Modelbus の有効化**します。

    3. ダイアログ ボックスで、次のように選択します。**この DSL を ModelBus に公開する**します。 この DSL モデルを公開して、他の Dsl への参照を使用する場合は、両方のオプションを選択できます。

    4. **[OK]** をクリックします。 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。

    5. クリックして**すべてのテンプレートの変換**します。

    6. ソリューションをリビルドします。

2. テキスト テンプレートからして、コマンドなどの他のコードから DSL にアクセスする場合は、複製、 **ModelBusAdapter**プロジェクト。

    1. Windows エクスプ ローラーにコピーして貼り付けるを含むフォルダー **ModelBusAdapter.csproj**します。

    2. プロジェクト ファイルの名前を変更 (たとえば、 **T4ModelBusAdapter.csproj**)。

    3. **ソリューション エクスプ ローラー**、ソリューション ノードを右クリックし、 をポイント**追加**、 をクリックし、**既存のプロジェクト**します。 新しいアダプター プロジェクト**T4ModelBusAdapter.csproj**します。

    4. 各`*.tt`ファイル、新しいプロジェクトの名前空間を変更します。

    5. **ソリューションエクスプローラー**で新しいプロジェクトを右クリックし、 **[プロパティ]** をクリックします。 プロパティ エディターで生成されるアセンブリと既定の名前空間の名前を変更します。

    6. DslPackage プロジェクト内には、両方のアダプターへの参照を新しいアダプター プロジェクトへの参照を追加します。

    7. DslPackage\source.extension.tt では、新しいアダプター プロジェクトを参照する行を追加します。

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **すべてのテンプレートの変換**ソリューションをリビルドします。 ビルド エラーは発生しません。

3. 新しいアダプター プロジェクトの場合、次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.TextTemplating.11.0
    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4. で AdapterManager.tt:

    - AdapterManagerBase の宣言を変更して、 [Vstexttemplatingmodeの adaptermanager](/previous-versions/ee844317(v=vs.140))から継承されるようにしてください。

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - ファイルの最後に、近くには、クラス AdapterManager の前に HostSpecific 属性を置き換えます。 次の行を削除します。

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         次の行を挿入します。

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         この属性は、アダプターの modelbus コンシューマーを検索するときに使用できるアダプターのセットをフィルター処理します。

5. **すべてのテンプレートの変換**ソリューションをリビルドします。 ビルド エラーは発生しません。

## <a name="write-a-text-template-that-can-resolve-modelbus-references"></a>ModelBus 参照を解決できるテキストテンプレートを作成する

通常、読み込み、"source"DSL からファイルを生成するテンプレートを使用して開始します。 このテンプレートで説明されている方法でソース モデル ファイルを読み取るソース DSL プロジェクトで生成されたディレクティブを使用して[テキスト テンプレートからへのアクセス モデル](../modeling/accessing-models-from-text-templates.md)します。 ただし、ソース DSL には、「ターゲット」DSL への ModelBus 参照が含まれています。 テンプレート コードでの参照を解決し、ターゲット DSL にアクセスできるようにするため。 次の手順に従って、テンプレートを調整する必要がありますので。

- テンプレートの基本クラスを[Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))に変更します。

- 含める`hostspecific="true"`template ディレクティブにします。

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
    // (Let's assume they're all in the same model file):
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

 このテキスト テンプレートを実行すると、`SourceDsl`ディレクティブは、ファイルを読み込みます`Sample.source`します。 テンプレートがモデルでは、開始からの要素にアクセスできます`this.ModelRoot`します。 コードには、ドメイン クラスとその DSL のプロパティを使用できます。

 さらに、テンプレートでは、ModelBus References を解決できます。 場所の参照は、ターゲットのモデルをポイントして、アセンブリ ディレクティブは、ドメイン クラスとそのモデルの DSL のプロパティを使用してコードを使用できます。

- DSL プロジェクトによって生成されるディレクティブを使用しない場合は、次の必要があります。

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- 使用`this.ModelBus`ModelBus へのアクセスを取得します。

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>チュートリアル: ModelBus を使用するテキスト テンプレートのテスト
 このチュートリアルでは、次の手順に従います。

1. 2 つの Dsl を作成します。 1 つの DSL、*コンシューマー*が、`ModelBusReference`プロパティその他の DSL を参照できる、*プロバイダー*します。

2. プロバイダーの 2 つの ModelBus アダプターを作成します。 他の通常のコード、テキスト テンプレートによるアクセスのいずれか。

3. 1 つの実験的なプロジェクトで、Dsl のインスタンス モデルを作成します。

4. その他のモデルをポイントする 1 つのモデルには、ドメイン プロパティを設定します。

5. 指すモデルを開く をダブルクリック ハンドラーを記述します。

6. 最初のモデルを読み込み、以下の他のモデルへの参照およびその他のモデルを読み取ることができます、テキスト テンプレートを記述します。

### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>DSL を ModelBus にアクセスできるコンス トラクター

1. 新しい DSL ソリューションを作成します。 この例では、Task Flow ソリューション テンプレートを選択します。 言語名を設定`MBProvider`と".provide"にファイル名拡張子。

2. DSL 定義図で、上部近くない図の空白部分を右クリックし、順にクリックします**Modelbus の有効化**します。

   [ **Modelbus を有効に**する] が表示されない場合は、VMSDK modelbus 拡張機能をダウンロードしてインストールします。

3. **Modelbus の有効化**ダイアログ ボックスで、**この DSL を ModelBus に公開**、 をクリックし、 **OK**。

    新しいプロジェクトの場合は、`ModelBusAdapter`ソリューションに追加されます。

DSL を ModelBus を使用してテキスト テンプレートからアクセスできるようになりましたがあります。 コマンド、イベント ハンドラー、または規則、モデル ファイル エディターの AppDomain で動作するすべてのコードへの参照を解決できます。 ただし、テキスト テンプレートでは、別の AppDomain で実行され、編集されているときに、モデルにアクセスできません。 テキスト テンプレートからこの DSL を ModelBus references をアクセスする場合は、個別の ModelBusAdapter が必要です。

### <a name="create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>テキストテンプレート用に構成されている ModelBus アダプターを作成する

1. ファイルエクスプローラーで、 *Modelbusadapter .csproj*を含むフォルダーをコピーして貼り付けます。

    フォルダーに**T4ModelBusAdapter**という名前を指定します。

    プロジェクトファイルの名前を*T4ModelBusAdapter*に変更します。

2. ソリューション エクスプ ローラーで T4ModelBusAdapter を MBProvider ソリューションに追加します。 ソリューション ノードを右クリックし、[**追加**、] をクリックし、**既存のプロジェクト**します。

3. T4ModelBusAdapter プロジェクト ノードを右クリックし、し、[プロパティ] をクリックします。 プロジェクトのプロパティ ウィンドウで次のように変更します。、**アセンブリ名**と**既定 Namespace**に`Company.MBProvider.T4ModelBusAdapters`します。

4. T4ModelBusAdapter で各 *.tt ファイルには、行は、次のようにするため、名前空間の最後の部分に"T4"を挿入します。

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. `DslPackage`プロジェクトでプロジェクト参照を追加、`T4ModelBusAdapter`します。

6. 下にある次の行を追加で DslPackage\source.extension.tt、`<Content>`します。

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. `T4ModelBusAdapter`プロジェクトへの参照の追加: **Microsoft.VisualStudio.TextTemplating.Modeling.11.0**

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

9. クリックして**すべてのテンプレートの変換**タイトル バーのソリューション エクスプ ローラーでします。

10. **F5**キーを押します。

11. DSL が動作していることを確認します。 実験用のプロジェクトで開きます`Sample.provider`します。 Visual Studio の実験用インスタンスを終了します。

    テキスト テンプレートと通常のコードで、この DSL を ModelBus References を解決ようになりましたことができます。

### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>ModelBus 参照ドメインのプロパティを使用して、DSL を作成します。

1. 最小言語ソリューション テンプレートを使用して、新しい DSL を作成します。 MBConsumer 言語の名前を指定し、".consume"にファイル名拡張子を設定します。

2. DSL プロジェクトでは、MBProvider DSL アセンブリへの参照を追加します。 右クリックして`MBConsumer\Dsl\References` をクリックし、**参照の追加**します。 **参照**タブで、 `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    これにより、他の DSL を使用するコードを作成することができます。 いくつかの Dsl への参照を作成する場合も追加します。

3. DSL 定義図でダイアグラムを右クリックし をクリックし、 **ModelBus の有効化**します。 ダイアログ ボックスで、次のように選択します。 **、ModelBus を使用するには、この DSL を有効にする**します。

4. クラスの`ExampleElement`、新しいドメインのプロパティを追加`MBR`、[プロパティ] ウィンドウにその型を設定および`ModelBusReference`。

5. 上の図は、ドメイン プロパティを右クリックし、をクリックし、**編集 ModelBusReference 固有プロパティ**します。 ダイアログ ボックスで、次のように選択します。**モデル要素**します。

    次に、ファイル ダイアログ フィルターを設定します。

    `Provider File|*.provide`

    後の部分文字列"&#124;"はファイルの選択 ダイアログ ボックスのフィルターです。 使用してすべてのファイルを許可するように設定できます *。\*

    **モデル要素の型**一覧で、プロバイダーの DSL (たとえば、Company.MBProvider.Task) 以上のドメイン クラスの 1 つ以上の名前を入力します。 抽象クラスがあります。 一覧を空白のままにした場合、ユーザーは任意の要素への参照を設定できます。

6. ダイアログ ボックスを閉じると**すべてのテンプレートの変換**します。

   別の DSL 内の要素への参照を含むことのできる DSL を作成しました。

### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>ソリューション内の別のファイルへの ModelBus 参照を作成します。

1. MBConsumer ソリューションでは、ctrl キーを押しながら f5 キーを押します。 Visual Studio の実験用インスタンスが開き、 **MBConsumer\Debugging**プロジェクト。

2. Sample.provide へのコピーを追加、 **MBConsumer\Debugging**プロジェクト。 これは、機能は、ModelBus 参照する必要があります、同じソリューション内のファイルを参照しているため必要です。

   1. デバッグ プロジェクトを右クリックし、[**追加**、] をクリックし、**既存項目の**します。

   2. **項目の追加**ダイアログ ボックスで、フィルターを設定**すべてのファイル (\*.\*)** .

   3. 移動します`MBProvider\Debugging\Sample.provide`し**追加**します。

3. `Sample.consume` を開きます。

4. 例の 1 つの図形をクリックし、[プロパティ] ウィンドウで次のようにクリックします **[...]。** MBR プロパティ。 ダイアログ ボックスで、次のようにクリックします。**参照**選択`Sample.provide`します。 要素のウィンドウでタスクの種類を展開し、要素の 1 つを選択します。

5. ファイルを保存します。 (まだ閉じないでください Visual Studio の実験用インスタンス。)

   別のモデルの要素への ModelBus 参照を含むモデルを作成しました。

### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>テキスト テンプレート内の ModelBus 参照を解決するには

1. Visual Studio の実験用インスタンスのサンプルのテキスト テンプレート ファイルを開きます。 その内容を次の手順に設定します。

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

    - `hostSpecific`と`inherits`の属性、`template`ディレクティブを設定する必要があります。

    - コンシューマー モデルは、その DSL で生成されたディレクティブ プロセッサを通常の方法でアクセスします。

    - アセンブリとインポート ディレクティブは、ModelBus および DSL プロバイダーの種類にアクセスできる必要があります。

    - Mbr を多くが、同じモデルにリンクされている場合は、1 回だけ CreateAdapter を呼び出すことをお勧めします。

2. テンプレートを保存します。 生成されたテキスト ファイルが、次のようになっていることを確認します。

    ```
    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2
    ```

### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>ジェスチャ ハンドラーの ModelBus 参照を解決するには

1. 実行されている場合は、Visual Studio の実験用インスタンスを閉じます。

2. *MBConsumer\Dsl\Custom.cs*という名前のファイルを追加し、その内容を次のように設定します。

    ```csharp
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

3. **Ctrl**+**F5**キーを押します。

4. Visual Studio の実験用インスタンスの開く`Debugging\Sample.consume`します。

5. 1 つの図形をダブルクリックします。

    その要素で MBR を設定した場合は、参照先のモデルが表示されますされ、参照先の要素が選択されます。

## <a name="see-also"></a>関連項目

- [Visual Studio Modelbus によるモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
