---
title: ビジュアルスタジオ SDK |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56f772d7d27f11318cdeb0bf365373d5f7c1294b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698075"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK を使用すると、Visual Studio の機能を拡張したり、新しい機能を Visual Studio に統合したりできます。 拡張機能は、他のユーザーに配布することも、Visual Studio マーケットプレースにも配布することもできます。 Visual Studio を拡張する方法の一部を次に示します。

- コマンド、ボタン、メニュー、その他の UI 要素を IDE に追加する

- 新しい機能のためのツール ウィンドウを追加する

- 特定の言語に対して IntelliSense を拡張するか、新しいプログラミング言語に IntelliSense を提供する

- 電球を使用して、開発者が優れたコードを書くのに役立つヒントや提案を提供する

- 新しい言語のサポートを有効にする

- カスタム プロジェクトの種類を追加する

- 何百万人もの開発者に、Visual Studio マーケットプレースを通じてリーチ

  Visual Studio 拡張機能を作成したことがない場合は、これらの機能の詳細と[Visual Studio 拡張機能の開発の開始](../extensibility/starting-to-develop-visual-studio-extensions.md)に関する情報を参照してください。

## <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール
 Visual Studio SDK は、Visual Studio のセットアップのオプション機能です。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="whats-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK の新機能
 Visual Studio SDK には、VSIX v3 形式などのいくつかの新機能と、拡張機能の更新が必要になる変更点があります。 詳細については[、「Visual Studio 2017 SDK の新機能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)」を参照してください。

## <a name="visual-studio-user-experience-guidelines"></a>ビジュアル スタジオ ユーザー エクスペリエンスのガイドライン
 [Visual Studio ユーザー エクスペリエンスのガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)で、拡張機能の UI を設計するためのヒントを紹介します。

 また、[アドレス DPI の問題の](../extensibility/addressing-dpi-issues2.md)記事で、高 DPI デバイスで拡張機能を見やすくする方法を学ぶことができます。

 [イメージ サービスとカタログ](../extensibility/image-service-and-catalog.md)を活用して、高い DPI とテーマの優れたイメージ管理とサポートを実現します。

## <a name="find-and-install-existing-visual-studio-extensions"></a>既存の Visual Studio 拡張機能を検索してインストールする
 Visual Studio 拡張機能は、[**ツール**] メニューの **[拡張機能と更新プログラム**] ダイアログで確認できます。 詳細については、「 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。 拡張機能は[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)で見つけることができます。

## <a name="visual-studio-sdk-reference"></a>ビジュアル スタジオ SDK リファレンス
 ビジュアル スタジオ SDK API リファレンスは、次のトピックを[参照してください](../extensibility/visual-studio-sdk-reference.md)。

## <a name="visual-studio-sdk-samples"></a>ビジュアル スタジオ SDK のサンプル
 VS SDK 拡張機能のオープン ソースの例については、GitHub[で参照してください](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。 この GitHub リポジトリには、Visual Studio のさまざまな拡張可能な機能を示すサンプルが含まれています。

## <a name="other-visual-studio-sdk-resources"></a>その他のビジュアル スタジオ SDK リソース
 VSSDK に関する質問がある場合や、拡張機能の開発経験を共有する場合は[、Visual Studio 拡張機能フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)または[ExtendVS Gitter チャットルーム](https://gitter.im/Microsoft/extendvs)を使用できます。

 [詳細については、VSX Arcana ブログ](https://blogs.msdn.microsoft.com/vsx/)と、Microsoft MVP によって書かれたブログの数を参照してください。

- [お気に入りのビジュアル スタジオ拡張機能](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [ビジュアル スタジオの機能拡張](http://www.visualstudioextensibility.com/overview/vs/)

- [拡張のビジュアル スタジオ](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>関連項目

- [メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)
- [方法: 拡張機能プロジェクトを Visual Studio 2017 に移行する](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [FAQ: アドインから VSPackage 拡張機能への変換](/visualstudio/extensibility/faq-converting-add-ins-to-vspackage-extensions?view=vs-2015)
- [マネージ コードで複数のスレッドを管理する](../extensibility/managing-multiple-threads-in-managed-code.md)
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [ツールバーにコマンドを追加する](../extensibility/adding-commands-to-toolbars.md)
- [ツール ウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)
- [エディターおよび言語サービス拡張](../extensibility/editor-and-language-service-extensions.md)
- [プロジェクトの拡張](../extensibility/extending-projects.md)
- [ユーザー設定とオプションを拡張する](../extensibility/extending-user-settings-and-options.md)
- [カスタム プロジェクトテンプレートと項目テンプレートを作成する](../extensibility/creating-custom-project-and-item-templates.md)
- [プロパティとプロパティ ウィンドウを拡張する](../extensibility/extending-properties-and-the-property-window.md)
- [ビジュアル スタジオの他の部分を拡張します。](../extensibility/extending-other-parts-of-visual-studio.md)
- [サービスの利用と提供](../extensibility/using-and-providing-services.md)
- [VSPackage を管理する](../extensibility/managing-vspackages.md)
- [ビジュアル スタジオの分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [出荷のビジュアル スタジオ拡張機能](../extensibility/shipping-visual-studio-extensions.md)
- [Visual Studio SDK の内部](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [Visual Studio SDK のサポート](../extensibility/support-for-the-visual-studio-sdk.md)
- [ビジュアル スタジオ SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)
