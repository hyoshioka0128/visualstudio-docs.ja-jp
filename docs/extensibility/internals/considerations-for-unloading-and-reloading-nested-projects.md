---
title: ネストされたプロジェクトのアンロードと再ロードに関する考慮事項 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2ab705953eea1fcac99883bb4f88c0e95eced108
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709297"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項

入れ子になったプロジェクトの種類を実装する場合は、プロジェクトをアンロードして再読み込みするときに、追加の手順を実行する必要があります。 ソリューション イベントにリスナーに正しく通知するには、 イベントと`OnBeforeUnloadProject``OnAfterLoadProject`イベントを正しく発生させる必要があります。

これらのイベントを発生させる理由の 1 つは、ソース コード管理 (SCC) です。 SCC から`Get`操作がある場合、SCC がサーバーから項目を削除し、*新しい*アイテムとして追加し直す必要はありません。 その場合、新しいファイルは SCC からロードされます。 ファイルが異なる場合に備えて、すべてのファイルをアンロードして再読み込みする必要があります。

ソース コード管理`ReloadItem`呼び出し。 呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>出`OnBeforeUnloadProject`し、プロジェクト`OnAfterLoadProject`を削除して再作成するインターフェイスを実装します。 この方法でインターフェイスを実装すると、SCC はプロジェクトが一時的に削除され、再度追加されたことを通知されます。 したがって、SCC はプロジェクトが*実際*に削除されて再追加されたかのようにプロジェクトを操作しません。

## <a name="reload-projects"></a>プロジェクトの再読み込み

入れ子になったプロジェクトの再読み込みをサポート<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>するには、メソッドを実装します。 の`ReloadItem`実装で、入れ子になったプロジェクトを閉じてから、それらを再作成します。

通常、プロジェクトが再読み込みされると、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A>は<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A>イベントと イベントを発生させます。 ただし、削除および再読み込みされたネストされたプロジェクトの場合、親プロジェクトは IDE ではなくプロセスを開始します。 親プロジェクトはソリューションイベントを発生させず、IDE にはプロセスの初期化に関する情報がないため、イベントは発生しません。

このプロセスを処理するために、親プロジェクトは`QueryInterface`インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents>呼び出します。 `IVsFireSolutionEvents`には、入れ子になったプロジェクトをアンロード`OnBeforeUnloadProject`するイベントを発生させ、イベントを発生させ、同`OnAfterLoadProject`じプロジェクトを再読み込みする関数があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [プロジェクトのネスト](../../extensibility/internals/nesting-projects.md)
