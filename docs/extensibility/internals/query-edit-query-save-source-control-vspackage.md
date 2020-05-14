---
title: クエリ編集クエリの保存 (ソース管理 VSPackage) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c09ac0cb4f51b8f2484b95d403ff6d0445631479
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705970"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>クエリの編集とクエリの保存 (ソース管理 VSPackage)
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]編集者は、クエリ編集クエリ保存 (QEQS) イベントをブロードキャストできます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理スタブは、QEQS イベントの受信者となるように、QEQS サービスを実装します。 これらのイベントは、現在アクティブなソース管理 VSPackage に委任されます。 アクティブなソース管理 VSPackage は<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>、およびそのメソッドを実装します。 `IVsQueryEditQuerySave2`通常、このインタフェースのメソッドは、ドキュメントが最初に編集される直前、およびドキュメントが保存される直前に呼び出されます。

## <a name="queryeditquerysave-events"></a>クエリ編集クエリ イベントの保存
 ソース管理の VSPackage は、インターフェイスと必要なメソッドを`IVsQueryEditQuerySave2`実装することによって、QEQS イベントを処理する必要があります。 以下は、VSPackage が実装する必要がある 2 つのメソッドの簡単な説明です。 実際の実装は、ソース管理モデルのロジックに従って行う必要があります。

### <a name="queryeditfiles-method"></a>メソッドを編集します。
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>プロジェクトまたはエディターがファイルを変更する場合に呼び出されます。 理想的には、このメソッドは、ファイルが変更される*前*とファイルが保存されるときに呼び出されます。 メソッドを呼び出`IVsQueryEditQuerySave2::QueryEditFiles`すと、指定したファイルがソース管理下にあるかどうか、チェックアウトする必要があるかどうか、および再読み込みできるかどうかがチェックされます。 状況によってファイルが編集可能になれない場合、`IVsQueryEditQuerySave2::QueryEditFiles`メソッドは呼び出し元のプログラムに編集を取り消すように指示します。 呼び出し元が呼び出しモードを指定することもできます。 "サイレント" モードでは、このメソッドは UI が表示されない場合にのみアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 このメソッドはトランザクション方式で動作します。つまり、1 つのファイルで編集が取り消されると、すべてのファイルの編集が取り消されます。 逆に、編集が許可されている場合は、すべてのファイルに対して許可されます。 このメソッドで特定のファイル セットの編集を 1 回許可する場合は、同じファイル セットの後続の呼び出しで常に編集を許可する必要があります。 許可/編集ループは、ファイルが閉じられ、保存され、再ロードされるまで続きます。属性 (プロパティ) が変更されるまで。または、ソース管理パッケージが変更されるまで。 メソッドの実装で考慮すべき`IVsQueryEditQuerySave2::QueryEditFiles`ケースとしては、複数のファイル、特殊なファイル、ユーザーからのキャンセル、メモリ内の編集などがあります。

### <a name="querysavefiles-method"></a>メソッドを保存します。
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>は、プロジェクトまたはエディターがファイルのセットを保存する必要がある場合に呼び出されます。 メソッドを呼び出`IVsQueryEditQuerySave2::QuerySaveFiles`すと、指定されたファイルが読み取り専用かどうか、およびソース管理下にあるかどうかをチェックします。 ファイルをチェックアウトする必要がある場合は、呼び出しがソース管理パッケージに委任されます。 状況によってファイルの保存ができない場合、`IVsQueryEditQuerySave2::QuerySaveFiles`メソッドはエディターに保存を取り消す必要があります。 メソッドと同様`IVsQueryEditQuerySave2::QueryEditFiles`に、呼び出し元が呼び出しモードを指定することもできます。 "サイレント" モードでは、このメソッドは UI が表示されない場合にのみアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 このメソッドはトランザクション的に動作する必要があります。つまり、1 つのファイルで保存が取り消されると、すべてのファイルの保存が取り消されます。 逆に、保存が許可されている場合は、すべてのファイルに対して許可する必要があります。 メソッドと同様`IVsQueryEditQuerySave2::QueryEditFiles`に、`IVsQueryEditQuerySave2::QuerySaveFiles`メソッドの実装で考慮すべきケースとして、複数のファイル、特殊なファイル、ユーザーからのキャンセル、およびメモリ内の編集が含まれます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
