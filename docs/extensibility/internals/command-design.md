---
title: コマンド設計 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6aa58813623dc8150cafb4fbfee6496d09f889ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709654"
---
# <a name="command-design"></a>コマンド設計
VSPackage にコマンドを追加する場合は、表示する場所、いつ使用できるか、および処理方法を指定する必要があります。

## <a name="define-commands"></a>コマンドの定義
 新しいコマンドを定義するには、VSPackage プロジェクトに Visual Studio コマンド テーブル (*.vsct*) ファイルを含めます。 Visual Studio パッケージ テンプレートを使用して VSPackage を作成した場合、プロジェクトにはこれらのファイルのいずれかが含まれます。 詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

 Visual Studio では、すべての *.vsct*ファイルがマージされ、コマンドを表示できます。 これらのファイルは VSPackage バイナリとは異なるため、Visual Studio はコマンドを見つけるためにパッケージを読み込む必要はありません。 詳細については、「 [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

 Visual Studio<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>では、登録属性を使用してメニュー リソースとコマンドを定義します。 詳細については、[コマンドの実装](../../extensibility/internals/command-implementation.md)を参照してください。

 コマンドは、さまざまな方法で実行時に変更できます。 表示または非表示、有効または無効にすることができます。 異なるテキストやアイコンを表示したり、異なる値を含めたりすることができます。 多くのカスタマイズは、Visual Studio が VSPackage を読み込む前に実行される可能性があります。 詳細については、「 [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

## <a name="command-handlers"></a>コマンド ハンドラー
 コマンドを作成する場合は、コマンドを実行するためのイベント ハンドラーを指定する必要があります。 ユーザーがコマンドを選択した場合は、適切にルーティングする必要があります。 コマンドのルーティングとは、コマンドを適切な VSPackage に送信して、それを有効または無効にし、表示または非表示にし、ユーザーが選択した場合にそれを実行することを意味します。 詳細については、コマンド[ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)を参照してください。

## <a name="visual-studio-command-environment"></a>ビジュアル スタジオ のコマンド環境
 Visual Studio は、任意の数の VSPackage をホストでき、それぞれが独自のコマンド セットを提供できます。 環境には、現在のタスクに適したコマンドのみが表示されます。 詳細については、「[コマンドの使用可能性](../../extensibility/internals/command-availability.md)」および[「選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)」を参照してください。

 新しいコマンド、メニュー、ツール バー、またはショートカット メニューを定義する VSPackage は、ネイティブ または マネージ アセンブリのリソースを参照するレジストリ エントリを使用して、インストール時に Visual Studio にそのコマンド情報を提供します。 各リソースは、Visual Studio コマンド テーブル (*.vsct*) ファイルをコンパイルするときに生成されるバイナリ データ リソース (*.cto*) ファイルを参照します。 これにより、Visual Studio は、インストールされているすべての VSPackage を読み込む必要なしにマージされたコマンド セット、メニュー、およびツール バーを提供できます。

### <a name="command-organization"></a>指揮組織
 環境は、グループ、優先順位、およびメニューごとにコマンドを配置します。

- グループは、関連するコマンドの論理的な集合です。 **Cut** **Copy** **Paste** グループは、メニューに表示されるコマンドです。

- 優先度は、グループ内の個々のコマンドがメニューに表示される順序を決定します。

- メニューは、グループのコンテナとして機能します。

  環境では、いくつかのコマンド、グループ、およびメニューが事前に定義されます。 詳細については、「[デフォルトのコマンド、グループ、およびツールバーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)」を参照してください。

  コマンドは、1 次グループに割り当てることができます。 メイン グループは、メイン メニュー構造と **[ユーザー設定**] ダイアログ ボックスでのコマンドの位置を制御します。 コマンドは複数のグループに表示できます。たとえば、コマンドはメイン メニュー、ショートカット メニュー、およびツールバーに表示されます。 詳細については、「 [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

### <a name="command-routing"></a>コマンド ルーティング
 VSPackage のコマンドを呼び出し、ルーティングするプロセスは、オブジェクト インスタンスのメソッドを呼び出すプロセスとは異なります。

 環境は、現在の選択に基づく最も内側の (ローカル) コマンド コンテキストから最も外側の (グローバル) コンテキストにコマンドを順次ルーティングします。 コマンドを実行できる最初のコンテキストは、そのコマンドを処理するコンテキストです。 詳細については、コマンド[ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)を参照してください。

 ほとんどの場合、環境はインターフェイスを使用してコマンドを処理<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>します。 コマンド ルーティング 方式では、多くの異なるオブジェクトが<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コマンドを処理できるため、任意の数のオブジェクトで実装できます。これらのオブジェクトには、Microsoft ActiveX コントロール、ウィンドウ ビューの実装、ドキュメント オブジェクト、プロジェクト階層、VSPackage オブジェクト (グローバル コマンドの場合) などがあります。 階層内のルーティング コマンドなど、特殊な場合には、インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>実装する必要があります。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[コマンドの実装](../../extensibility/internals/command-implementation.md)|VSPackage でコマンドを実装する方法について説明します。|
|[コマンドの可用性](../../extensibility/internals/command-availability.md)|Visual Studio のコンテキストによって、使用できるコマンドが決定されるしくみについて説明します。|
|[コマンドルーティングアルゴリズム](../../extensibility/internals/command-routing-algorithm.md)|Visual Studio のコマンド ルーティング アーキテクチャによって、異なる VSPackages によってコマンドを処理する方法について説明します。|
|[コマンド配置のガイドライン](../../extensibility/internals/command-placement-guidelines.md)|Visual Studio 環境でコマンドを配置する方法を説明します。|
|[VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|VSPackage が Visual Studio のコマンド アーキテクチャを最大限に活用する方法について説明します。|
|[既定のコマンド、グループ、およびツールバーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|VSPackage が Visual Studio に含まれているコマンドを最もよく使用する方法について説明します。|
|[VSPackage を管理する](../../extensibility/managing-vspackages.md)|VS パッケージを読み込む方法について説明します。|
|[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|VSPackages のコマンドのレイアウトと外観を記述するために使用される、XML ベースの *.vsct*ファイルについて説明します。|
