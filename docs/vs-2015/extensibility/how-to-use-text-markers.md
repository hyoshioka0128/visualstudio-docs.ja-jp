---
title: '方法: テキストマーカーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - using text markers
ms.assetid: 76eed51c-eecb-4579-823e-13df2f0526b9
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 25c3c4f3a3d9a253b9ec671892d0d44ccf9ca3ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841684"
---
# <a name="how-to-use-text-markers"></a>方法: テキスト マーカーを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オブジェクトを編集するには、テキストマーカーを適用でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> ます。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-apply-text-markers"></a>テキストマーカーを適用するには  
  
1. クラスのインスタンスを取得 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> します。  
  
    > [!NOTE]
    > コアエディターでは、編集中のドキュメントに標準のテキストマーカーが自動的に適用されるため、標準のテキストマーカーを明示的に適用する必要はありません。  
  
2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A>操作するテキストマーカーのを使用してメソッドを呼び出すことにより、目的のマーカーのマーカーの種類 ID を取得し `GUID` ます。  
  
    > [!NOTE]
    > `GUID`テキストマーカーを提供する VSPackage またはサービスのを使用しないでください。  
  
3. メソッドまたはメソッドを呼び出すパラメーターとしてメソッドを呼び出すことによって取得したマーカーの種類 ID を使用して、テキスト <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> の特定の領域にテキストマーカーを適用します。  
  
#### <a name="to-add-features-to-text-markers"></a>機能をテキストマーカーに追加するには  
  
1. ツールヒント、特別なコンテキストメニュー、特別な状況のハンドラーなど、テキストマーカーに機能を追加することをお勧めします。 そのためには次を行います。  
  
2. インターフェイスを実装するオブジェクトを作成 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> します。  
  
3. 追加の機能が必要な場合は、インターフェイスを実装 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx> するのと同じオブジェクトに、、およびの各インターフェイスを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> ます。  
  
4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>作成したインターフェイスを、メソッドの呼び出しに渡すか、テキスト <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> の特定の領域にテキストマーカーを適用するために使用するメソッドに渡します。  
  
5. コンテキストメニューのサポートをテキストマーカー領域に追加する場合は、メニューを作成する必要があります。  
  
     コンテキストメニューを作成する方法の詳細については、「 [コンテキストメニュー](../extensibility/context-menus.md)」を参照してください。  
  
6. 環境は、メソッドなど、指定された [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インターフェイスのメソッド、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetTipText%2A> または <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> 必要に応じてメソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [レガシ API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [方法: 標準テキストマーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)   
 [方法: カスタムテキストマーカーを作成する](../extensibility/how-to-create-custom-text-markers.md)   
 [方法: エラー マーカーを実装する](../extensibility/how-to-implement-error-markers.md)
