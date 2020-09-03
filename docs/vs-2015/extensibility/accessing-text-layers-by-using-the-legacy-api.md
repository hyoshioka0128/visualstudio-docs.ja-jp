---
title: 従来の API を使用したテキストレイヤーへのアクセス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text layers
ms.assetid: 2258fcdd-38d1-479d-b8f8-1d4e6525f72c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 975e8624a6ffbfe0c5ae7544f2b978487465e34e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148018"
---
# <a name="accessing-text-layers-by-using-the-legacy-api"></a>レガシ API を使用するテキスト レイヤーへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストレイヤーは、通常、テキストレイアウトの一部の要素をカプセル化します。 たとえば、"時間単位の関数" レイヤーは、キャレット (テキスト挿入ポイント) を含む関数の前後のテキストを非表示にします。  
  
 テキストレイヤーは、バッファーとビューの間に存在し、ビューがバッファーの内容を確認する方法を変更します。  
  
## <a name="text-layer-information"></a>テキストレイヤー情報  
 次の一覧では、でのテキストレイヤーの動作について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
- テキストレイヤー内のテキストは、構文の色分けおよびマーカーによって装飾できます。  
  
- 現在、独自のレイヤーを実装することはできません。  
  
- レイヤーは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> 、から派生したを公開 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> します。 テキストバッファー自体はレイヤーとしても実装されます。これにより、ビューが基になるレイヤーとポリモーフィックを処理できるようになります。  
  
- ビューとバッファーの間には、任意の数のレイヤーを配置できます。 各レイヤーは、その下のレイヤーのみを処理し、ビューは主に最上位層として扱われます。 (ビューには、バッファーに関する情報がいくつかあります)。  
  
- レイヤーは、その下にあるレイヤーにのみ影響することがあります。 これは、元の標準イベント以外の層には影響を与えません。  
  
- エディターでは、非表示テキスト、合成テキスト、および右端での折り返しがレイヤーとして実装されます。 レイヤーを直接操作しなくても、非表示テキストと合成テキストを実装できます。 詳細については、「 [従来の言語サービスでのアウトライン](../extensibility/internals/outlining-in-a-legacy-language-service.md) 」と「」を参照してください <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSyntheticTextSession> 。  
  
- 各テキストレイヤーには、インターフェイスを介して公開される独自のローカル座標系があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> ます。 たとえば、線の折り返しレイヤーには2行が含まれる場合がありますが、基になるテキストバッファーには1行しか含まれない可能性があります。  
  
- ビューは、インターフェイスを介してレイヤーと通信し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView> ます。 このインターフェイスを使用して、ビュー座標とバッファー座標を調整します。  
  
- テキストを発信する合成テキストレイヤーなどのレイヤーは、のローカル実装を提供する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A> ます。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>また、テキストレイヤーでは、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> インターフェイスでイベントを実装して起動する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents> ます。  
  
## <a name="see-also"></a>参照  
 [カスタムエディターでの構文の色分け](../extensibility/syntax-coloring-in-custom-editors.md)   
 [レガシ API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [レガシ API を使用するエディター コントロールおよびメニューのカスタマイズ](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)
