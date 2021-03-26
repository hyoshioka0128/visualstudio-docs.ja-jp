---
title: RDT_ReadLock 使用法 |Microsoft Docs
description: _VSRDTFLAGS について説明します。RDT_ReadLock フラグ。実行中のドキュメントテーブル内のドキュメントをロックするためのロジックを提供します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6add02e763c9664c19fe21b1cfc37dd29b3010b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060836"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock の使用法

[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) は、現在 Visual STUDIO IDE で開いているすべてのドキュメントの一覧である、実行中のドキュメントテーブル (RDT) 内のドキュメントをロックするためのロジックを提供するフラグです。 このフラグは、ドキュメントがいつ開かれるか、およびドキュメントがユーザーインターフェイスに表示されるか、またはメモリ内に非表示で保持されるかを決定します。

一般に、_VSRDTFLAGS を使用し [ます。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) 次のいずれかに該当する場合に RDT_ReadLock します。

- ドキュメントを非表示にして読み取り専用で開き、まだ作成していない場合は、それを所有する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。

- ユーザーが UI に表示されたドキュメントを保存するようにユーザーに要求し、その後、ユーザーがそれを閉じようとしました。

## <a name="how-to-manage-visible-and-invisible-documents"></a>表示および非表示のドキュメントを管理する方法

ユーザーが UI でドキュメントを開くときに、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ドキュメントの所有者と _VSRDTFLAGS を確立する必要があり [ます。RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>) フラグを設定する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>所有者を設定できない場合、ユーザーが [**すべて保存**] をクリックするか IDE を閉じると、ドキュメントは保存されません。 つまり、ドキュメントがメモリ内で変更されている場所で非表示になっている場合に、[ **すべて保存** ] を選択した場合に、ドキュメントをシャットダウンまたは保存するように求めるメッセージが表示された場合は、を `RDT_ReadLock` 使用できません。 代わりに、を使用して、__VSREGDOCLOCKHOLDER するときにを登録する必要があり `RDT_EditLock` <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> [ます。RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>) フラグ。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock とドキュメントの変更

前に説明したフラグは、ドキュメントが表示されているドキュメント `RDT_EditLock` **ウィンドウ** にユーザーがドキュメントを開いたときに、ドキュメントを開いていない状態になったときに、それを生成することを示しています。 この場合、表示されている **Documentwindow** が閉じられると、ユーザーには **保存** を求めるメッセージが表示されます。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` サービスを使用する実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> は、のみを取得した場合 `RDT_ReadLock` (つまり、ドキュメントが開いているときに情報を解析するために開かれた場合) に最初に動作します。 その後、ドキュメントを変更する必要がある場合は、ロックが脆弱な **RDT_EditLock** にアップグレードされます。 その後、ユーザーが表示されている **Documentwindow** でドキュメントを開くと、 `CodeModel` の脆弱 `RDT_EditLock` なが解放されます。

その後、ユーザーがドキュメント **ウィンドウ** を閉じて、開いているドキュメントを保存するように求められたときに [ **いいえ** ] を選択すると、実装はドキュメント `CodeModel` 内のすべての情報を破棄し、ドキュメントの追加情報が次に必要になったときには非表示になります。 この動作のはらみは、ユーザーが表示されていない開いているドキュメントの **Documentwindow** を開き、それを変更して閉じ、ドキュメントを保存するように求められたときに [ **いいえ** ] を選択したインスタンスです。 この場合、ドキュメントにが含まれていると、ドキュメントは実際には `RDT_ReadLock` 閉じられず、ユーザーがドキュメントを保存しないことを選択した場合でも、変更されたドキュメントはメモリ内で非表示になります。

ドキュメントが開いていない状態で使用されている場合は、 `RDT_EditLock` ユーザーがドキュメントを開いたときにロックが生成され、他のロックは保持されません。 ユーザーがドキュメントウィンドウを閉じ、ドキュメントを保存するように求められたら [**いいえ** **]** を選択すると、ドキュメントをメモリから閉じる必要があります。 これは、非表示のクライアントが、この発生を追跡するために RDT イベントをリッスンする必要があることを意味します。 ドキュメントが次に必要になったときに、ドキュメントを再度開く必要があります。
