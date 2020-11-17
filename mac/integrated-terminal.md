---
title: Visual Studio for Mac - 統合ターミナル
description: Visual Studio for Mac の統合ターミナルを使用する。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/14/2020
ms.assetid: EFD53CE9-8174-4FE4-8863-2984D22FD921
ms.openlocfilehash: f91c2b1c3f06f8f1fbe54e32fde70b9fe88c5f5d
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94492873"
---
# <a name="integrated-terminal"></a>統合ターミナル
Visual Studio for Mac では、統合ターミナル ウィンドウを開くことができ、最初はご利用のソリューションのルートから開始します。 ターミナルは、フロントエンド タスクの実行 (npm、ng、vue など)、コンテナーの管理、高度な git コマンドの実行、Entity Framework コマンドの実行、dotnet CLI 出力の表示、NuGet パッケージの追加など、さまざまな種類の状況で役に立ちます。 

ターミナルを開くには:
- **Ctrl + `** キーボード ショートカットを使用して、ターミナル ウィンドウの表示と非表示を切り替えます。
- **[表示]** の **[ターミナル]** メニューを使用します。
- 検索バーから **terminal** コマンドを使用します。

![\* 起動直後の Visual Studio for Mac 統合ターミナル *](media/integrated-terminal-intro.png)

既定では、ターミナルが起動されると、次のようになります。
- 作業ディレクトリを現在のソリューションのパスに設定します。
- 既定のシステム シェルを読み込みます。

## <a name="search"></a>検索
ターミナル ウィンドウのコンテンツを検索するには、 **[検索] > [検索...]** メニューを使用します。

![\* Visual Studio for Mac 統合ターミナルでの検索エクスペリエンス *](media/integrated-terminal-search.png)

## <a name="terminal-keyboard-shortcuts"></a>ターミナルのキーボード ショートカット
|コマンド|キーボード ショートカット|
|-|-|
|ターミナル ウィンドウの表示と非表示を切り替えます|**Ctrl+ `**|
|新しいターミナル インスタンスを作成します|**Ctrl + '**|
|ページを上にスクロールします|**PageUp**|
|ページを下にスクロールします|**PageDown**|
|以前に使用したコマンドを順番に実行します|**↑**、**↓**|
|フォント サイズを大きくします|**⌘+**|
|フォント サイズを小さくします|**⌘-**|

## <a name="multiple-instances"></a>複数インスタンス
ターミナルの複数のインスタンスをいつでも実行できます。 **Ctrl+'** キーボード ショートカットを使用して新しいインスタンスを作成できます。 インスタンスを切り替えるには、各インスタンスのタブをクリックするか、**Ctrl + tab** ショートカットを使用してウィンドウ ピッカー ダイアログを使用します。

![\* Visual Studio for Mac 内の複数のターミナル インスタンス *](media/integrated-terminal-multiple-instances.png) 

## <a name="customizing-the-terminal-window"></a>ターミナル ウィンドウのカスタマイズ
### <a name="configuring-the-terminal-font"></a>ターミナル フォントの構成
ターミナル コンテンツに使用されるフォントとサイズは、[基本設定] > [環境] > [フォント] ウィンドウで変更できます。 既定では、フォントは出力ウィンドウのコンテンツと同じで、Menlo Regular、サイズ 11 を使用します。 エディターのフォントに関係なく、任意のフォントに設定できます。

![\* 統合ターミナルのフォント設定のカスタマイズ *](media/integrated-terminal-change-font.png)

### <a name="reusing-system-terminal-customizations"></a>システム ターミナルのカスタマイズの再利用
統合ターミナルでは、macOS システム ターミナルと同じ既定値と構成が使用されます。 つまり、ターミナルのカスタマイズ (zsh、oh-my-zsh など) も統合ターミナルで機能します。
