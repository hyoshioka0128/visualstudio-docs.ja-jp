---
title: 入れ子になったプロジェクトのコマンド処理の実装 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2092fc8033d5a5cc53b12bd63a945bd9865ca30e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707608"
---
# <a name="implementing-command-handling-for-nested-projects"></a>入れ子になったプロジェクト向けのコマンド処理の実装
IDE では、およびインターフェイスを介して渡されたコマンドを <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 入れ子になったプロジェクトに渡すことができます。また、親プロジェクトはコマンドをフィルター処理またはオーバーライドできます。

> [!NOTE]
> 通常、親プロジェクトによって処理されるコマンドのみをフィルター処理できます。 IDE によって処理される **ビルド** や **配置** などのコマンドはフィルター処理できません。

 次の手順では、コマンド処理を実装するプロセスについて説明します。

## <a name="procedures"></a>手順

#### <a name="to-implement-command-handling"></a>コマンド処理を実装するには

1. 入れ子になったプロジェクトまたは入れ子になったプロジェクト内のノードをユーザーが選択すると、次のようになります。

   1. IDE はメソッドを呼び出し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ます。

      または

   2. ソリューションエクスプローラーのショートカットメニューコマンドなど、階層ウィンドウでコマンドが生成された場合、IDE は <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> プロジェクトの親のメソッドを呼び出します。

2. 親プロジェクトは、に渡されるパラメーター (やなど) を調べて、 `QueryStatus` `pguidCmdGroup` `prgCmds` 親プロジェクトがコマンドをフィルター処理する必要があるかどうかを判断できます。 フィルターコマンドに親プロジェクトが実装されている場合は、次のように設定する必要があります。

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    次に、親プロジェクトからが返さ `S_OK` れます。

    親プロジェクトがコマンドをフィルター処理しない場合は、を返すだけ `S_OK` です。 この場合、IDE はコマンドを子プロジェクトに自動的にルーティングします。

    親プロジェクトは、子プロジェクトにコマンドをルーティングする必要がありません。 IDE がこのタスクを実行します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
