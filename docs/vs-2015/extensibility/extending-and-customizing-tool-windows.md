---
title: ツールウィンドウの拡張とカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b232fa1275bce453e3b32cea6a5ff37fdd501c6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204545"
---
# <a name="extending-and-customizing-tool-windows"></a>ツール ウィンドウの拡張とカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio には、ツールウィンドウ、ドキュメントウィンドウ、ダイアログウィンドウなど、いくつかの異なる種類のウィンドウが用意されています。 プロパティウィンドウ、[出力] ウィンドウ、[タスク一覧] ウィンドウなどの他のウィンドウは、ツールウィンドウの種類です。  
  
## <a name="tool-windows"></a>ツール ウィンドウ  
 通常、Visual Studio ツールウィンドウは、ファイルベースではない読み取り専用のウィンドウです。 この点で、ツール ウィンドウは、読み取り/書き込みモードでファイルを表示するドキュメント ウィンドウと異なります。 **ツールボックス**、 **ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、および **Web ブラウザー** はツール ウィンドウの例です。  
  
 単純なツールウィンドウを作成する方法については、「 [ツールウィンドウの追加](../extensibility/adding-a-tool-window.md)」を参照してください。  
  
 ツールウィンドウを Visual Studio に登録する方法については、「 [ツールウィンドウの登録](../extensibility/registering-a-tool-window.md)」を参照してください。  
  
 ツール ウィンドウは、既定では単一インスタンスです、つまり、一度に開くことができるツール ウィンドウのインスタンスは 1 つのみです。 単一インスタンスのツール ウィンドウを開いた後は、IDE が閉じられるまで開いたままです。 単一インスタンスのツールウィンドウを閉じると、その可視性だけが変化します。 複数インスタンスのツール ウィンドウを作成して、ウィンドウの複数のインスタンスを同時に開くことも可能です。 詳細について [は、「マルチインスタンスツールウィンドウの作成](../extensibility/creating-a-multi-instance-tool-window.md) 」を参照してください。  
  
 ツールウィンドウは *動的*にすることができます。つまり、関連する UI コンテキストが適用されるたびに表示されます。 自動表示の使用により、IDE でのウィンドウの煩雑さが軽減されます。 詳細については、「 [動的ツールウィンドウを開く](../extensibility/opening-a-dynamic-tool-window.md)」を参照してください。  
  
 ツール ウィンドウは、ドッキング、フローティング、またはドキュメント フレームのタブ付けが可能です。 ツール ウィンドウの枠は IDE によって提供され、サイズ、位置、ドッキング状態と、その他の永続的なプロパティを制御するために使用します。 ツール ウィンドウのペインには、内容が表示されます。 既定のサイズと位置はツール ウィンドウを最初に開くときにのみ適用されます。その後、ツール ウィンドウの状態は保持されます。  
  
 ツール ウィンドウのペインでは、WPF ユーザー コントロールをホストして、ツールバーをサポートすることができます。 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> プロパティをオーバーライドして、ホストされるコントロールのハンドルを返すことができます。  
  
 ツールウィンドウには、さまざまな機能を追加できます。 たとえば、ツールウィンドウに [ツールバーを](../extensibility/adding-a-toolbar-to-a-tool-window.md) 追加したり、ショートカットメニューを追加したりできます。ツール [ウィンドウにショートカットメニュー](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)を追加する方法です。 ツールウィンドウ内の項目の検索を可能にする検索コントロールを追加できます。 [ツールウィンドウに検索機能を追加](../extensibility/adding-search-to-a-tool-window.md)します。  
  
 ツールウィンドウイベント ( [イベントのサブスクライブ](../extensibility/subscribing-to-an-event.md)) にサブスクライブできます。  
  
## <a name="extending-existing-tool-windows"></a>拡張 (既存のツールウィンドウを)  
 新しい **オプション** ページにツールウィンドウに関する情報を追加し、[ **プロパティ** ] ページで新しい設定を追加して、[ **タスク一覧** と **出力** ] ウィンドウに書き込むことができます。 詳細については、「 [プロパティ、タスク一覧、出力、およびオプションウィンドウの拡張](../extensibility/extending-the-properties-task-list-output-and-options-windows.md) 」および「 [プロパティ、タスク一覧、出力、およびオプションの](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)各ウィンドウの拡張」を参照してください。  
  
## <a name="modal-dialog-boxes"></a>モーダルダイアログボックス  
 Visual Studio 拡張機能では、モーダルダイアログボックスをから派生させることによって作成する必要があり <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName> ます。これにより、コントロールと残りの UI を制御できます。 詳細については、「」を参照してください。 [モーダルダイアログボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)。  
  
## <a name="see-also"></a>参照  
 [ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)
