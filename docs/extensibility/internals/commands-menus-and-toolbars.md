---
title: コマンド、メニュー、ツールバー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2be2f719d0f123328d5c518c08e30df2185e2a19
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709501"
---
# <a name="commands-menus-and-toolbars"></a>コマンド、メニュー、およびツールバー
メニューとツール バーは、ユーザーが VSPackage のコマンドにアクセスする方法です。 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。 メニューとツール バーは、ユーザーにコマンドをグラフィカルに表示する便利な方法です。 通常、関連するコマンドは、同じメニューやツール バーにまとめられます。

- メニューは通常、統合開発環境 (IDE) やツール ウィンドウの上部にある列にまとめられた 1 語の文字列として表示されます。 メニューは、右クリック イベントの結果として表示することもでき、これはそのコンテキストのショートカット メニューと呼ばれます。 クリックすると、メニューが展開して 1 つ以上のコマンドが表示されます。 コマンドをクリックすると、タスクを実行したり、追加のコマンドを含むサブメニューを起動したりすることができます。 よく知られているメニュー名には、**ファイル**、**編集**、**表示**、および**ウィンドウ**があります。 詳細については、[メニューとコマンドの拡張を](../../extensibility/extending-menus-and-commands.md)参照してください。

- ツール バーは通常、ボタンと他のコントロール (コンボ ボックス、リスト ボックス、テキスト ボックス、メニュー コント ローラーなど) の行です。 すべてのツール バー コントロールは、コマンドに関連付けられます。 ツール バー ボタンをクリックすると、関連付けられているコマンドがアクティブ化されます。 ツール バー ボタンには、通常、[印刷] コマンド用のプリンターなどの基になるコマンドを示すアイコンがあります。 ドロップダウン リスト コントロールでは、リスト内の各項目は、異なるコマンドに関連付けられています。 メニュー コントローラーは、コントロールの一方の側がツール バー ボタン、もう一方の側が、クリックして追加のコマンドを表示する下矢印の組み合わせです。 詳細については、「[メニュー コントローラーをツールバーに追加する](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)」を参照してください。

- コマンドを作成するときは、コマンド用のイベント ハンドラーも作成する必要があります。 イベント ハンドラーでは、コマンドをいつ表示または有効にするかを決定し、コマンドのテキストを変更し、アクティブ化したときにコマンドが適切に応答する (「ルーティングする」) ようにすることができます。 ほとんどの場合、IDE では <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではコマンドは階層形式でルーティングし、ローカルの選択に基づいて最も内側のコマンド コンテキストから開始し、グローバルの選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。 詳細については、「[メニュー コマンドと OleMenuCommands と](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)[選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)」を参照してください。

  新しいメニューとツール バーを定義するには、Visual Studio コマンド テーブル (*.vsct*) ファイルで説明する必要があります。 Visual Studio パッケージ テンプレートは、テンプレートで選択したコマンド、ツール バー、およびエディターをサポートするために必要な要素と共に、このファイルを自動的に作成します。 または、ここで説明する XML スキーマを使用して、独自の *.vsct* [VSCT XML schema reference](../../extensibility/vsct-xml-schema-reference.md)ファイルを作成することもできます。

  *vsct*ファイルの操作の詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

  このセクションのトピックでは、VSPackages でのコマンド、メニュー、およびツール バーの動作について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンド・テーブルのフォーマット指定の詳細な説明。

- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 コマンド テーブルの XML ベースの構文とコンパイラについて説明します。

- [既定のコマンド、グループ、およびツールバーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 定義済みのコマンド、グループ、メニュー、およびツール バーについて説明します。

- [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 IDE で使用できる定義済みのメニュー、コマンド、およびコマンドグループを指定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

- [コマンド設計](../../extensibility/internals/command-design.md)

 コマンドのデザイン方法について説明します。

- [メニューコマンドとツールバーコマンドを最適化する](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 コマンドのガイドラインを示します。

- [コマンドを使用可能にする](../../extensibility/internals/making-commands-available.md)

 コマンドを Visual Studio で使用できるようにする方法について説明します。

- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 相互運用機能アセンブリを使用するコマンドを実装する方法について説明します。

## <a name="related-sections"></a>関連項目
- [VS パッケージでのコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)

 VSPackages でのコマンド ルーティングについて説明します。
