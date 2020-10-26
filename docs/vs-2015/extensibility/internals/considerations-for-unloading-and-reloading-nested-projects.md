---
title: 入れ子になったプロジェクトのアンロードと再読み込みに関する考慮事項 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65145530c8cd6b68b82391a09b395bb8c9a61117
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197010"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

入れ子になったプロジェクトの種類を実装する場合は、プロジェクトをアンロードして再読み込みするときに、追加の手順を実行する必要があります。 リスナーにソリューションイベントを正しく通知するには、イベントとイベントを正しく発生させる必要があり `OnBeforeUnloadProject` `OnAfterLoadProject` ます。  
  
 このような状況でこれらのイベントを発生させる必要がある理由の1つは、ソースコード管理 (SCC) がサーバーから項目を削除してから、SCC からの操作がある場合に新しいものとして追加し直す必要がないことです `Get` 。 この場合、新しいファイルが SCC から読み込まれ、ファイルが異なる場合に備えて、すべてのファイルをアンロードして再読み込みする必要があります。 SCC 呼び出し `ReloadItem` 。 この呼び出しの実装では、プロジェクトを削除し、 `IVsFireSolutionEvents` とを呼び出すためにを実装することによって再作成し `OnBeforeUnloadProject` `OnAfterLoadProject` ます。 この実装を実行すると、SCC には、プロジェクトが一時的に削除され、再び追加されたことが通知されます。 そのため、SCC は、プロジェクトが実際にサーバーから削除された後に再び追加されたかのように、プロジェクトでは動作しません。  
  
## <a name="reloading-projects"></a>プロジェクトの再読み込み  
 入れ子になったプロジェクトの再読み込みをサポートするには、メソッドを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> ます。 の実装では `ReloadItem` 、入れ子になったプロジェクトを閉じてから再作成します。  
  
 通常、プロジェクトが再読み込みされると、IDE によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> イベントとイベントが発生し `M:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject(Microsoft.VisualStudio.Shell.Interop.IVsHierarchy,Microsoft.VisualStudio.Shell.Interop.IVsHierarchy)` ます。 ただし、入れ子になったプロジェクトを削除して再読み込みすると、IDE ではなく、親プロジェクトがプロセスを開始します。 親プロジェクトはソリューションイベントを発生させず、IDE にはプロセスの初期化に関する情報がないため、イベントは発生しません。  
  
 このプロセスを処理するために、親プロジェクトはインターフェイスからインターフェイスを呼び出し `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> ます。 `IVsFireSolutionEvents` には、入れ子になったプロジェクトをアンロードするように IDE に指示し、イベントを発生させて同じプロジェクトを再読み込みする機能があり `OnBeforeUnloadProject` `OnAfterLoadProject` ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
