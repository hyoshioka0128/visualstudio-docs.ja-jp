---
title: ネストされたプロジェクトのコマンド処理の実装 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707608"
---
# <a name="implementing-command-handling-for-nested-projects"></a>入れ子になったプロジェクト向けのコマンド処理の実装
IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>および<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスを介して入れ子になったプロジェクトに渡されるコマンドを渡すことができます。

> [!NOTE]
> 親プロジェクトが通常処理するコマンドのみをフィルター処理できます。 IDE によって処理される**ビルド**や**配置**などのコマンドは、フィルター処理できません。

 次の手順では、コマンド処理を実装するプロセスについて説明します。

## <a name="procedures"></a>プロシージャ

#### <a name="to-implement-command-handling"></a>コマンド処理を実装するには

1. ネストされたプロジェクトまたはネストされたプロジェクトのノードをユーザーが選択すると、次のようになります。

   1. IDE がメソッド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>を呼び出します。

      - または -

   2. ソリューション エクスプローラーのショートカット メニュー コマンドなど、階層ウィンドウでコマンドが作成された場合、IDE はプロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>の親のメソッドを呼び出します。

2. 親プロジェクトは、 や`QueryStatus``pguidCmdGroup``prgCmds`など、 に渡すパラメーターを調べて、親プロジェクトがコマンドをフィルター処理するかどうかを判断できます。 親プロジェクトがコマンドをフィルタするために実装されている場合は、次のように設定する必要があります。

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    次に、親プロジェクトは`S_OK`を返す必要があります。

    親プロジェクトがコマンドをフィルタしない場合は、 を返す`S_OK`だけです。 この場合、IDE は自動的にコマンドを子プロジェクトにルーティングします。

    親プロジェクトは、コマンドを子プロジェクトにルーティングする必要はありません。 IDE はこのタスクを実行します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
