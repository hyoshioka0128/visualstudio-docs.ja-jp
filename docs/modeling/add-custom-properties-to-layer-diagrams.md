---
title: 依存関係図へのカスタム プロパティの追加
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c68d8a75ca8203a790684506ffd44b3d890648a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546916"
---
# <a name="add-custom-properties-to-dependency-diagrams"></a>依存関係図へのカスタム プロパティの追加

依存関係図の拡張コードを記述する場合は、任意の要素を持つ値を依存関係図に格納できます。 値は、図が保存され、再び開かれたときに保持されます。 また、これらのプロパティを [ **プロパティ** ] ウィンドウに表示して、ユーザーが表示および編集できるようにすることもできます。 たとえば、ユーザーが各レイヤーに正規表現を指定できるようにすることや、各レイヤーのクラスの名前がユーザーが指定したパターンに準拠していることを確認するための検証コードをユーザーが記述できるようにすることができます。

## <a name="non-visible-properties"></a>非表示のプロパティ

コードで依存関係図の要素に値をアタッチするだけの場合は、MEF コンポーネントを定義する必要はありません。 `Properties` [Ilayerelement](/previous-versions/ff644511(v=vs.140))にという名前のディクショナリがあります。 マーシャリング可能な値を任意のレイヤー要素のディクショナリに単純に追加します。 これらは、依存関係図の一部として保存されます。

## <a name="editable-properties"></a>編集可能なプロパティ

**最初の準備**

> [!IMPORTANT]
> プロパティを表示するには、レイヤーのプロパティを表示する各コンピューターで、次の変更を行います。
>
> 1. " **管理者として実行**" を使用してメモ帳を実行します。 *%ProgramFiles%\Microsoft Visual Studio [バージョン] \Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest*を開きます。
> 2. **Content**要素内で、次を追加します。
>
>     ```xml
>     <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>
>     ```
>
> 3. Visual Studio アプリケーションの [スタート] メニューの [ **Visual Studio Tools** ] セクションで、 **開発者コマンドプロンプト**を開きます。 次を入力します。
>
>      `devenv /rootSuffix /updateConfiguration`
>
>      `devenv /rootSuffix Exp /updateConfiguration`
> 4. Visual Studio を再起動します。

**コードが VSIX プロジェクトに含まれていることを確認する**

プロパティがコマンド、ジェスチャ、または検証プロジェクトの一部である場合は、何も追加する必要はありません。 カスタム プロパティのコードは、MEF コンポーネントとして定義された Visual Studio 機能拡張プロジェクトで定義する必要があります。 詳細については、「 [依存関係図へのコマンドおよびジェスチャの追加](../modeling/add-commands-and-gestures-to-layer-diagrams.md) 」または「 [依存関係図へのカスタムアーキテクチャ検証の追加](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)」を参照してください。

**カスタム プロパティを定義する**

カスタム プロパティを作成するには、次のようなクラスを定義します。

```csharp
[Export(typeof(IPropertyExtension))]
public class MyProperty : PropertyExtension<ILayerElement>
{
  // Implement the interface.
}
```

[Ilayerelement](/previous-versions/ff644511(v=vs.140))またはその派生クラスには、次のようなプロパティを定義できます。

- `ILayerModel` -モデル

- `ILayer` -各層

- `ILayerDependencyLink` - レイヤー間のリンク

- `ILayerComment`

- `ILayerCommentLink`

## <a name="example"></a>例

次のコードは、標準的なカスタム プロパティ記述子です。 この例では、Boolean プロパティがレイヤー モデル (`ILayerModel`) で定義されており、ユーザーはこれを使用してカスタム検証メソッドに値を提供できます。

```csharp
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;

namespace MyNamespace
{
  /// <summary>
  /// Custom properties are added to the Layer Designer via a custom
  /// Property Descriptor. We have to export this Property Descriptor
  /// using MEF to make it available in the Layer Designer.
  /// </summary>
  [Export(typeof(IPropertyExtension))]
  public class AllTypesMustBeReferencedProperty
      : PropertyExtension<ILayerModel>
  {
    /// <summary>
    /// Each custom property must have a unique name.
    /// Usually we use the full name of this class.
    /// </summary>
    public static readonly string FullName =
      typeof(AllTypesMustBeReferencedProperty).FullName;

    /// <summary>
    /// Construct the property. Notice the use of FullName.
    /// </summary>
    public AllTypesMustBeReferencedProperty()
            : base(FullName)
    {  }

    /// <summary>
    /// The display name is shown in the Properties window.
    /// We therefore use a localizable resource.
    /// </summary>
    public override string DisplayName
    {
      get { return Strings.AllTypesMustBeReferencedDisplayName; }
    }

    /// <summary>
    /// Description shown at the bottom of the Properties window.
    /// We use a resource string for easier localization.
    /// </summary>
    public override string Description
    {
      get { return Strings.AllTypesMustBeReferencedDescription; }
    }

    /// <summary>
    /// This is called to set a new value for this property. We must
    /// throw an exception if the value is invalid.
    /// </summary>
    /// <param name="component">The target ILayerElement</param>
    /// <param name="value">The new value</param>
    public override void SetValue(object component, object value)
    {
      ValidateValue(value);
      base.SetValue(component, value);
    }
    /// <summary>
    /// Helper to validate the value.
    /// </summary>
    /// <param name="value">The value to validate</param>
    private static void ValidateValue(object value)
    {  }

    public override Type PropertyType
    { get { return typeof(bool); } }

    /// <summary>
    /// The segment label of the properties window.
    /// </summary>
    public override string Category
    {
      get
      {
        return Strings.AllTypesMustBeReferencedCategory;
      }
    }
  }
}
```

## <a name="see-also"></a>関連項目

- [依存関係図の拡張](../modeling/extend-layer-diagrams.md)
