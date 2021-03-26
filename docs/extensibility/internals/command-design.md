---
title: コマンドのデザイン |Microsoft Docs
description: Visual Studio で VSPackage 用のコマンドをデザインする方法について説明します。 を含む、表示される場所を指定する方法、使用できる場合、および処理する方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0acef6dd38238ef58f1dd66f7d8de35318e4ffc6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078930"
---
# <a name="command-design"></a>コマンドのデザイン
コマンドを VSPackage に追加するときは、表示される場所、使用可能な場合、およびその処理方法を指定する必要があります。

## <a name="define-commands"></a>コマンドの定義
 新しいコマンドを定義するには、VSPackage プロジェクトに Visual Studio コマンドテーブル (*vsct*) ファイルを含めます。 Visual Studio パッケージテンプレートを使用して VSPackage を作成した場合、プロジェクトにはこれらのファイルのいずれかが含まれます。 詳細については、「 [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

 Visual Studio は、見つかったすべての *vsct* ファイルをマージして、コマンドを表示できるようにします。 これらのファイルは VSPackage バイナリとは異なるため、Visual Studio では、コマンドを検索するためにパッケージを読み込む必要はありません。 詳細については、「 [How vspackage add user interface elements](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

 Visual Studio では、 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 登録属性を使用して、メニューリソースとコマンドを定義します。 詳細については、「 [コマンドの実装](../../extensibility/internals/command-implementation.md)」を参照してください。

 コマンドは、実行時にさまざまな方法で変更できます。 表示または非表示にしたり、有効または無効にしたりすることができます。 異なるテキストやアイコンを表示したり、異なる値を含めたりすることができます。 Visual Studio によって VSPackage が読み込まれる前に、多くのカスタマイズが実行される場合があります。 詳細については、「 [How vspackage add user interface elements](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

## <a name="command-handlers"></a>コマンドハンドラー
 コマンドを作成する場合は、コマンドを実行するためのイベントハンドラーを指定する必要があります。 ユーザーがコマンドを選択した場合は、適切にルーティングされている必要があります。 コマンドをルーティングするということは、正しい VSPackage に送信して有効または無効にしたり、非表示にしたり、ユーザーが選択したときに実行したりすることを意味します。 詳細については、「 [コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)」を参照してください。

## <a name="visual-studio-command-environment"></a>Visual Studio コマンド環境
 Visual Studio は任意の数の Vspackage をホストでき、それぞれが独自のコマンドセットを提供できます。 環境には、現在のタスクに適したコマンドのみが表示されます。 詳細については、「 [コマンドの可用性](../../extensibility/internals/command-availability.md) 」および「 [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)」を参照してください。

 新しいコマンド、メニュー、ツールバー、またはショートカットメニューを定義する VSPackage は、インストール時に、ネイティブアセンブリまたはマネージアセンブリ内のリソースを参照するレジストリエントリを通じて、そのコマンド情報を Visual Studio に提供します。 次に、各リソースはバイナリデータリソース (*cto*) ファイルを参照します。これは、Visual Studio のコマンドテーブル (*vsct*) ファイルをコンパイルするときに生成されます。 これにより、インストールされているすべての VSPackage を読み込まなくても、マージされたコマンドセット、メニュー、ツールバーを Visual Studio で提供できるようになります。

### <a name="command-organization"></a>コマンドの編成
 環境では、コマンドがグループ、優先度、およびメニューによって配置されます。

- グループは、 **切り取り**、 **コピー**、 **貼り付け** の各コマンドグループなど、関連するコマンドの論理コレクションです。 グループは、メニューに表示されるコマンドです。

- 優先順位は、グループ内の個々のコマンドがメニューに表示される順序を決定します。

- メニューは、グループのコンテナーとして機能します。

  環境によって、一部のコマンド、グループ、およびメニューが事前されます。 詳細については、「 [既定のコマンド、グループ、およびツールバーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)」を参照してください。

  コマンドは、プライマリグループに割り当てることができます。 プライマリグループは、メインメニュー構造と [ **カスタマイズ** ] ダイアログボックスでコマンドの位置を制御します。 コマンドは複数のグループに表示できます。たとえば、コマンドはメインメニュー、ショートカットメニュー、およびツールバー上に配置できます。 詳細については、「 [How vspackage add user interface elements](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

### <a name="command-routing"></a>コマンド ルーティング
 Vspackage のコマンドの呼び出しとルーティングコマンドの処理は、オブジェクトインスタンスでメソッドを呼び出すプロセスとは異なります。

 環境では、最も内側の (ローカル) コマンドコンテキストから、現在の選択に基づいて、最も外側の (グローバルな) コンテキストにコマンドを順次ルーティングします。 コマンドを実行できる最初のコンテキストは、コマンドを処理するコンテキストです。 詳細については、「 [コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)」を参照してください。

 ほとんどの場合、環境はインターフェイスを使用してコマンドを処理し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 コマンドルーティングスキームでは、コマンドを処理するために多くの異なるオブジェクトが使用できるため、は <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 任意の数のオブジェクトによって実装できます。これには、Microsoft ActiveX コントロール、ウィンドウビューの実装、ドキュメントオブジェクト、プロジェクト階層、および VSPackage オブジェクト (グローバルコマンドの場合) が含まれます。 階層内のコマンドのルーティングなど、特殊なケースでは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスを実装する必要があります。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[コマンドの実装](../../extensibility/internals/command-implementation.md)|VSPackage でコマンドを実装する方法について説明します。|
|[コマンドの可用性](../../extensibility/internals/command-availability.md)|使用可能なコマンドを Visual Studio のコンテキストで判断する方法について説明します。|
|[コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)|Visual Studio のコマンドルーティングアーキテクチャによって、さまざまな Vspackage でコマンドを処理できるようにする方法について説明します。|
|[コマンド配置のガイドライン](../../extensibility/internals/command-placement-guidelines.md)|Visual Studio 環境でコマンドを配置する方法について説明します。|
|[Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|Vspackage が Visual Studio コマンドアーキテクチャを最大限に活用する方法について説明します。|
|[既定のコマンド、グループ、およびツールバーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|Vspackage が Visual Studio に含まれているコマンドを最適に使用する方法について説明します。|
|[VSPackage を管理する](../../extensibility/managing-vspackages.md)|Visual Studio が Vspackage を読み込む方法について説明します。|
|[Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|Vspackage のコマンドのレイアウトと外観を記述するために使用される XML ベースの *vsct* ファイルに関する情報を提供します。|
