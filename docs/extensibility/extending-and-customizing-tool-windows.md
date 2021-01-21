---
title: ツールウィンドウの拡張とカスタマイズ |Microsoft Docs
description: プロパティウィンドウ、出力ウィンドウ、タスク一覧ウィンドウなど、Visual Studio に用意されているツールウィンドウの拡張とカスタマイズについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: ca7f6aa0c029cd3d85ba569aa93d6ae2087afd52
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995864"
---
# <a name="extend-and-customize-tool-windows"></a>ツールウィンドウの拡張とカスタマイズ
Visual Studio には、ツールウィンドウ、ドキュメントウィンドウ、ダイアログウィンドウなど、いくつかの異なる種類のウィンドウが用意されています。 [ **プロパティ** ] ウィンドウ、[ **出力** ] ウィンドウ、[ **タスク一覧** ] ウィンドウなどの他のウィンドウは、ツールウィンドウの種類です。

## <a name="tool-windows"></a>ツール ウィンドウ
 通常、Visual Studio ツールウィンドウは、ファイルベースではない読み取り専用のウィンドウです。 この点で、ツール ウィンドウは、読み取り/書き込みモードでファイルを表示するドキュメント ウィンドウと異なります。 **ツールボックス**、 **ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、および **Web ブラウザー** はツール ウィンドウの例です。

 単純なツールウィンドウを作成する方法については、「 [ツールウィンドウの追加](../extensibility/adding-a-tool-window.md)」を参照してください。

 ツールウィンドウを Visual Studio に登録するには、「 [ツールウィンドウを登録](../extensibility/registering-a-tool-window.md)する」を参照してください。

 ツール ウィンドウは、既定では単一インスタンスです、つまり、一度に開くことができるツール ウィンドウのインスタンスは 1 つのみです。 単一インスタンスのツール ウィンドウを開いた後は、IDE が閉じられるまで開いたままです。 単一インスタンスのツールウィンドウを閉じると、その可視性だけが変化します。 複数インスタンスのツール ウィンドウを作成して、ウィンドウの複数のインスタンスを同時に開くことも可能です。 詳細について [は、「複数インスタンスのツールウィンドウを作成する](../extensibility/creating-a-multi-instance-tool-window.md) 」を参照してください。

 ツールウィンドウは *動的* にすることができます。つまり、関連する UI コンテキストが適用されるたびに表示されます。 自動表示の使用により、IDE でのウィンドウの煩雑さが軽減されます。 詳細については、「 [動的ツールウィンドウを開く](../extensibility/opening-a-dynamic-tool-window.md)」を参照してください。

 ツール ウィンドウは、ドッキング、フローティング、またはドキュメント フレームのタブ付けが可能です。 ツール ウィンドウの枠は IDE によって提供され、サイズ、位置、ドッキング状態と、その他の永続的なプロパティを制御するために使用します。 ツール ウィンドウのペインには、内容が表示されます。 既定のサイズと位置はツール ウィンドウを最初に開くときにのみ適用されます。その後、ツール ウィンドウの状態は保持されます。

 ツール ウィンドウのペインでは、WPF ユーザー コントロールをホストして、ツールバーをサポートすることができます。 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> プロパティをオーバーライドして、ホストされるコントロールのハンドルを返すことができます。

 ツールウィンドウには、さまざまな機能を追加できます。 たとえば、ツールバーを追加したり、ツールウィンドウにツール [バーを追加](../extensibility/adding-a-toolbar-to-a-tool-window.md) したり、ショートカットメニューを追加したりできます。 [ツールウィンドウにショートカットメニューを追加](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)する方法です。 ツールウィンドウ内の項目を検索するための検索コントロールを追加できます。 [ツールウィンドウに [検索] を追加](../extensibility/adding-search-to-a-tool-window.md)します。

 ツールウィンドウイベントをサブスクライブできます。 [イベントをサブスクライブ](../extensibility/subscribing-to-an-event.md)します。

## <a name="extend-existing-tool-windows"></a>既存のツールウィンドウを拡張する
 新しい **オプション** ページにツールウィンドウに関する情報を追加し、[ **プロパティ** ] ページで新しい設定を追加して、[ **タスク一覧** と **出力** ] ウィンドウに書き込むことができます。 詳細については、「 [プロパティ、タスク一覧、出力、およびオプションの各ウィンドウを拡張する](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)」を参照してください。

## <a name="modal-dialog-boxes"></a>モーダルダイアログボックス
 Visual Studio 拡張機能では、モーダルダイアログボックスをから派生させることによって作成する必要があり <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName> ます。これにより、コントロールと残りの UI を制御できます。 詳細については、「 [モーダルダイアログボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [ツールウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)
- [プロジェクトの拡張](../extensibility/extending-projects.md)
- [ソリューションの拡張](../extensibility/extending-solutions.md)
