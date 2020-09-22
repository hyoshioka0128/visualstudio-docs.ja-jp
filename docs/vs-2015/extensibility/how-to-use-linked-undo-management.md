---
title: '方法: リンクされた元に戻す管理を使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - linked undo management
ms.assetid: af5cc22a-c9cf-45b1-a894-1022d563f3ca
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 67d0d173909b8cdfe2eaf0d56aa5c99c437d5ad8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841588"
---
# <a name="how-to-use-linked-undo-management"></a>方法: リンクされた元に戻すの管理を使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[リンクされた元に戻す] を使用すると、複数のファイルで同じ編集を同時に元に戻すことができます。 たとえば、ヘッダーファイルや Visual C++ ファイルなど、複数のプログラムファイルにまたがるテキストの同時変更は、リンクされた undo トランザクションです。 リンクされた元に戻す機能は、元に戻すマネージャーの環境の実装に組み込まれており、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> この機能を操作できます。 リンクされた undo は、個別の undo スタックをリンクして1つの取り消し単位として扱うことができる、親の取り消し単位によって実装されます。 リンクされた元に戻す操作の手順については、次のセクションで詳しく説明します。  
  
### <a name="to-use-linked-undo"></a>リンクされた元に戻すを使用するには  
  
1. へ `QueryService` の `SVsLinkedUndoManager` ポインターを取得するには、を呼び出し `IVsLinkedUndoTransactionManager` ます。  
  
2. を呼び出して、親のリンクされた最初の undo 単位を作成し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.OpenLinkedUndo%2A> ます。 これにより、元に戻すスタックのセットの開始点が、リンクされた元に戻すスタックにグループ化されます。 メソッドでは `OpenLinkedUndo` 、リンクされた元に戻すを厳密にするかどうかを指定する必要もあります。 非厳密にリンクされた元に戻す動作では、リンクされた undo 兄弟を持つドキュメントの一部を閉じても、他のリンク元の undo 兄弟をスタックに残しておくことができます。 厳密にリンクされた元に戻す動作では、すべてのリンク元に戻す兄弟スタックをまとめて戻すか、まったく使用しないかを指定します。 [IOleUndoManager:: Add](/windows/desktop/api/ocidl/nf-ocidl-ioleundomanager-add)メソッドを呼び出して、後続のリンク元の undo スタックを追加します。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager.CloseLinkedUndo%2A>を呼び出して、リンクされているすべての undo ユニットを1としてロールバックします。  
  
    > [!NOTE]
    > エディターでリンクされた元に戻す管理を実装するには、[元に戻す] 管理を追加します。 リンクされた元に戻す管理の実装の詳細については、「 [方法: 元に戻す管理を実装](../extensibility/how-to-implement-undo-management.md)する」を参照してください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>   
 [IOleParentUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleparentundounit)   
 [IOleUndoUnit](/windows/desktop/api/ocidl/nn-ocidl-ioleundounit)   
 [方法: 元に戻すの管理を実装する](../extensibility/how-to-implement-undo-management.md)
