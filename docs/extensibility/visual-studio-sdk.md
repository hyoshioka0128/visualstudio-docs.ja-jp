---
title: Visual Studio SDK |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5949a651c99c0ce45f963b5f2042cdfe6cb40b87
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848573"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK は Visual Studio の機能を拡張することや、Visual Studio に新しい機能を追加するのに役立ちます。 Visual Studio Marketplace では、あなたが作成した拡張機能を他のユーザーへ配布することができます。 Visual Studio を拡張する方法の一部を次に示します。

- IDE にコマンド、ボタン、メニューおよびその他の UI 要素を追加

- ツール ウィンドウに新しい機能を追加する

- 指定された言語の IntelliSense を拡張するか、新しいプログラミング言語に IntelliSense を提供します

- 電球を使用して、優れたコードを記述のヒントと開発者に役立つ提案を提供

- 新しい言語のサポートを有効にする

- カスタム プロジェクトの種類を追加する

- Visual Studio Marketplace で何百万もの開発者に公開する

  以前に Visual Studio 拡張機能を書いたことが無い場合、これらの機能についての詳細については"[Visual Studio 拡張機能の開発を始める](../extensibility/starting-to-develop-visual-studio-extensions.md)"を参照してください。

## <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール
 Visual Studio SDK は、Visual Studio セットアップのオプション機能です。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="whats-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK の新機能について
 Visual Studio SDK は一部の新機能などで VSIX v3 形式だけでなく互換性の無い変更などがあり、拡張機能を更新する必要がある場合があります 詳細については、[Visual Studio 2017 SDKの新機能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)を参照してください。

## <a name="visual-studio-user-experience-guidelines"></a>Visual Studio ユーザーエクスペリエンスガイドライン
 [Visual Studio ユーザー エクスペリエンス ガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)で拡張機能の UI を設計するための便利なヒントを取得します。

 [DPIの問題の対処方法](../extensibility/addressing-dpi-issues2.md)で高 DPI デバイスに美しく表示拡張機能を作成する方法を確認できます。

 [イメージ サービスとカタログ](../extensibility/image-service-and-catalog.md)を活用して優れた画像の管理や、高DPIとテーマのサポートをします。

## <a name="find-and-install-existing-visual-studio-extensions"></a>既存の Visual Studio 拡張機能の検索とインストール
 **ツール**メニューの**拡張機能と更新**ダイアログでVisual Studio 拡張機能を見つけることができます。 詳細については、"[検索と使用の Visual Studio Extensions](../ide/finding-and-using-visual-studio-extensions.md)"を参照してください。 また、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)で拡張機能を検索することもできます。

## <a name="visual-studio-sdk-reference"></a>Visual Studio SDK リファレンス
 [Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)でVisual Studio SDK の API リファレンスを検索できます。

## <a name="visual-studio-sdk-samples"></a>Visual Studio SDK のサンプル
 GitHub の[Visual Studio のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)で VS SDK 拡張機能のオープン ソースの例を検索できます。 この GitHub リポジトリには、Visual Studio のさまざまな拡張機能を示すサンプルが含まれています。

## <a name="other-visual-studio-sdk-resources"></a>その他の Visual Studio SDK リソース
 VSSDK について質問があるか、拡張機能の開発経験を共有する場合、 [Visual Studio 機能拡張フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)または[ExtendVS Gitter チャット ルーム](https://gitter.im/Microsoft/extendvs)を利用できます。

 [Visual Studio ブログ](https://blogs.msdn.microsoft.com/vsx/)と Microsoft MVP によって書かれたブログで詳細を確認することができます。

- [お気に入りの Visual Studio 拡張機能](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [Visual Studio の機能拡張](http://www.visualstudioextensibility.com/overview/vs/)

- [拡張 (Visual Studio を)](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>関連項目

- [メニューコマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)
- [方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [FAQ: アドインを VSPackage 拡張機能に変換する](/visualstudio/extensibility/faq-converting-add-ins-to-vspackage-extensions?view=vs-2015)
- [マネージコード内の複数のスレッドを管理する](../extensibility/managing-multiple-threads-in-managed-code.md)
- [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)
- [ツールバーにコマンドを追加する](../extensibility/adding-commands-to-toolbars.md)
- [ツールウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)
- [エディターと言語サービスの拡張機能](../extensibility/editor-and-language-service-extensions.md)
- [プロジェクトの拡張](../extensibility/extending-projects.md)
- [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)
- [カスタムプロジェクトと項目テンプレートの作成](../extensibility/creating-custom-project-and-item-templates.md)
- [プロパティとプロパティウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)
- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
- [Vspackage の管理](../extensibility/managing-vspackages.md)
- [Visual Studio 分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [Visual Studio 拡張機能を出荷する](../extensibility/shipping-visual-studio-extensions.md)
- [Visual Studio SDK の内部](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [Visual Studio SDK のサポート](../extensibility/support-for-the-visual-studio-sdk.md)
- [Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)
