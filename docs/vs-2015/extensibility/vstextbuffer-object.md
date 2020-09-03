---
title: VSTextBuffer オブジェクト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5b68d443e542b6bd707aacc2b22d0efc1064152c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690640"
---
# <a name="vstextbuffer-object"></a>VSTextBuffer オブジェクト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストバッファーオブジェクトは、通常はファイルに関連付けられている Unicode テキストのストリームを表します。 オブジェクトは、 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ウィザードの場合と同様に、コアエディターのコンテキストの外部で使用できます。  
  
 次の表は、のインターフェイスを示して `VSTextBuffer` います。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IOleCommandTarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|標準 OLE インターフェイス。 主に、バッファー内の元に戻す/やり直し処理に使用されます。|  
|[IPersistFile](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|標準 OLE インターフェイス。|  
|[IPersistStream](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|標準 OLE インターフェイス。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合語アクション (つまり、1つの元に戻す/やり直し単位でグループ化されたアクション) を作成できるようにします。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|テキストバッファーによって管理されるドキュメントデータの永続化を有効にします。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|基本的なサービスを提供します。多くのクライアントで使用されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|バッファーを検索するために使用します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|2次元座標を使用して読み取りおよび書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|1次元座標を使用して読み取りおよび書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|バッファー内のテキストへの高速でストリーム指向のシーケンシャルアクセスを提供します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|プロパティのジェネリックコレクションへのアクセスを提供します。 最も重要なプロパティは、バッファーの名前 (モニカー) です。 このインターフェイスを使用して独自のランダムデータをバッファーに格納するには、GUID を作成し、それをキーとして使用します。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|イベントの接続ポイントをサポートします。|  
  
## <a name="remarks"></a>注釈  
 は、通常、の `VSTextBuffer` 呼び出しによって検出され `QueryInterface` `IVsTextBuffer` ます。 詳細については、「 [テキストバッファー](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 [図形の編集](https://msdn.microsoft.com/f08872bd-fd9c-4e36-8cf2-a2a2622ef986)
