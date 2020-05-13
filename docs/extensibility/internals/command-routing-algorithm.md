---
title: コマンド ルーティング アルゴリズム |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af8d3e53e09214ce36a80ca18856085dfb2bb746
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709537"
---
# <a name="command-routing-algorithm"></a>コマンドルーティングアルゴリズム
Visual Studio では、コマンドはさまざまなコンポーネントによって処理されます。 コマンドは、現在の選択に基づく最も内側のコンテキストから最も外側の (グローバルとも呼ばれる) コンテキストにルーティングされます。 詳細については、[コマンドの可用性を](../../extensibility/internals/command-availability.md)参照してください。

## <a name="order-of-command-resolution"></a>コマンド解決の順序
 コマンドは、次のレベルのコマンド コンテキストを通じて渡されます。

1. アドイン: 環境では、まず、存在するすべてのアドインに対してコマンドを提供します。

2. 優先コマンド: これらのコマンドは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget>を使用して登録されます。 これらは Visual Studio のすべてのコマンドに対して呼び出され、登録された順序で呼び出されます。

3. コンテキスト メニュー コマンド: コンテキスト メニュー上にあるコマンドは、まずコンテキスト メニューに提供されるコマンド ターゲットに提供され、その後は通常のルーティングに提供されます。

4. ツールバー set コマンドターゲット: これらのコマンドターゲットは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A>を呼び出すときに登録されます。 パラメータ`pCmdTarget`は`null`. が使用されていない`null`場合、このコマンド ターゲットは、設定しているツールバーにあるコマンドを更新するために使用されます。 シェルがツールバーを設定している場合、ツールバー上の`pCmdTarget`コマンドに対するすべての更新が、フォーカスがなくてもウィンドウ フレームを通ってフローするように、ウィンドウ フレームとして渡されます。

5. ツール ウィンドウ: 通常はインターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>実装するツール ウィンドウは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>ツール ウィンドウがアクティブ ウィンドウのときに Visual Studio がコマンド ターゲットを取得できるように、インターフェイスも実装する必要があります。 ただし、フォーカスのあるツール ウィンドウが**プロジェクト**ウィンドウの場合、コマンドは選択した項目の<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>共通の親であるインターフェイスにルーティングされます。 この選択が複数のプロジェクトにまたがる場合、コマンドは階層にルーティング<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution>されます。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>には、インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>の<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>対応するコマンドに類似したメソッドと メソッドが<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>含まれています。

6. ドキュメント ウィンドウ: コマンドの`RouteToDocs`*.vsct*ファイルにフラグが設定されている場合、Visual Studio は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>ドキュメント<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>ビュー オブジェクトのコマンド ターゲットを検索します。 ドキュメント ビュー オブジェクトがコマンドをサポートしていない場合、Visual Studio は返される<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスにコマンドをルーティングします。 (これは、ドキュメント データ オブジェクトのオプションのインターフェイスです)。

7. 現在の階層: 現在の階層は、アクティブなドキュメント ウィンドウを所有するプロジェクト、またはソリューション**エクスプローラ**で選択した階層にすることができます。 Visual Studio は<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>、現在の階層 (アクティブな階層) に実装されているインターフェイスを検索します。 階層は、プロジェクト項目のドキュメント ウィンドウにフォーカスがある場合でも、階層がアクティブな場合は常に有効なコマンドをサポートする必要があります。 ただし、**ソリューション エクスプローラー**にフォーカスがある場合にのみ適用されるコマンドは<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>、インターフェイスとその<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>使用してサポートする必要があります。

     **切り取り**、**コピー**、**貼り付け**、**削除**、**名前の変更**、**入力**、および**ダブルクリック**の各コマンドには、特別な処理が必要です。 階層内の**削除**コマンドと**削除**コマンドを処理する方法については、インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>参照してください。

8. グローバル: 前述のコンテキストでコマンドが処理されていない場合、Visual Studio はインターフェイスを実装するコマンドを所有する VSPackage にコマンドを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>ルーティングしようとします。 VSPackage がまだ読み込まれていない場合は、Visual Studio がメソッドを呼<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>び出すときに読み込まれません。 VSPackage は、メソッドが<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>呼び出されたときにのみ読み込まれます。

## <a name="see-also"></a>関連項目
- [コマンド設計](../../extensibility/internals/command-design.md)
