---
title: 拡張とカスタマイズ ツール ウィンドウ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 76c094ec73a69baa46a5e8313dd26febd57e5887
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711815"
---
# <a name="extend-and-customize-tool-windows"></a>ツール ウィンドウの拡張とカスタマイズ
Visual Studio には、ツール ウィンドウ、ドキュメント ウィンドウ、ダイアログ ウィンドウなど、さまざまな種類のウィンドウが用意されています。 その他のウィンドウは、[**プロパティ]** ウィンドウ、[**出力**] ウィンドウ、および [**タスク一覧**] ウィンドウなど、ツール ウィンドウの種類です。

## <a name="tool-windows"></a>ツール ウィンドウ
 Visual Studio のツール ウィンドウは、通常、ファイル ベースではない読み取り専用ウィンドウです。 この点で、ツール ウィンドウは、読み取り/書き込みモードでファイルを表示するドキュメント ウィンドウと異なります。 **ツールボックス**、 **ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、および **Web ブラウザー** はツール ウィンドウの例です。

 簡単なツール ウィンドウの作成方法については、「ツール[ウィンドウを追加する](../extensibility/adding-a-tool-window.md)」を参照してください。

 Visual Studio でツール ウィンドウを登録するには、「[ツール ウィンドウの登録](../extensibility/registering-a-tool-window.md)」を参照してください。

 ツール ウィンドウは、既定では単一インスタンスです、つまり、一度に開くことができるツール ウィンドウのインスタンスは 1 つのみです。 単一インスタンスのツール ウィンドウを開いた後は、IDE が閉じられるまで開いたままです。 単一インスタンス ツール ウィンドウを閉じると、その表示設定だけが変更されます。 複数インスタンスのツール ウィンドウを作成して、ウィンドウの複数のインスタンスを同時に開くことも可能です。 詳細については、「[マルチインスタンス ツール ウィンドウの作成](../extensibility/creating-a-multi-instance-tool-window.md)」を参照してください。

 ツール ウィンドウは*動的*な 、つまり、関連する UI コンテキストが適用されるたびに表示されます。 自動表示の使用により、IDE でのウィンドウの煩雑さが軽減されます。 詳細については、「[動的ツール ウィンドウを開く](../extensibility/opening-a-dynamic-tool-window.md)」を参照してください。

 ツール ウィンドウは、ドッキング、フローティング、またはドキュメント フレームのタブ付けが可能です。 ツール ウィンドウの枠は IDE によって提供され、サイズ、位置、ドッキング状態と、その他の永続的なプロパティを制御するために使用します。 ツール ウィンドウのペインには、内容が表示されます。 既定のサイズと位置はツール ウィンドウを最初に開くときにのみ適用されます。その後、ツール ウィンドウの状態は保持されます。

 ツール ウィンドウのペインでは、WPF ユーザー コントロールをホストして、ツールバーをサポートすることができます。 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> プロパティをオーバーライドして、ホストされるコントロールのハンドルを返すことができます。

 ツール ウィンドウには、さまざまな機能を追加できます。 たとえば、ツールバーを追加できます: ツール ウィンドウまたはショートカット メニュー[にツールバーを追加](../extensibility/adding-a-toolbar-to-a-tool-window.md)する:[ツール ウィンドウにショートカット メニューを追加](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)します。 ツール ウィンドウ内のアイテムを検索できる検索コントロールを追加[できます。](../extensibility/adding-search-to-a-tool-window.md)

 ツール ウィンドウ イベントをサブスクライブできます:[イベントを購読](../extensibility/subscribing-to-an-event.md)します。

## <a name="extend-existing-tool-windows"></a>既存のツール ウィンドウを拡張する
 ツール ウィンドウに関する情報を新しい **[オプション]** ページに追加し、[**プロパティ]** ページの新しい設定を **[タスク一覧**] ウィンドウと **[出力**] ウィンドウに書き込むことができます。 詳細については、「[プロパティ ウィンドウ、タスク一覧ウィンドウ、出力ウィンドウ、およびオプション ウィンドウの拡張](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)」を参照してください。

## <a name="modal-dialog-boxes"></a>モーダル ダイアログ ボックス
 Visual Studio 拡張機能では、モーダル ダイアログ ボックスを<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName>から派生して作成する必要があります。 詳細については、「[モーダル ダイアログ ボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ツール ウィンドウを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)
- [プロジェクトの拡張](../extensibility/extending-projects.md)
- [ソリューションの拡張](../extensibility/extending-solutions.md)
