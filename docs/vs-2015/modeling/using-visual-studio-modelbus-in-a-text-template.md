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
ms.openlocfilehash: 3815ed93156a70a547a892a281f8907419503a3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75845411"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>テキスト テンプレートでの Visual Studio ModelBus の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Modelbus 参照を含むモデルを読み取るテキストテンプレートを作成する場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ターゲットモデルにアクセスするための参照を解決することができます。 その場合は、テキストテンプレートと参照先のドメイン固有言語 (Dsl) を調整する必要があります。

- 参照のターゲットである DSL には、テキストテンプレートからアクセスできるように構成されている ModelBus アダプターが必要です。 他のコードから DSL にアクセスする場合は、標準の ModelBus アダプターに加えて、再構成されたアダプターも必要です。

     アダプターマネージャーは [Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140)) から継承する必要があり、属性を持っている必要があり `[HostSpecific(HostName)]` ます。

- このテンプレートは、 [Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))から継承する必要があります。

> [!NOTE]
> ModelBus 参照を含まない DSL モデルを読み取る場合は、DSL プロジェクトで生成されたディレクティブプロセッサを使用できます。 詳細については、「 [テキストテンプレートからのモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」を参照してください。

 テキストテンプレートの詳細については、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。

## <a name="creating-a-model-bus-adapter-for-access-from-text-templates"></a>テキストテンプレートからアクセスするためのモデルバスアダプターの作成
 テキストテンプレートで ModelBus 参照を解決するには、ターゲット DSL に互換性のあるアダプターが必要です。 テキストテンプレートは、ドキュメントエディターとは別の AppDomain で実行される [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ため、アダプターは DTE 経由でアクセスするのではなく、モデルを読み込む必要があります。

#### <a name="to-create-a-modelbus-adapter-that-is-compatible-with-text-templates"></a>テキストテンプレートと互換性のある ModelBus アダプターを作成するには

1. ターゲット DSL ソリューションに **Modelbusadapter** プロジェクトがない場合は、Modelbus 拡張機能ウィザードを使用して作成します。

    1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]Modelbus 拡張機能をまだインストールしていない場合は、ダウンロードしてインストールします。 詳細については、「 [視覚化とモデリング SDK](https://www.visualstudio.com/)」を参照してください。

    2. DSL 定義ファイルを開きます。 デザイン画面を右クリックし、[ **Modelbus の有効化**] をクリックします。

    3. ダイアログボックスで、[ **この DSL を ModelBus に公開する**] を選択します。 この DSL の両方でモデルを公開し、他の dsl への参照を使用する場合は、両方のオプションを選択できます。

    4. **[OK]** をクリックします。 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。

    5. [ **すべてのテンプレートの変換**] をクリックします。

    6. ソリューションをリビルドします。

2. テキストテンプレートと、コマンドなどの他のコードから DSL にアクセスする場合は、 **Modelbusadapter** プロジェクトを複製します。

    1. Windows エクスプローラーで、 **Modelbusadapter .csproj**を含むフォルダーをコピーして貼り付けます。

    2. プロジェクトファイルの名前を変更します (たとえば、 **T4ModelBusAdapter**)。

    3. **ソリューションエクスプローラー**で、ソリューションノードを右クリックして [**追加**] をポイントし、[**既存のプロジェクト**] をクリックします。 新しいアダプタープロジェクト **T4ModelBusAdapter**を探します。

    4. `*.tt`新しいプロジェクトの各ファイルで、名前空間を変更します。

    5. ソリューションエクスプローラーで新しいプロジェクトを右クリックし、[プロパティ] をクリックします。 プロパティエディターで、生成されたアセンブリの名前と既定の名前空間を変更します。

    6. DslPackage プロジェクトで、新しいアダプタープロジェクトへの参照を追加して、両方のアダプターを参照できるようにします。

    7. DslPackage\source.extension.tt で、新しいアダプタープロジェクトを参照する行を追加します。

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **すべてのテンプレートを変換** し、ソリューションをリビルドします。 ビルドエラーは発生しません。

3. 新しいアダプタープロジェクトで、次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.TextTemplating.11.0

         VisualStudio を作成します。

4. AdapterManager.tt の場合:

    - AdapterManagerBase の宣言を変更して、 [Vstexttemplatingmodeの adaptermanager](/previous-versions/ee844317(v=vs.140))から継承されるようにしてください。

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - ファイルの末尾付近で、HostSpecific の属性を AdapterManager クラスの前に置きます。 次の行を削除します。

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         次の行を挿入します。

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         この属性は、modelbus コンシューマーがアダプターを検索するときに使用できるアダプターのセットをフィルター処理します。

5. **すべてのテンプレートを変換** し、ソリューションをリビルドします。 ビルドエラーは発生しません。

## <a name="writing-a-text-template-that-can-resolve-modelbus-references"></a>ModelBus 参照を解決できるテキストテンプレートの作成
 通常は、"ソース" DSL からファイルを読み取り、生成するテンプレートから始めます。 このテンプレートは、ソース DSL プロジェクトで生成されたディレクティブを使用して、「 [テキストテンプレートからのモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」で説明されている方法でソースモデルファイルを読み取ります。 ただし、ソース DSL には、"ターゲット" DSL への ModelBus 参照が含まれています。 このため、テンプレートコードを有効にして、参照を解決し、ターゲット DSL にアクセスする必要があります。 そのため、次の手順に従ってテンプレートを調整する必要があります。

- テンプレートの基本クラスを [Modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))に変更します。

- `hostspecific="true"`テンプレートディレクティブにを含めます。

- ターゲット DSL とそのアダプターにアセンブリ参照を追加し、ModelBus を有効にします。

- ターゲット DSL の一部として生成されるディレクティブは必要ありません。

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

 このテキストテンプレートを実行すると、ディレクティブによって `SourceDsl` ファイルが読み込まれ `Sample.source` ます。 テンプレートは、から開始して、そのモデルの要素にアクセスでき `this.ModelRoot` ます。 このコードでは、その DSL のドメインクラスとプロパティを使用できます。

 さらに、テンプレートで ModelBus 参照を解決できます。 参照がターゲットモデルを指す場合、アセンブリディレクティブを使用すると、コードはそのモデルの DSL のドメインクラスとプロパティを使用できます。

- DSL プロジェクトによって生成されるディレクティブを使用しない場合は、次のものも含める必要があります。

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- `this.ModelBus`ModelBus へのアクセスを取得するには、を使用します。

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>チュートリアル: ModelBus を使用するテキストテンプレートのテスト
 このチュートリアルでは、次の手順に従います。

1. 2つの Dsl を構築します。 1つの DSL ( *コンシューマー*) には、 `ModelBusReference` 他の dsl ( *プロバイダー*) を参照できるプロパティがあります。

2. プロバイダーで2つの ModelBus アダプターを作成します。1つはテキストテンプレートによるアクセス用、もう1つは通常のコード用です。

3. 1つの実験用プロジェクトに Dsl のインスタンスモデルを作成します。

4. 一方のモデルのドメインプロパティを他のモデルを指すように設定します。

5. ポイントされているモデルを開くダブルクリックハンドラーを作成します。

6. 最初のモデルを読み込んで、他のモデルへの参照に従い、もう一方のモデルを読み取ることができるテキストテンプレートを作成します。

#### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>ModelBus にアクセス可能な DSL を構築する

1. 新しい DSL ソリューションを作成します。 この例では、タスクフローソリューションテンプレートを選択します。 [言語名] をに設定し `MBProvider` 、ファイル名拡張子を "..." に設定します。

2. DSL 定義図で、上部にない図の空白部分を右クリックし、[ **Modelbus の有効化**] をクリックします。

   - [ **Modelbus を有効に**する] が表示されない場合は、VMSDK modelbus 拡張機能をダウンロードしてインストールする必要があります。 VMSDK サイトの [視覚化およびモデリング SDK](https://www.visualstudio.com/)で検索します。

3. [ **Modelbus の有効化** ] ダイアログボックスで、[ **この DSL を Modelbus に公開する**] を選択し、[ **OK**] をクリックします。

    新しいプロジェクト `ModelBusAdapter` がソリューションに追加されます。

   これで、ModelBus を使用してテキストテンプレートからアクセスできる DSL が作成されました。 この参照は、コマンド、イベントハンドラー、またはルールのコードで解決できます。これらはすべて、モデルファイルエディターの AppDomain で動作します。 ただし、テキストテンプレートは別の AppDomain で実行され、編集時にモデルにアクセスすることはできません。 テキストテンプレートからこの DSL への ModelBus 参照にアクセスするには、別の ModelBusAdapter が必要です。

#### <a name="to-create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>テキストテンプレート用に構成されている ModelBus アダプターを作成するには

1. Windows エクスプローラーで、ModelBusAdapter .csproj を含むフォルダーをコピーして貼り付けます。

    フォルダーに T4ModelBusAdapter という名前を指定します。

    プロジェクトファイルの名前を T4ModelBusAdapter に変更します。

2. ソリューションエクスプローラーで、MBProvider ソリューションに T4ModelBusAdapter を追加します。 ソリューションノードを右クリックして [ **追加**] をポイントし、[ **既存のプロジェクト**] をクリックします。

3. T4ModelBusAdapter プロジェクトノードを右クリックし、[プロパティ] をクリックします。 プロジェクトのプロパティウィンドウで、 **アセンブリ名** と既定の **名前空間** をに変更し `Company.MBProvider.T4ModelBusAdapters` ます。

4. T4ModelBusAdapter の各 * .tt ファイルで、名前空間の最後の部分に "T4" を挿入して、行が次のようになるようにします。

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. プロジェクトで `DslPackage` 、にプロジェクト参照を追加 `T4ModelBusAdapter` します。

6. DslPackage\source.extension.tt で、の下に次の行を追加し `<Content>` ます。

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. プロジェクト内に `T4ModelBusAdapter` 、: **VisualStudio**への参照を追加します。

8. T4ModelBusAdapter\AdapterManager.tt を開きます。

   1. AdapterManagerBase の基本クラスを [Vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))に変更します。 ファイルのこの部分は次のようになります。

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

   2. ファイルの末尾付近で、クラス AdapterManager の前に次の追加属性を挿入します。

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        結果は次のようになります。

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

9. ソリューションエクスプローラーのタイトルバーで [ **すべてのテンプレートの変換** ] をクリックします。

10. ソリューションをリビルドします。 F5 キーを押します。

11. F5 キーを押して、DSL が動作していることを確認します。 実験用プロジェクトでを開き `Sample.provider` ます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスを閉じます。

    この DSL への ModelBus 参照は、テキストテンプレートおよび通常のコードでも解決できるようになりました。

#### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>ModelBus 参照ドメインプロパティを使用して DSL を構築する

1. 最小言語ソリューションテンプレートを使用して、新しい DSL を作成します。 言語に MBConsumer という名前を設定し、ファイル名拡張子を ". consumer" に設定します。

2. DSL プロジェクトで、MBProvider DSL アセンブリへの参照を追加します。 を右クリック  `MBConsumer\Dsl\References` し、[ **参照の追加**] をクリックします。 [ **参照** ] タブで、を見つけます。 `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    これにより、他の DSL を使用するコードを作成できます。 複数の Dsl への参照を作成する場合は、それらも追加します。

3. DSL 定義図で図を右クリックし、[ **ModelBus の有効化**] をクリックします。 ダイアログボックスで、[ **この DSL で ModelBus を使用できるようにする**] をオンにします。

4. クラスで、 `ExampleElement` 新しいドメインプロパティを追加 `MBR` し、プロパティウィンドウで、その型をに設定し `ModelBusReference` ます。

5. ダイアグラムの [ドメイン] プロパティを右クリックし、[ **ModelBusReference 固有のプロパティの編集**] をクリックします。 ダイアログボックスで、 **モデル要素**を選択します。

    ファイルダイアログフィルターを次のように設定します。

    `Provider File|*.provide`

    "&#124;" の後の部分文字列は、[ファイルの選択] ダイアログボックスのフィルターです。 * を使用してすべてのファイルを許可するように設定できます。\*

    [ **モデル要素の種類** ] ボックスの一覧で、プロバイダー DSL 内の1つ以上のドメインクラスの名前を入力します (たとえば、「Company」と入力します)。 抽象クラスにすることができます。 リストを空白のままにすると、ユーザーは任意の要素への参照を設定できます。

6. ダイアログを閉じて、 **すべてのテンプレートを変換**します。

   別の DSL の要素への参照を含むことができる DSL を作成しました。

#### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>ソリューション内の別のファイルへの ModelBus 参照を作成する

1. MBConsumer ソリューションで、CTRL キーを押しながら F5 キーを押します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **MBConsumer\Debugging**プロジェクトでの実験用インスタンスが開きます。

2. サンプルのコピーを追加します。 **MBConsumer\Debugging** プロジェクトにを指定します。 ModelBus 参照は同じソリューション内のファイルを参照する必要があるため、これが必要になります。

   1. デバッグプロジェクトを右クリックし、[ **追加**] をポイントして、[ **既存の項目**] をクリックします。

   2. [ **項目の追加** ] ダイアログボックスで、フィルターを [ **すべてのファイル ( \* . \* )**] に設定します。

   3. に移動 `MBProvider\Debugging\Sample.provide` し、[ **追加**] をクリックします。

3. `Sample.consume`を開きます。

4. 1つの例の図形をクリックし、プロパティウィンドウで、MBR プロパティの [ **...]** をクリックします。 ダイアログボックスで、[ **参照** ] をクリックしてを選択し `Sample.provide` ます。 [要素] ウィンドウで、[型タスク] を展開し、いずれかの要素を選択します。

5. ファイルを保存します。

    (の実験用インスタンスはまだ閉じていません [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] )。

   別のモデルの要素への ModelBus 参照を含むモデルを作成しました。

#### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>テキストテンプレートで ModelBus 参照を解決する

1. の実験用インスタンスで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、サンプルテキストテンプレートファイルを開きます。 その内容を次のように設定します。

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

    1. `hostSpecific` `inherits` ディレクティブの属性と属性を `template` 設定する必要があります。

    2. コンシューマーモデルは、その DSL で生成されたディレクティブプロセッサを介して通常の方法でアクセスされます。

    3. アセンブリディレクティブとインポートディレクティブは、ModelBus とプロバイダー DSL の型にアクセスできる必要があります。

    4. 多くの Mbr が同じモデルにリンクされていることがわかっている場合は、CreateAdapter を1回だけ呼び出すことをお勧めします。

2. テンプレートを保存します。 生成されたテキストファイルが次のようになっていることを確認します。

    ```

    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2

    ```

#### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>ジェスチャハンドラーで ModelBus 参照を解決する

1. の実験用インスタンスを終了し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます (実行中の場合)。

2. MBConsumer\Dsl\Custom.cs という名前のファイルを追加し、その内容を次のように設定します。

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

3. Ctrl キーを押しながら、F5 キーを押します。

4. の実験用インスタンスで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、を開き `Debugging\Sample.consume` ます。

5. 1つの図形をダブルクリックします。

     その要素に MBR を設定してある場合は、参照先のモデルが開き、参照されている要素が選択されます。

## <a name="see-also"></a>参照
 [Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md) [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)を使用したモデルの統合
