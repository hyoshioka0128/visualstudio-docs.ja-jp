---
title: レガシ API | を使用したテキストバッファーへのアクセスMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text buffers
ms.assetid: cd6cf4ae-fff5-4e23-b293-7cbafdb8aed2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f2cfbd84bc4f9298358a2a2d1ba87f76d6e5303c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184994"
---
# <a name="accessing-the-text-buffer-by-using-the-legacy-api"></a>レガシ API を使用するテキスト バッファーへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストストリームとファイルの永続化を管理するテキストです。 バッファーは他の形式の読み取りや書き込みが可能ですが、バッファーとの通常の通信はすべて Unicode を使用して実行されます。 従来の Api では、テキストバッファーは、1つまたは2次元の座標系を使用して、バッファー内の文字の位置を識別できます。  
  
## <a name="one--and-two-dimension-coordinate-systems"></a>1次元と2次元の座標系  
 1次元の座標位置は、バッファー内の最初の文字からの文字の位置 (147 など) に基づいています。 このインターフェイスを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> バッファー内の1次元の位置にアクセスします。 2次元座標系は、行とインデックスのペアに基づいています。 たとえば、バッファー内の 43, 5 の文字は、43行目の最初の文字の右側に5文字となります。 バッファー内の2次元の位置には、インターフェイスを使用してアクセスし <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> ます。 とインターフェイスはどちらも <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> テキストバッファーオブジェクト () によって実装され、を使用して相互に <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> アクセスでき `QueryInterface` ます。 次の図は、のこれらの主要なインターフェイスを示して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> います。  
  
 ![テキスト バッファー オブジェクト](../extensibility/media/vstextbuffer.gif "vsTextBuffer")  
テキストバッファーオブジェクト  
  
 どちらの座標系もテキストバッファー内で動作しますが、2次元座標を使用するように最適化されています。 1次元の座標系では、パフォーマンスのオーバーヘッドが生じる可能性があります。 したがって、可能な限り2次元の座標系を使用してください。  
  
 テキストバッファーの2番目の役割は、ファイルの永続化です。 これを行うには、テキストバッファーオブジェクトがを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> し、永続化に関係するプロジェクト項目およびその他の環境コンポーネントのドキュメントデータオブジェクトコンポーネントとして機能します。 詳細については、「 [プロジェクト項目を開いて保存](../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レガシ API を使用する表示設定の変更](../extensibility/changing-view-settings-by-using-the-legacy-api.md)  
 レガシ API を使用して表示設定を変更する方法について説明します。  
  
 [グローバル設定を監視するためのテキスト マネージャーの使用](../extensibility/using-the-text-manager-to-monitor-global-settings.md)  
 テキストマネージャーを使用してグローバル設定を監視する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [コア エディターの内部](../extensibility/inside-the-core-editor.md)
