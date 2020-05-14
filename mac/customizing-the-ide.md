---
title: IDE のカスタマイズ
description: Visual Studio for Mac はさまざまな方法でカスタマイズできます。効率性とデザイン性の両方のニーズを満たす環境でアプリを開発できます。 この記事では、Visual Studio for Mac を自分のニーズに合わせてカスタマイズするためのさまざまな方法を紹介します。
author: alanjclark
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: F7C2A28C-0759-4E0D-A28E-B72D5AB73DB6
ms.custom: video
ms.openlocfilehash: d35cd7ebc5534cd49f18db794b5fdeb5f62f4758
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "79306681"
---
# <a name="customizing-the-ide"></a>IDE のカスタマイズ

Visual Studio for Mac は、ユーザーが効率性とデザイン性の両方のニーズを満たす環境でアプリを開発できるようにカスタマイズすることができます。 この記事では、Visual Studio for Mac を自分のニーズに合わせてカスタマイズするためのさまざまな方法を紹介します。

## <a name="dark-theme"></a>ダーク テーマ

![ダーク テーマ ビュー](media/customizing-the-ide-image7a.png)

Visual Studio for Mac ではテーマを切り替えることができます。次の図のように、 **[Visual Studio]、[ユーザー設定]、[環境]、[視覚スタイル]** の順に選択し、 **[ユーザー インターフェイス テーマ]** ドロップダウンから希望のテーマを選択します。

![ダーク テーマの選択](media/customizing-the-ide-image7b.png)

## <a name="localization"></a>ローカリゼーション

Visual Studio for Mac は次の 14 か国語にローカライズされており、よりたくさんの開発者にご利用いただけます。

* 中国語 - 中国
* 中国語 - 台湾
* Czech
* French
* German
* English
* Italian
* Japanese
* Korean
* Polish
* ポルトガル語 - ブラジル
* Russian
* Spanish
* Turkish

Visual Studio for Mac の表示言語を変更するには、次の図のように、 **[Visual Studio]、[ユーザー設定]、[環境]、[視覚スタイル]** の順に選択し、 **[ユーザー インターフェイス言語]** ドロップダウンから希望の言語を選択します。

![言語の選択](media/customizing-the-ide-image11a.png)

## <a name="author-information"></a>作成者情報

作成者情報パネルでは、名前、メール アドレス、作品の著作権所有者、会社、商標など、自分に関する関連情報を追加できます。

![作成者情報の編集セクション](media/customizing-the-ide-image9a.png)

この情報は、新しいファイルに追加する可能性がある、ライセンスなど、標準ファイル ヘッダーに入力するために使用されます。

![標準ヘッダー オプション](media/customizing-the-ide-image8a.png)

Visual Studio for Mac のバージョン管理からコミットが行われた場合、そのコミットで、 **[名前]** フィールドと **[電子メール]** フィールドに入力されたデータが利用されます。 このフィールドにデータを入力していない場合、バージョン管理を利用するときに、Visual Studio for Mac から入力が求められます。

## <a name="key-bindings"></a>キー バインド

キー バインドまたはキーボード ショートカットを利用することで、より効率的に Visual Studio for Mac を操作できるように開発環境を調整できます。 Visual Studio (Windows)、ReSharper、Visual Studio Code、Xcode など、人気のある多くの IDE 用に使い慣れたキー バインドが提供されています。

次の図のように、 **[Visual Studio]、[ユーザー設定]、[環境]、[キー バインド]** の順に選択し、キー バインドを設定できます。

![キー バインドの設定](media/customizing-the-ide-image10a.png)

ここからキー バインドの組み合わせを検索したり、競合するバインドを表示したり、新しいバインドを追加したり、既存のバインドを編集したりできます。

これらのバインドは、Visual Studio for Mac の初回セットアップ中に、 **[キーボードの選択]** 画面を使用して設定することもできます。

![キーバインドの設定、最初の実行](media/ide-tour-2019-keyboard-shortcut.png)

## <a name="workspace-layout"></a>ワークスペースのレイアウト

Visual Studio for Mac のワークスペースは、メインのドキュメント領域 (通常、エディター、デザイナー サーフェス、またはオプション ファイル) で構成されています。この補完的な領域は*パッド*で囲まれています。このパッドには、アプリケーション ファイルにアクセスし、管理、テスト、およびデバッグを行う際に役立つ情報が含まれています。

 ![ワークスペースのレイアウト](media/customizing-the-ide-image1a.png)

### <a name="viewing-and-arranging-pads"></a>パッドの表示と整理

Visual Studio for Mac で新しいソリューションまたはファイルを開くとき、ワークスペースに*パッド*が表示されます。これには、Solution Pad、ドキュメント アウトライン、エラーが含まれます。

![Solution Pad](media/customizing-the-ide-image2a.png)

Visual Studio for Mac のパッドには追加情報、ツール、ナビゲーション補助が含まれています。これには、 **[表示]、[パッド]** メニュー項目の順に選択し、それを追加するパッドを選択するとアクセスできるようになります。

![新しいパッドを選択する](media/customizing-the-ide-image3a.png)

パッドはさまざまなコマンドで自動的に開くこともできます。たとえば、 **[複数のファイル内を検索]** (Shift + Command + F) コマンドを実行すると、別のパッドが開き、検索結果が表示されます。

パッドは、自分にとって最も便利になるようにワークフロー内の任意の場所に移動したり、配置したりできます。 たとえば、ドキュメント エディターのあらゆる側面にパッドを配置できます。別のパッドの隣に、上に、または下に配置することで、あるいはタブ付きパッドのセットとして配置することですばやく切り替えることができます。

頻繁に使用されるパッドについては、Visual Studio for Mac からパッドを完全に切り離し、そのパッドのためのウィンドウを別に作成することもできます。

各パッドの右上隅にあるトグルをクリックすると、パッドを非表示にしたり、閉じたりできます。

![パッドを非表示にする/閉じる](media/customizing-the-ide-image5a.png)

自動非表示のパッドはワークスペースの側面にドッキングされます。必要なとき、簡単に表示されます。 パッドの上にカーソルを合わせると再び表示されます。マウスやキーボードの焦点を外すと、非表示になります。

### <a name="organizing-layouts"></a>レイアウトの整理

常に表示されるパッドは、現在のコンテキストによって決まります。 たとえば、ビジュアル デザイナーを使用するときは、ツールボックス パッドとプロパティ パッドが最も重要になります。デバッグのときには、スタックやローカルを表示するためにデバッガー パッドを用意すると便利です。

開いているパッドの状態を表現したものが*レイアウト*です。 次の図のように、レイアウトは [表示] メニューから手動で切り替えることができます。あるいは、デバッグしたり、ストーリーボードを開いたり、特定のアクションを実行すると自動的に切り替わります。

![新しいレイアウトの選択](media/customizing-the-ide-image6b.png)

1 つのレイアウトが常に有効になります。レイアウト内を変更すると、たとえば、パッドを追加したり、パッドの位置を変更したりすると、そのとき有効なレイアウトだけが変更されます。 Visual Studio for Mac を閉じると、変更は保存されません。

ただし、新しいレイアウトを作成することができます。 **[表示]、[Save Current Layout]\(現在のレイアウトを保存\)** メニュー項目を使用します。 このコマンドを実行すると、現在のレイアウトがメニューに追加され、いつでも選択できるようになります。

![現在のレイアウトを保存する](media/customizing-the-ide-image6a.png)

### <a name="side-by-side-editing-support"></a>サイド バイ サイド編集

Visual Studio for Mac では、テキスト エディターを並べて開いたり、エディターを別のウィンドウとして表示したりできます。

2 列モードは、 **[表示] > [エディター列] > [2 columns]\(2 列\)** を選択するか、[エディター] タブをエディター領域のいずれかの端にドラッグすることで、[表示] メニュー項目を介して有効にすることができます。

![2 列のサイド バイ サイド モード](media/customizing-the-ide-sbs.png)

エディター タブはドキュメント領域の外にドラッグできます。エディター ウィンドウが別ウィンドウとして表示されます。 この別ウィンドウもサイド バイ サイド エディターに対応し、複数のエディター タブを含めることができます。

![新しいウィンドウを作成する](media/customizing-the-ide-sbs1.png)

![2 列サイド バイ サイドと追加タブ](media/customizing-the-ide-sbs2.png)

1 つのエディターを開いている状態に戻すには、 **[表示]、[エディター列]、[1 列]** の順に選択します。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Customize-the-Look-and-Feel/player]

## <a name="see-also"></a>参照

- [Visual Studio IDE のカスタマイズ (Windows)](/visualstudio/ide/personalizing-the-visual-studio-ide)