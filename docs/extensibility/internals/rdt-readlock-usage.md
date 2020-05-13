---
title: RDT_ReadLockの使用法 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fb897fab61e1e14b52863b5853748c685200d5ba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705927"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock の使用法

[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)は、実行中のドキュメント テーブル (RDT) でドキュメントをロックするためのロジックを提供するフラグです。 このフラグは、ドキュメントを開くタイミング、およびドキュメントがユーザー インターフェイスで表示されるか、メモリ内に表示されない状態かどうかを決定します。

一般的に[、_VSRDTFLAGSを使用します。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)次のいずれかが当てはまる場合です。

- ドキュメントを目に見えない状態で読み取り専用で開きたいのですが、ドキュメントを<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>所有する必要があるドキュメントはまだ確立されていません。

- ユーザーが UI に表示される前に目に見えない形で開かれたドキュメントを保存するように求めるメッセージを表示し、それを閉じようとします。

## <a name="how-to-manage-visible-and-invisible-documents"></a>表示/非表示ドキュメントの管理方法

ユーザーが UI でドキュメントを開くときに<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、ドキュメントの所有者を確立し、_VSRDTFLAGSする必要があります[。RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>)フラグを設定する必要があります。 所有者を<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>設定できない場合、ユーザーが **[すべて保存**] をクリックするか、IDE を閉じると、ドキュメントは保存されません。 つまり、メモリ内で変更された場所でドキュメントが目に見えない状態で開かれ、ユーザーがシャットダウン時にドキュメントを保存するか、[**すべて保存**] を選択した場合に`RDT_ReadLock`保存するように求めるメッセージが表示された場合は、 を使用できません。 代わりに、 を`RDT_EditLock`使用し<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>[、__VSREGDOCLOCKHOLDERを登録する必要があります。RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>)フラグ。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLockとドキュメントの変更

前述のフラグは、ドキュメントがユーザーによって開かれ、表示されている`RDT_EditLock`**DocumentWindow**にドキュメントが開かれたときに、ドキュメントを非表示にして開く場合に表示されることを示します。 この場合、表示されている**DocumentWindow**が閉じられると、ユーザーに**保存**のプロンプトが表示されます。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel`サービスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager>使用する実装は、最初にが`RDT_ReadLock`取られた場合(つまり、ドキュメントが情報を解析するために目に見えないほど開かれた場合)に機能します。 後でドキュメントを変更する必要がある場合は、ロックが弱い**RDT_EditLock**にアップグレードされます。 ユーザーが表示されている**DocumentWindow**でドキュメントを開くと、'`CodeModel``RDT_EditLock`弱い' が解放されます。

開いているドキュメントを保存するように求められたときにユーザーが**DocumentWindow**を閉じて **[いいえ**] を`CodeModel`選択すると、実装はドキュメント内のすべての情報を破棄し、次回ドキュメントに関してより多くの情報が必要になったときに、ドキュメントを目に見えない形で開きます。 この動作の微妙な点は、ユーザーが非表示の開いているドキュメントの**DocumentWindow を**開いて変更し、閉じ、ドキュメントを保存するように求められたときに **[いいえ**] を選択するインスタンスです。 この場合、ドキュメントに`RDT_ReadLock`が含まれる場合、ドキュメントは実際には閉じず、ユーザーがドキュメントを保存しないことを選択したにもかかわらず、変更されたドキュメントはメモリ内で目に見えない形で開いたままになります。

ドキュメントの非表示の開口部が弱`RDT_EditLock`を使用している場合、ユーザーがドキュメントを目に見えて開いたときにロックが発生し、他のロックは保持されません。 ユーザーが**DocumentWindow**を閉じ、ドキュメントを保存するかどうかを確認するメッセージが表示されたときに **[いいえ**] を選択すると、ドキュメントをメモリから閉じる必要があります。 つまり、非表示のクライアントは、この発生を追跡するために RDT イベントをリッスンする必要があります。 次回ドキュメントが必要な場合は、ドキュメントを再度開く必要があります。
