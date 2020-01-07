---
title: RDT_ReadLock の使用法 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154134"
---
# <a name="rdtreadlock-usage"></a>RDT_ReadLock の使用法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> これは、Visual Studio IDE で現在開いているすべてのドキュメントの一覧で、実行されているドキュメント テーブル (RDT)、ドキュメントをロックするためのロジックを提供するフラグ。 このフラグは、ドキュメントが開かれた文書は、ユーザー インターフェイスに表示されるか、メモリの目に見えない形で保持されているかどうかを判断します。  
  
 一般に、使用するよう<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>次のいずれかが true の場合。  
  
- ドキュメントを自動的に開く場合、読み取り専用はまだが確立されていることが、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>所有する必要があります。  
  
- ユーザーが、ユーザーの前に自動的に開かれたドキュメントを保存するよう求める場合は、UI に表示されることと閉じるましょう。  
  
## <a name="how-to-manage-visible-and-invisible-documents"></a>表示と非表示のドキュメントを管理する方法  
 ユーザーが UI では、ドキュメントを開いたときに、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>ドキュメントの所有者を確立する必要があります、<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>フラグを設定する必要があります。 ない場合は<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>所有者が確立されると、その後、ユーザーがクリックしたときに、ドキュメントは保存されません**すべて保存**または IDE を終了します。 かどうか、ドキュメントが開いていない視覚的、メモリ内で変更されていて、ユーザーがシャット ダウン時にドキュメントを保存するように求めまたは保存つまり**すべて保存**を選択した場合、`RDT_ReadLock`は使用できません。 代わりに、使用する必要があります、`RDT_EditLock`を登録し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>ときに、<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER>フラグ。  
  
## <a name="rdteditlock-and-document-modification"></a>RDT_EditLock とドキュメントの変更  
 前に説明されているフラグは、ドキュメントの非表示の開始を生成することを示します、`RDT_EditLock`ドキュメントが開かれた場合、ユーザーに表示されている**ドキュメント ウィンドウ**します。 この問題が発生すると、ユーザーがで表示されます。 を**保存**求めるときに、表示可能な**ドキュメント ウィンドウ**が閉じられました。 Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel 実装を使用する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager>のみに最初に、サービスが動作を`RDT_ReadLock`は (つまり、ドキュメントを開いたときにない視覚的情報を解析する) を取得します。 後で、ドキュメントを変更する必要があります、ロックにアップグレード、弱**RDT_EditLock**します。 ユーザーが表示されているでし、ドキュメントを開く場合**ドキュメント ウィンドウ**、`CodeModel`の弱い`RDT_EditLock`解放されます。  

ユーザーが終了した場合、**ドキュメント ウィンドウ**選択**いいえ**、開いているドキュメントを保存するように求められたら、`CodeModel`実装は、ドキュメント内のすべての情報を破棄し、再度開かれます、ディスクの詳細については、ドキュメントに必要な次の時間目に見えない形からドキュメントです。 この動作の細部は、ユーザーが開いたインスタンス、**ドキュメント ウィンドウ**、非表示の開いているドキュメントの変更が閉じるし、選択**いいえ**文書を保存するように求められたらします。 この場合は、ドキュメントがある場合、`RDT_ReadLock`ドキュメントは実際に閉じられましていないおよび文書を保存していないユーザーが選択した場合でもに、変更したドキュメントがメモリを目に見えない形で開いたままです。  
  
 ドキュメントの非表示の開始、弱を使用している場合`RDT_EditLock`、ユーザーが文書がはっきりと他のロックが保持されていないときにそのロックを得られます。 ユーザーが閉じたとき、**ドキュメント ウィンドウ**選択**いいえ**ドキュメントの保存を求められたら、ドキュメント閉じる必要がありますメモリから。 つまり、非表示のクライアントは、この状況の発生を追跡するために RDT イベントをリッスンする必要があります。 ドキュメントが必要になる、次に、ドキュメントを再開する必要があります。
