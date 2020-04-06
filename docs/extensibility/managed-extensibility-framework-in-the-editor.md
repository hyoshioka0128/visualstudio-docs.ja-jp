---
title: エディタでのマネージ機能拡張フレームワーク |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 888c5206b87079cf9fa91cb68e9801cb3c4f8c1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702877"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>エディターでのマネージ機能拡張フレームワーク
エディターは、マネージ機能拡張フレームワーク (MEF) コンポーネントを使用してビルドされます。 エディターを拡張する独自の MEF コンポーネントをビルドし、コードはエディター コンポーネントを使用することもできます。

## <a name="overview-of-the-managed-extensibility-framework"></a>マネージ機能拡張フレームワークの概要
 MEF は、MEF プログラミング モデルに従ってアプリケーションまたはコンポーネントの機能を追加および変更できる .NET ライブラリです。 Visual Studio エディターは、MEF コンポーネントパーツを提供および使用できます。

 MEF は、.NET フレームワーク バージョン 4*システム.コンポーネントモデル.コンポジション.dll*アセンブリに含まれています。

 MEF の詳細については、「[マネージ機能拡張フレームワーク (MEF) 」](/dotnet/framework/mef/index)を参照してください。

### <a name="component-parts-and-composition-containers"></a>コンポーネント部品と構成コンテナ
 コンポーネントパーツは、次のいずれか(または両方)を実行できるクラスまたはクラスのメンバーです。

- 別のコンポーネントを使用する

- 別のコンポーネントで消費される

  たとえば、倉庫在庫コンポーネントによって提供される製品の在庫データに依存する注文入力コンポーネントを持つショッピング アプリケーションを考えてみます。 MEF の用語では、在庫部品は製品の利用可能在庫データを*エクスポート*でき、注文入力部はデータを*インポート*できます。 注文入力部分と在庫部分は、互いについて知っている必要はありません。*構成コンテナー* (ホスト アプリケーションによって提供されます) は、エクスポートのセットを維持し、エクスポートとインポートを解決します。

  通常、構成コンテナー<xref:System.ComponentModel.Composition.Hosting.CompositionContainer>は ホストが所有します。 合成コンテナは、エクスポートされたコンポーネントパーツの*カタログ*を保持します。

### <a name="export-and-import-component-parts"></a>コンポーネント部品のエクスポートとインポート
 パブリック クラスまたはクラスのパブリック メンバー (プロパティまたはメソッド) として実装されている限り、任意の機能をエクスポートできます。 コンポーネントパーツを<xref:System.ComponentModel.Composition.Primitives.ComposablePart>から派生させる必要はありません。 代わりに、エクスポートする<xref:System.ComponentModel.Composition.ExportAttribute>クラスまたはクラス メンバーに属性を追加する必要があります。 この属性は、別のコンポーネントパーツが機能をインポートできる*コントラクト*を指定します。

### <a name="the-export-contract"></a>輸出契約
 は<xref:System.ComponentModel.Composition.ExportAttribute>、エクスポートされるエンティティ (クラス、インターフェイス、または構造体) を定義します。 通常、エクスポート属性は、エクスポートの種類を指定するパラメーターを受け取ります。

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 既定では、属性<xref:System.ComponentModel.Composition.ExportAttribute>は、エクスポートするクラスの型であるコントラクトを定義します。

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 この例では、既定`[Export]`の属性は に`[Export(typeof(TestAdornmentLayerDefinition))]`相当します。

 次の例に示すように、プロパティまたはメソッドをエクスポートすることもできます。

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>MEF エクスポートのインポート
 MEF エクスポートを使用する場合は、エクスポート元のコントラクト (通常はタイプ) を知り、その値を持<xref:System.ComponentModel.Composition.ImportAttribute>つ属性を追加する必要があります。 デフォルトでは、import 属性は 1 つのパラメーターを受け取ります。 次のコード行は、型<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>をインポートします。

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネントパーツからエディター機能を取得する
 既存のコードが MEF コンポーネントパーツの場合は、MEF メタデータを使用してエディター コンポーネントの部分を使用できます。

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネントパーツからエディタ機能を使用するには

1. グローバル アセンブリ キャッシュ (GAC) 内にある*System.Composition.ComponentModel.dll*への参照とエディター アセンブリへの参照を追加します。

2. 関連する using ディレクティブを追加します。

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. 次のように`[Import]`、サービス インターフェイスに属性を追加します。

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. サービスを取得したら、そのサービスのコンポーネントのいずれかを使用できます。

5. アセンブリをコンパイルしたら、*.に配置します。\共通 7\IDE\\*コンポーネント フォルダーの Visual Studio インストール。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
