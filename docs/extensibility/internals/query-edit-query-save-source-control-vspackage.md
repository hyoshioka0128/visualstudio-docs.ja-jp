---
title: クエリの編集クエリの保存 (ソース管理 VSPackage) |Microsoft Docs
description: Query-Edit Query-Save イベントの役割と、ソース管理 VSPackage によってイベントがどのように処理されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e320d6f7b6126736719eb2a428d47a39a61730ae
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837272"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>クエリの編集とクエリの保存 (ソース管理 VSPackage)
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] エディターでは、query Edit Query Save (QEQS) イベントをブロードキャストできます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理スタブは、QEQS イベントの受信者になるように QEQS サービスを実装します。 これらのイベントは、現在アクティブなソース管理 VSPackage に委任されます。 アクティブなソース管理 VSPackage は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> とそのメソッドを実装します。 通常、インターフェイスのメソッドは、 `IVsQueryEditQuerySave2` ドキュメントが最初に編集される直前と、ドキュメントが保存される直前に呼び出されます。

## <a name="queryeditquerysave-events"></a>QueryEditQuerySave イベント
 ソース管理 VSPackage は、 `IVsQueryEditQuerySave2` インターフェイスと必要なメソッドを実装することによって、QEQS イベントを処理する必要があります。 少なくとも VSPackage が実装する必要がある2つのメソッドについて、以下に簡単に説明します。 実際の実装は、ソース管理モデルのロジックに従っている必要があります。

### <a name="queryeditfiles-method"></a>QueryEditFiles メソッド
 は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> プロジェクトまたはエディターがファイルを変更するときに呼び出されます。 このメソッドは、ファイルが変更される前とファイルが保存される *前に* 呼び出されるのが理想的です。 このメソッドを呼び出すと、指定した `IVsQueryEditQuerySave2::QueryEditFiles` ファイルがソース管理下にあるかどうか、チェックアウトする必要があるかどうか、およびそれらを再読み込みできるかどうかがチェックされます。 状況によってファイルを編集できないようにすると、 `IVsQueryEditQuerySave2::QueryEditFiles` メソッドは呼び出し元のプログラムに対して編集をキャンセルするように指示します。 呼び出し元が呼び出しモードを指定することもできます。 "サイレント" モードでは、このメソッドは UI が表示されない場合にのみアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 メソッドはトランザクション方式で動作します。つまり、1つのファイルで編集がキャンセルされた場合、すべてのファイルに対して編集がキャンセルされます。 逆に、編集が許可されている場合は、すべてのファイルに対して許可されます。 このメソッドによって、特定のファイルセットに対して1回の編集が許可される場合は、同じファイルセットに対する後続の呼び出しでの編集が常に許可されている必要があります。 Allow-edit ループは、ファイルが閉じられ、保存されて、再読み込みされるまで続行されます。属性 (プロパティ) が変更されるまで、または、ソース管理パッケージが変更されます。 メソッドの実装で考慮すべきケースとしては、 `IVsQueryEditQuerySave2::QueryEditFiles` 複数のファイル、特別なファイル、ユーザーからのキャンセル、メモリ内の編集などがあります。

### <a name="querysavefiles-method"></a>QuerySaveFiles メソッド
 は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> プロジェクトまたはエディターがファイルのセットを保存する必要があるときに呼び出されます。 メソッドを呼び出すと、指定した `IVsQueryEditQuerySave2::QuerySaveFiles` ファイルが読み取り専用かどうか、およびソース管理下にあるかどうかがチェックされます。 ファイルをチェックアウトする必要がある場合は、呼び出しがソース管理パッケージに委任されます。 状況によってファイルが保存されないようにするには、メソッドで、 `IVsQueryEditQuerySave2::QuerySaveFiles` 保存をキャンセルするようにエディターに指示する必要があります。 メソッドと同様に、 `IVsQueryEditQuerySave2::QueryEditFiles` 呼び出し元が呼び出しモードを指定することもできます。 "サイレント" モードでは、このメソッドは UI が表示されない場合にのみアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 このメソッドは、トランザクション方式で動作する必要があります。つまり、1つのファイルで保存がキャンセルされた場合、すべてのファイルに対して保存が取り消されます。 逆に、保存が許可されている場合は、すべてのファイルに対して保存が許可されている必要があります。 メソッドの場合と同様に、メソッドの実装時には、 `IVsQueryEditQuerySave2::QueryEditFiles` `IVsQueryEditQuerySave2::QuerySaveFiles` 複数のファイル、特別なファイル、ユーザーからのキャンセル、メモリ内の編集などが考えられます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
