---
title: UML モデルの検証制約を定義する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, validation constraints
ms.assetid: 87b3b0da-122d-4121-9318-200c38ff49d0
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 32f249b971e8a37bc5b596203cde6bc7b0bcf6f1
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849734"
---
# <a name="define-validation-constraints-for-uml-models"></a>UML モデルの検証制約を定義する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定した条件をモデルが満たしているかどうかをテストする検証制約を定義できます。 たとえば、ユーザーが継承関係のループを作成していないことを確認するための制約を定義できます。 制約は、ユーザーがモデルを開くか、または保存しようとしたときに実行されるほか、手動で実行することもできます。 制約が失敗した場合は、ユーザー定義のエラー メッセージがエラー ウィンドウに追加されます。 これらの制約を[VSIX](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)(Visual Studio Integration Extension) にパッケージ化し、他の Visual Studio ユーザーに配布できます。

 また、モデルをデータベースなどの外部リソースに照らし合わせて検証する制約も定義できます。 レイヤー図に対してプログラムコードを検証する場合は、「[レイヤー図へのカスタムアーキテクチャ検証の追加](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)」を参照してください。

 UML モデルをサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="requirements"></a>要件
 「 [要件](../modeling/extend-uml-models-and-diagrams.md#Requirements)」を参照してください。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="applying-validation-constraints"></a>検証制約の適用
 検証制約は、モデルを保存したとき、モデルを開いたとき、および **[アーキテクチャ]** メニューの **[UML モデルの検証]** をクリックしたときの 3 つのケースで適用されます。 どのケースでも、そのケースに対して定義された制約だけが適用されますが、通常は、1 つ以上のケースに対して適用されるよう制約を定義します。

 検証エラーは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] エラー ウィンドウに報告されるので、エラーをダブルクリックすると、エラーが発生しているモデル要素を選択することができます。

 検証の適用の詳細については、「 [UML モデルの検証](../modeling/validate-your-uml-model.md)」を参照してください。

## <a name="defining-a-validation-extension"></a>検証拡張機能の定義
 UML デザイナーの検証拡張機能を作成するには、検証制約を定義するクラスを生成し、そのクラスを Visual Studio Integration Extension (VSIX) に埋め込む必要があります。 VSIX は、制約をインストールできるコンテナーとして機能します。 検証拡張機能を定義する方法は 2 つあります。

- **プロジェクトテンプレートを使用して、独自の VSIX に検証拡張機能を作成します。** これはより簡単な方法です。 検証制約を他の種類の拡張機能 (メニュー コマンド、カスタム ツールボックス項目、ジェスチャ ハンドラーなど) と組み合わせない場合は、この方法を使用します。 複数の制約を 1 つのクラスで定義できます。

- **個別の検証クラスと VSIX プロジェクトを作成します。** 複数の種類の拡張機能を同じ VSIX に組み合わせる場合は、この方法を使用します。 たとえば、メニュー コマンドが特定の制約に従うモデルを必要とする場合は、そのモデルを検証メソッドとして同じ VSIX に埋め込むことができます。

#### <a name="to-create-a-validation-extension-in-its-own-vsix"></a>検証拡張機能を独自の VSIX に生成するには

1. **[新しいプロジェクト]** ダイアログ ボックスの **[モデリング プロジェクト]** で、 **[検証拡張機能]** をクリックします。

2. 新しいプロジェクトで **.cs** ファイルを開き、クラスを変更して検証制約を実装します。

    詳細については、「 [検証制約の評価](#Implementing)」を参照してください。

   > [!IMPORTANT]
   > **.cs** ファイルに次の `using` ステートメントが含まれていることを確認します。
   >
   >  `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`

3. 新しいメソッドを定義して制約を追加できます。 メソッドを検証メソッドとして識別するには、最初の検証メソッドと同じように属性をタグ付ける必要があります。

4. F5 キーを押して制約をテストします。 詳細については、「 [検証制約の実行](#Executing)」を参照してください。

5. 別のコンピューターにメニューコマンドをインストールします。そのためには、プロジェクトによってビルドされた **\\\*.vsix\\\*ファイルビン**をコピーします。 詳細については、「 [拡張機能のインストールとアンインストール](#Installing)」を参照してください。

   他の **.cs** ファイルを追加すると、通常は次の `using` ステートメントが必要になります。

```csharp
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Uml.Classes;

```

 次の手順も使用できます。

#### <a name="to-create-a-separate-validation-constraint-in-a-class-library-project"></a>クラス ライブラリ プロジェクトで個別の検証制約を生成するには

1. クラス ライブラリ プロジェクトを作成し、それを既存の VSIX ソリューションに追加するか、または新規のソリューションを作成します。

    1. **[ファイル]** メニューで、 **[新規]** 、 **[プロジェクト]** をクリックします。

    2. **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、中央の列で、 **[クラス ライブラリ]** をクリックします。

2. ソリューションに既存の VSIX プロジェクトが存在しない場合は、新しく作成します。

    1. **ソリューション エクスプローラー**のソリューションのショートカット メニューで、  **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。

    2. **[インストールされたテンプレート]** の **[Visual C#]** または **[Visual Basic]** を展開し、 **[機能拡張]** をクリックします。 中央の列で、 **[VSIX プロジェクト]** をクリックします。

3. VSIX プロジェクトをソリューションのスタートアップ プロジェクトとして設定します。

    - ソリューション エクスプローラーで、VSIX プロジェクトのショートカット メニューを開き、 **[スタートアップ プロジェクトに設定]** をクリックします。

4. **source.extension.vsixmanifest**の **[コンテンツ]** で、クラス ライブラリ プロジェクトを MEF コンポーネントとして追加します。

    1. **[メタデータ]** タブで、VSIX の名前を設定します。

    2. **[インストールの対象]** タブで、Visual Studio のバージョンを対象として設定します。

    3. **[アセット]** タブで、 **[新規作成]** をクリックし、ダイアログ ボックスで次のように設定します。

         **[種類]**  = **MEF コンポーネント**

         **[ソース]**  = **現在のソリューション内のプロジェクト**

         **[プロジェクト]**  = *クラス ライブラリ プロジェクト*

#### <a name="to-define-the-validation-class"></a>検証クラスを定義するには

1. 検証プロジェクト テンプレートから検証クラスを独自の VSIX と共に生成した場合、この手順は必要ありません。

2. 検証クラス プロジェクトで、次の [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] アセンブリへの参照を追加します。

     `Microsoft.VisualStudio.Modeling.Sdk.[version]`

     `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`

     `Microsoft.VisualStudio.Uml.Interfaces`

     `System.ComponentModel.Composition`

3. 次の例と似たコードを含むクラス ライブラリ プロジェクトにファイルを追加します。

    - 各検証制約は、特定の属性でマークされているメソッド内に含まれています。 このメソッドは、モデル要素の型のパラメーターを受け取ります。 検証が起動されると、検証フレームワークは、パラメーター型に対応するすべてのモデル要素に対して、すべての検証メソッドを適用します。

    - このようなメソッドは任意のクラスおよび名前空間に配置できます。 それらのメソッドをカスタマイズします。

    ```
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using Microsoft.VisualStudio.Modeling.Validation;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    using Microsoft.VisualStudio.Uml.Classes;
    // You might also need the other Microsoft.VisualStudio.Uml namespaces.

    namespace Validation
    {
      public class MyValidationExtensions
      {
        // SAMPLE VALIDATION METHOD.
        // All validation methods have the following attributes.
        [Export(typeof(System.Action<ValidationContext, object>))]
        [ValidationMethod(
           ValidationCategories.Save
         | ValidationCategories.Open
         | ValidationCategories.Menu)]
        public void ValidateClassNames
          (ValidationContext context,
           // This type determines what elements
           // will be validated by this method:
           IClass elementToValidate)
        {
          // A validation method should not change the model.

          List<string> attributeNames = new List<string>();
          foreach (IProperty attribute in elementToValidate.OwnedAttributes)
          {
            string name = attribute.Name;
            if (!string.IsNullOrEmpty(name) && attributeNames.Contains(name))
            {
              context.LogError(
                string.Format("Duplicate attribute name '{0}' in class {1}", name, elementToValidate.Name),
                "001", elementToValidate);
            }
            attributeNames.Add(name);
          }

        }
        // Add more validation methods for different element types.
      }
    }
    ```

## <a name="Executing"></a>検証制約の実行
 テストを行う場合は、検証メソッドをデバッグ モードで実行します。

#### <a name="to-test-the-validation-constraint"></a>検証制約をテストするには

1. **F5**キーを押すか、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスが開始します。

     **トラブルシューティング**: 新しい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が起動しない場合:

    - 複数のプロジェクトがある場合は、VSIX プロジェクトがソリューションのスタートアップ プロジェクトとして設定されていることを確認してください。

    - ソリューション エクスプローラーで、スタートアップまたはプロジェクトのみのショートカット メニューを開き、 **[プロパティ]** をクリックします。 プロジェクトのプロパティエディターで、 **[デバッグ]** タブを選択します。 **[外部プログラムの開始]** フィールドの文字列が [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の完全なパス名であることを確認します。通常は次のようになります。

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. 実験用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、モデリング プロジェクトを開くか、または生成し、モデリング図を開くか、または生成します。

3. 前のセクションの制約のサンプルのテストを設定するには、次の手順に従います。

    1. クラス図を開きます。

    2. クラスを作成し、名前が同じ 2 つの属性を追加します。

4. 図の任意の場所でショートカット メニューを開き、 **[検証]** をクリックします。

5. モデル内のエラーがエラー ウィンドウで報告されます。

6. エラー報告をダブルクリックします。 この報告にある要素が画面に表示された場合は、強調表示されます。

     **トラブルシューティング**: **[検証]** コマンドがメニューに表示されない場合は、次の点について確認してください。

    - 検証プロジェクトが、VSIX プロジェクトの **source.extensions.manifest** の **[アセット]** タブに MEF コンポーネントとして表示される。

    - 適切な `Export` 属性と `ValidationMethod` 属性が検証メソッドに追加されている。

    - `ValidationCategories.Menu` は、`ValidationMethod` 属性の引数に含まれており、Logical OR (&#124;) を使用して他の値で構成されています。

    - すべての `Import` 属性と `Export` 属性のパラメーターが有効である。

## <a name="Implementing"></a>制約の評価
 検証メソッドは、適用される検証制約が true と false のどちらかであるかを判定します。 true の場合、検証メソッドは何も行いません。 false の場合、検証メソッドは、 `ValidationContext` パラメーターによって提供されるメソッドを使用して、エラーを報告します。

> [!NOTE]
> 検証メソッドによってモデルが変更されることはありません。 制約がいつどのような順序で実行されるかは保証されません。 検証実行内の検証メソッドの連続的な実行の間で情報を渡す必要がある場合は、「 [複数の検証の調整](#ContextCache)」で説明されているコンテキスト キャッシュを使用できます。

 たとえば、すべての型 (クラス、インターフェイス、または列挙子) の名前が 3 文字以上であることを確認するには、次のメソッドを使用できます。

```
public void ValidateTypeName(ValidationContext context, IType type)
{
  if (!string.IsNullOrEmpty(type.Name) && type.Name.Length < 3)
  {
    context.LogError(
      string.Format("Type name {0} is too short", type.Name),
               "001", type);
   }
 }
```

 モデルをナビゲートして読み込むために使用できるメソッドおよび型の詳細については、「 [Programming with the UML API](../modeling/programming-with-the-uml-api.md) 」を参照してください。

### <a name="about-validation-constraint-methods"></a>検証制約のメソッドについて
 それぞれの検証制約は、次の形式のメソッドで定義されます。

```
[Export(typeof(System.Action<ValidationContext, object>))]
 [ValidationMethod(ValidationCategories.Save
  | ValidationCategories.Menu
  | ValidationCategories.Open)]
public void ValidateSomething
  (ValidationContext context, IClassifier elementToValidate)
{...}
```

 各検証メソッドの属性およびパラメーターを次に示します。

|||
|-|-|
|`[Export(typeof(System.Action <ValidationContext, object>))]`|Managed Extensibility Framework (MEF) を使用して、メソッドを検証制約として定義します。|
|`[ValidationMethod (ValidationCategories.Menu)]`|検証をいつ実行するかを指定します。 複数のオプションを&#124;組み合わせる場合は、ビットごとの or () を使用します。<br /><br /> `Menu` は、[検証] メニューによって呼び出されます。<br /><br /> `Save` は、モデルを保存するときに呼び出されます。<br /><br /> `Open` は、モデルを開くときに呼び出されます。 `Load` は、モデルを保存するときに呼び出されますが、違反の場合は、モデルを再度開くことができない可能性があることをユーザーに警告します。 また、読み込み時 (モデルが解析される前) にも呼び出されます。|
|`public void ValidateSomething`<br /><br /> `(ValidationContext context,`<br /><br /> `IElement element)`|`IElement` という 2 番目のパラメーターを、制約を適用する要素の型に置き換えます。 制約メソッドは、指定された型のすべての要素に対して呼び出されます。<br /><br /> メソッドの名前は重要ではありません。|

 2 番目のパラメーターに異なる型を指定し、任意の数の検証メソッドを定義できます。 検証が起動されると、パラメーター型に対応する各モデル要素に対し、それぞれの検証メソッドが呼び出されます。

### <a name="reporting-validation-errors"></a>検証エラーの報告
 エラー レポートを生成するには、 `ValidationContext`によって提供されるメソッドを使用します。

 `context.LogError("error string", errorCode, elementsWithError);`

- `"error string"` が、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] エラー一覧に表示されます。

- `errorCode` は、エラーの一意の識別子である文字列です。

- `elementsWithError` は、モデル内の要素を識別します。 ユーザーがエラー レポートをダブルクリックすると、この要素を表すシェイプが選択されます。

  `LogError(),` `LogWarning()` と `LogMessage()`、エラー一覧の異なるセクションにメッセージを配置します。

## <a name="how-validation-methods-are-applied"></a>検証メソッドの適用方法
 検証は、リレーションシップや、クラスの属性や操作のパラメーターなどの大きい要素のパートを含む、モデルのすべての要素に対して適用されます。

 どの検証メソッドも、2 番目のパラメーターの型に対応する各要素に対して適用されます。 つまり、たとえば、2 番目のパラメーターが `IUseCase` の検証メソッドと、スーパータイプが `IElement`の検証メソッドを定義すると、これらのメソッドはどちらも、モデルの各ユース ケースに対して適用されます。

 型の階層は、 [UML モデル要素の型](../modeling/uml-model-element-types.md)にまとめられています。

 また、リレーションシップに従うことによって要素にアクセスすることもできます。 たとえば、 `IClass`で検証メソッドを定義する場合、所有されているプロパティに対してループ処理を行うことができます。

```
public void ValidateTypeName(ValidationContext context, IClass c)
{
   foreach (IProperty property in c.OwnedAttributes)
   {
       if (property.Name.Length < 3)
       {
            context.LogError(
                 string.Format(
                        "Property name {0} is too short",
                        property.Name),
                 "001", property);
        }
   }
}
```

### <a name="creating-a-validation-method-on-the-model"></a>モデルでの検証メソッドの生成
 検証を実行するたびに検証メソッドが必ず 1 回呼び出されるようにする必要がある場合、 `IModel`を検証できます。

```
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs; ...
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{  foreach (IElement element in model.OwnedElements)
   { ...
```

### <a name="validating-shapes-and-diagrams"></a>図形と図の検証
 検証メソッドの主な目的とはモデルを検証することなので、図や図形などの表示要素では呼び出されません。 ただし、図コンテキストを使用すると、現在の図にアクセスすることができます。

 検証クラス内で、インポート プロパティとして `DiagramContext` を宣言します。

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
...
[Import]
public IDiagramContext DiagramContext { get; set; }
```

 検証メソッドで、 `DiagramContext` を使用して現在のフォーカス図にアクセスできます (存在する場合)。

```
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{
  IDiagram focusDiagram = DiagramContext.CurrentDiagram;
  if (focusDiagram != null)
  {
    foreach (IShape<IUseCase> useCaseShape in
              focusDiagram.GetChildShapes<IUseCase>())
    { ...
```

 `LogError`に図形を渡すことはできないため、エラーを記録するには、図形が表しているモデル要素を取得する必要があります。

```
IUseCase useCase = useCaseShape.Element;
context.LogError(... , usecase);
```

### <a name="ContextCache"></a>複数の検証の調整
 たとえば、ユーザーによって図のメニューから検証が起動されると、それぞれのモデル要素にそれぞれの検証メソッドが適用されます。 これは、検証フレームワークの 1 回の起動において、同じメソッドが異なる要素に何度も適用される可能性があることを示します。

 これは、要素間の関係を対象とする検証において問題となります。 たとえば、ユース ケースから始まり、 **include** 関係までを対象として、ループが存在しないことを確認するための検証を記述したとします。 しかし、多くの **include** リンクを含むモデル内の各ユース ケースにこのメソッドを適用した場合、モデルの同じ領域が繰り返し処理される可能性があります。

 このような状況を回避するには、検証実行中に情報を保持するコンテキスト キャッシュを使用できます。 コンテキスト キャッシュを使用すると、検証メソッドの実行間で情報を渡すことができます。 たとえば、この検証実行によって処理済みの要素のリストを格納できます。 キャッシュは、それぞれの検証実行の開始時に生成されます。キャッシュを使用して検証実行間で情報を渡すことはできません。

|||
|-|-|
|`context.SetCacheValue<T> (name, value)`|値を格納します。|
|`context.TryGetCacheValue<T> (name, out value)`|値を取得します。 正常に終了した場合は true を返します。|
|`context.GetValue<T>(name)`|値を取得します。|
|`Context.GetValue<T>()`|指定した型の値を取得します。|

## <a name="Installing"></a>拡張機能のインストールとアンインストール
 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張機能は、自分のコンピューターと他のコンピューターの両方にインストールできます。

#### <a name="to-install-an-extension"></a>拡張機能をインストールするには

1. 自分のコンピューターで、VSIX プロジェクトによってビルドされた **.vsix** ファイルを見つけます。

    1. **ソリューション エクスプローラー**で、VSIX プロジェクトのショートカット メニューを開き、 **[エクスプローラーでフォルダーを開く]** をクリックします。

    2. _YourProject_ **\\\*\\ファイルビン**を見つけ**ます。**

2. 拡張機能をインストールするターゲット コンピューターに **.vsix** ファイルをコピーします。 自分のコンピューターでも別のコンピューターでもかまいません。

    - ターゲットコンピューターは、 **source.extension.vsixmanifest**で指定した [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] のいずれかのエディションを持っている必要があります。

3. ターゲット コンピューター上で、 **.vsix** ファイルを開きます。

     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]を起動または再起動します。

#### <a name="to-uninstall-an-extension"></a>拡張機能をアンインストールするには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. **[インストール済みの拡張機能]** を展開します。

3. 拡張機能を選択し、 **[アンインストール]** をクリックします。

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、次の場所からファイルを削除することによって拡張機能を削除できます。 *% Localappdata%* は通常*DriveName*: \ Users\\*UserName*\appdata\local です):

   *%LocalAppData%* **\Microsoft\VisualStudio\\[version]\Extensions**

## <a name="Example"></a> 「例」
 この例は、要素間の依存関係におけるループを検索します。

 保存したときと検証メニュー コマンドを選択したときに検証が実行されます。

```
/// <summary>
/// Verify that there are no loops in the dependency relationsips.
/// In our project, no element should be a dependent of itself.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">Element to start validation from.</param>
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu
     | ValidationCategories.Save | ValidationCategories.Open)]
public void NoDependencyLoops(ValidationContext context, INamedElement element)
{
    // The validation framework will call this method
    // for every element in the model. But when we follow
    // the dependencies from one element, we will validate others.
    // So we keep a list of the elements that we don't need to validate again.
    // The list is kept in the context cache so that it is passed
    // from one execution of this method to another.
    List<INamedElement> alreadySeen = null;
    if (!context.TryGetCacheValue("No dependency loops", out alreadySeen))
    {
       alreadySeen = new List<INamedElement>();
       context.SetCacheValue("No dependency loops", alreadySeen);
    }

    NoDependencyLoops(context, element,
                new INamedElement[0], alreadySeen);
}

/// <summary>
/// Log an error if there is any loop in the dependency relationship.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">The element to be validated.</param>
/// <param name="dependants">Elements we've followed in this recursion.</param>
/// <param name="alreadySeen">Elements that have already been validated.</param>
/// <returns>true if no error was detected</returns>
private bool NoDependencyLoops(ValidationContext context,
    INamedElement element, INamedElement[] dependants,
    List<INamedElement> alreadySeen)
{
    if (dependants.Contains(element))
    {
        context.LogError(string.Format("{0} should not depend on itself", element.Name),
        "Fabrikam.UML.NoGenLoops", // unique code for this error
        dependants.SkipWhile(e => e != element).ToArray());
            // highlight elements that are in the loop
        return false;
    }
    INamedElement[] dependantsPlusElement =
        new INamedElement[dependants.Length + 1];
    dependants.CopyTo(dependantsPlusElement, 0);
    dependantsPlusElement[dependantsPlusElement.Length - 1] = element;

    if (alreadySeen.Contains(element))
    {
        // We have already validated this when we started
        // from another element during this validation run.
        return true;
    }
    alreadySeen.Add(element);

    foreach (INamedElement supplier in element.GetDependencySuppliers())
    {
        if (!NoDependencyLoops(context, supplier,
             dependantsPlusElement, alreadySeen))
        return false;
    }
    return true;
}
```

## <a name="see-also"></a>参照
 [UML API を使用して](../modeling/programming-with-the-uml-api.md)[モデリング拡張機能のプログラミングを定義およびインストールする](../modeling/define-and-install-a-modeling-extension.md)
