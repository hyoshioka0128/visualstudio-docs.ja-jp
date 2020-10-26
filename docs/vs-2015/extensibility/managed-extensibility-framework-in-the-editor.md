---
title: エディターでの Managed Extensibility Framework |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f19b71c86d972b59a9d46f379bf7ec93f63aeb9a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65679955"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>エディター内の Managed Extensibility Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターは、Managed Extensibility Framework (MEF) コンポーネントを使用して作成されます。 独自の MEF コンポーネントをビルドしてエディターを拡張することができます。また、コードでエディターコンポーネントを使用することもできます。  
  
## <a name="overview-of-the-managed-extensibility-framework"></a>Managed Extensibility Framework の概要  
 MEF は、MEF プログラミングモデルに準拠するアプリケーションまたはコンポーネントの機能を追加および変更できる .NET ライブラリです。 Visual Studio エディターでは、MEF コンポーネントパーツを提供および使用することができます。  
  
 MEF は .NET Framework version 4 System.ComponentModel.Composition.dll アセンブリに含まれています。  
  
 MEF の詳細については、「 [Managed Extensibility Framework (mef)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)」を参照してください。  
  
### <a name="component-parts-and-composition-containers"></a>コンポーネントパーツと合成コンテナー  
 コンポーネントパーツは、次のいずれかまたは両方の操作を実行できるクラスまたはクラスのメンバーです。  
  
- 別のコンポーネントを使用する  
  
- 別のコンポーネントによって使用される  
  
  たとえば、倉庫の在庫コンポーネントによって提供される製品の可用性データに依存する注文エントリコンポーネントを持つショッピングアプリケーションを考えてみます。 MEF 用語では、在庫部分は製品の可用性データを *エクスポート* でき、注文エントリパーツはデータを *インポート* できます。 注文エントリパーツと在庫部分は、互いについて知る必要はありません。(ホストアプリケーションによって提供される) *合成コンテナー* は、エクスポートのセットを維持し、エクスポートとインポートを解決します。  
  
  合成コンテナーは、 <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> 通常、ホストによって所有されます。 合成コンテナーは、エクスポートされたコンポーネントパーツの *カタログ* を保持します。  
  
### <a name="exporting-and-importing-component-parts"></a>コンポーネントパーツのエクスポートとインポート  
 パブリッククラスまたはクラスのパブリックメンバー (プロパティまたはメソッド) として実装されている限り、任意の機能をエクスポートできます。 からコンポーネント部分を派生させる必要はありません <xref:System.ComponentModel.Composition.Primitives.ComposablePart> 。 代わりに、 <xref:System.ComponentModel.Composition.ExportAttribute> エクスポートするクラスまたはクラスメンバーに属性を追加する必要があります。 この属性は、別のコンポーネントパーツが機能をインポートする際に使用する *コントラクト* を指定します。  
  
### <a name="the-export-contract"></a>エクスポートコントラクト  
 は、 <xref:System.ComponentModel.Composition.ExportAttribute> エクスポートされるエンティティ (クラス、インターフェイス、または構造体) を定義します。 通常、export 属性は、エクスポートの種類を指定するパラメーターを受け取ります。  
  
```  
[Export(typeof(ContentTypeDefinition))]  
class TestContentTypeDefinition : ContentTypeDefinition {   }  
```  
  
 既定では、 <xref:System.ComponentModel.Composition.ExportAttribute> 属性はエクスポートするクラスの型であるコントラクトを定義します。  
  
```  
[Export]  
[Name("Structure")]  
[Order(After = "Selection", Before = "Text")]  
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }  
```  
  
 この例では、既定の `[Export]` 属性はと同じです `[Export(typeof(TestAdornmentLayerDefinition))]` 。  
  
 次の例に示すように、プロパティまたはメソッドをエクスポートすることもできます。  
  
```  
[Export]  
[Name("Scarlet")]  
[Order(After = "Selection", Before = "Text")]  
public AdornmentLayerDefinition scarletLayerDefinition;  
```  
  
### <a name="importing-a-mef-export"></a>MEF エクスポートのインポート  
 MEF エクスポートを使用する場合は、エクスポートされたコントラクト (通常は型) を把握し、その値を持つ属性を追加する必要があり <xref:System.ComponentModel.Composition.ImportAttribute> ます。 既定では、import 属性は、変更するクラスの型であるパラメーターを1つ受け取ります。 次のコード行は、型をインポートし <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> ます。  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationRegistry;  
```  
  
## <a name="getting-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネントパーツからエディター機能を取得する  
 既存のコードが MEF コンポーネントのパーツである場合、MEF メタデータを使用してエディターコンポーネントのパーツを使用できます。  
  
#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネントパーツからエディター機能を使用するには  
  
1. グローバルアセンブリキャッシュ (GAC) およびエディターアセンブリにある System.Composition.ComponentModel.dll への参照を追加します。  
  
2. 関連する using ステートメントを追加します。  
  
    ```  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text;  
    ```  
  
3. 次のように、 `[Import]` サービスインターフェイスに属性を追加します。  
  
    ```  
    [Import]  
    ITextBufferFactoryService textBufferService;  
    ```  
  
4. サービスを取得したら、そのコンポーネントのいずれかを使用できます。  
  
5. アセンブリをコンパイルしたら、...Visual Studio のインストールの \Common7\IDE\Components\ フォルダー。  
  
## <a name="see-also"></a>参照  
 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
