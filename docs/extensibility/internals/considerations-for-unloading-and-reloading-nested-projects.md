---
title: 入れ子になったプロジェクトのアンロードと再読み込み
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 154eb51014d9719b601cf87d53383f57941403a8
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036822"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>入れ子になったプロジェクトのアンロードと再読み込みに関する考慮事項

入れ子になったプロジェクトの種類を実装する場合は、プロジェクトをアンロードして再読み込みするときに、追加の手順を実行する必要があります。 リスナーにソリューションイベントを正しく通知するには、イベントとイベントを正しく発生させる必要があり `OnBeforeUnloadProject` `OnAfterLoadProject` ます。

これらのイベントを発生させる理由の1つは、ソースコード管理 (SCC) 用です。 Scc がサーバーから項目を削除してから、SCC からの操作がある場合は *新しい* ものとして追加し直す必要はありません `Get` 。 その場合は、新しいファイルが SCC から読み込まれます。 ファイルが異なっている場合は、すべてのファイルをアンロードして再読み込みする必要があります。

ソースコード管理 `ReloadItem` の呼び出し。 を <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> 呼び出し、プロジェクトを `OnBeforeUnloadProject` 削除して再作成するためのインターフェイスを実装し `OnAfterLoadProject` ます。 この方法でインターフェイスを実装すると、SCC には、プロジェクトが一時的に削除され、再び追加されたことが通知されます。 そのため、SCC は、プロジェクトが *実際* に削除され、再追加されたかのように、プロジェクトでは動作しません。

## <a name="reload-projects"></a>プロジェクトの再読み込み

入れ子になったプロジェクトの再読み込みをサポートするには、メソッドを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> ます。 の実装では `ReloadItem` 、入れ子になったプロジェクトを閉じてから再作成します。

通常、プロジェクトが再読み込みされると、IDE によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> イベントとイベントが発生し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> ます。 ただし、入れ子になったプロジェクトを削除して再読み込みする場合、親プロジェクトは IDE ではなくプロセスを開始します。 親プロジェクトはソリューションイベントを発生させず、IDE にはプロセスの初期化に関する情報がないため、イベントは発生しません。

このプロセスを処理するために、親プロジェクトは `QueryInterface` インターフェイスでを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> ます。 `IVsFireSolutionEvents` には、入れ子になったプロジェクトをアンロードするように IDE に指示し、イベントを発生させて同じプロジェクトを再読み込みする機能があり `OnBeforeUnloadProject` `OnAfterLoadProject` ます。

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [入れ子 (プロジェクトを)](../../extensibility/internals/nesting-projects.md)
