---
title: RDT_ReadLock 使用法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9a6b5f86f0cfbb71f6264bdc74df72ad9209c9d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154134"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock の使用法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> は、Visual Studio IDE で現在開いているすべてのドキュメントの一覧である、実行中のドキュメントテーブル (RDT) 内のドキュメントをロックするためのロジックを提供するフラグです。 このフラグは、ドキュメントがいつ開かれるか、およびドキュメントがユーザーインターフェイスに表示されるか、またはメモリ内に非表示で保持されるかを決定します。  
  
 通常、 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 次のいずれかに該当する場合は、を使用します。  
  
- ドキュメントを非表示または読み取り専用で開くが、まだ確立されていない場合は、それを所有する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。  
  
- ユーザーが UI に表示されている前に開いていたドキュメントを保存するようにユーザーに要求した後、そのドキュメントを閉じようとした場合。  
  
## <a name="how-to-manage-visible-and-invisible-documents"></a>表示および非表示のドキュメントを管理する方法  
 ユーザーが UI でドキュメントを開くときには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ドキュメントの所有者を設定し、 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> フラグを設定する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>所有者を設定できない場合、ユーザーが [**すべて保存**] をクリックするか IDE を閉じると、ドキュメントは保存されません。 つまり、ドキュメントがメモリ内で変更されている場所で非表示になっている場合に、[ **すべて保存** ] を選択した場合に、ドキュメントをシャットダウンまたは保存するように求めるメッセージが表示された場合は、を `RDT_ReadLock` 使用できません。 代わりに、を使用し、フラグが指定さ `RDT_EditLock` れたときにを登録する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> <xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER> ます。  
  
## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock とドキュメントの変更  
 前に説明したフラグは、ドキュメントが表示されているドキュメント `RDT_EditLock` **ウィンドウ**にユーザーがドキュメントを開いたときに、ドキュメントを開いていない状態になったときに、それを生成することを示しています。 この場合、表示されている**Documentwindow**が閉じられると、ユーザーには**保存**を求めるメッセージが表示されます。 サービスを使用する VisualStudio 実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> `RDT_ReadLock` は、が取得されたとき (つまり、ドキュメントを開いて情報を解析するために非表示になったとき) に最初に動作します。 その後、ドキュメントを変更する必要がある場合は、ロックが脆弱な **RDT_EditLock**にアップグレードされます。 その後、ユーザーが表示されている **Documentwindow**でドキュメントを開くと、 `CodeModel` の脆弱 `RDT_EditLock` なが解放されます。  
  
 その後、ユーザーがドキュメント **ウィンドウ** を閉じて、開いているドキュメントを保存するように求められたときに [ **いいえ** ] を選択すると、実装はドキュメント `CodeModel` 内のすべての情報を破棄し、ドキュメントの追加情報が次に必要になったときには非表示になります。 この動作のはらみは、ユーザーが表示されていない開いているドキュメントの **Documentwindow** を開き、それを変更して閉じ、ドキュメントを保存するように求められたときに [ **いいえ** ] を選択したインスタンスです。 この場合、ドキュメントにが含まれていると、ドキュメントは実際には `RDT_ReadLock` 閉じられず、ユーザーがドキュメントを保存しないことを選択した場合でも、変更されたドキュメントはメモリ内で非表示になります。  
  
 ドキュメントが開いていない状態で使用されている場合は、 `RDT_EditLock` ユーザーがドキュメントを開いたときにロックが生成され、他のロックは保持されません。 ユーザーがドキュメントウィンドウを閉じ、ドキュメントを保存するように求められたら [**いいえ** **]** を選択すると、ドキュメントをメモリから閉じる必要があります。 これは、非表示のクライアントが、この発生を追跡するために RDT イベントをリッスンする必要があることを意味します。 ドキュメントが次に必要になったときに、ドキュメントを再度開く必要があります。
