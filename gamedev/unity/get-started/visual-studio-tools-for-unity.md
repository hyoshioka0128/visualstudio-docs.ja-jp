---
title: Visual Studio Tools for Unity | Microsoft Docs
description: Visual Studio Tools for Unity の概要について確認します。これは、無料の Visual Studio 拡張機能であり、Unity でのクロスプラットフォームのゲームとアプリの開発に役立ちます。
ms.custom: ''
ms.date: 10/25/2019
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: overview
ms.assetid: 6cabc626-5310-4622-a743-210a9abb5535
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: ee4e9e0dc9df4eb5decb3fc9c2afb0411e9cb75c
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93405390"
---
# <a name="visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity
![Visual Studio Tools for Unity](../media/hero.png)

## <a name="overview"></a>概要
Visual Studio Tools for Unity は、無料の Visual Studio 拡張機能であり、Visual Studio を Unity でクロスプラットフォームのゲームとアプリを開発するための強力なツールにします。

Unity エディターは、ゲームの世界をまとめ上げるのに適していますが、それ自体の中でコードを記述することはできません。 Visual Studio Tools for Unity を使用すると、Visual Studio の使い慣れたコードの編集、デバッグ、生産性の機能を使用して、C# で Unity プロジェクト用のエディターおよびゲーム スクリプトを作成できます。その後、Visual Studio の強力なデバッグ機能によってデバッグできます。

しかし、Visual Studio Tools for Unity が行えるのはそれだけではありません。Unity エディターと緊密に統合されているため、簡単なタスクを行うために両者を行ったり来たりする時間が短縮されます。また、Unity 特有の生産性拡張機能を利用でき、Unity ドキュメントを簡単に利用できます。

### <a name="compatible-with-visual-studio-community-on-windows-and-macos-and-bundled-with-unity"></a>Windows と macOS 上の Visual Studio Community との互換性と Unity とのバンドル
Visual Studio と Visual Studio for Mac Community は無料で利用でき、Unity のインストールにバンドルされています。 インストールとセットアップについて詳しくは、Visual Studio Tools for Unity の[使用開始に関するドキュメント](getting-started-with-visual-studio-tools-for-unity.md)にアクセスしてください。

## <a name="intellisense-for-unity-messages"></a>Unity メッセージ用の IntelliSense
IntelliSense コードの補完を使うと、`OnCollisionEnter` などの [Unity API メッセージとそのパラメーターの実装](using-visual-studio-tools-for-unity.md#intellisense-for-unity-api-messages)が速く簡単になります。

![OnCollisionEnter を表示している IntelliSense ダイアログ](../media/vs/intellisense-example.png)

## <a name="superior-debugging"></a>優れたデバッグ機能
Visual Studio Tools for Unity は、Visual Studio に期待される堅牢な[デバッグ](using-visual-studio-tools-for-unity.md#unity-debugging)機能をサポートしています。

* ブレークポイント (条件付きブレークポイントを含む) の設定。
* [ウォッチ] ウィンドウでの複雑な式の評価。
* 変数および引数の値の検査と変更。
* 複雑なオブジェクトやデータ構造体へのドリルダウン。

![変数を検査するブレークポイントで停止](../media/vs/debugging-inspecting.png)

## <a name="integrated-suggestions-for-best-practices-and-performance-insights"></a>ベスト プラクティスとパフォーマンスの分析情報に関する統合された提案
Visual Studio による Unity プロジェクトの深い理解を利用して、ベスト プラクティスをとらえたより良いコードを記述します。

![VS リファクタリングによる CompareTag を使った文字列比較](../media/vs/unity-diagnostics.png)

## <a name="codelens-support-for-unity-scripts-and-messages"></a>CodeLens による Unity スクリプトとメッセージのサポート
Unity によって提供される内容とコードの内容を簡単に認識できるように、Unity スクリプトとメッセージ関数はヒントで修飾されています。

 ![Unity スクリプトと Unity メッセージに関する CodeLens のヒントを示す新しいスクリプト](../media/vs/codelens-support.png)

> [!NOTE]
> CodeLens サポートは Visual Studio 2019 で使用できます。

## <a name="optimized-view-of-all-your-scripts-to-match-unity"></a>Unity に一致するすべてのスクリプトの最適化表示
Unity Project Explorer (UPE) は、標準のソリューション エクスプローラーでプロジェクト ファイルを表示する別の方法です。 UPE により、表示されるファイルがフィルター処理され、Unity に一致する階層で表示されます (Visual Studio 2019 の **[表示] > [Unity Project Explorer]** )。

![Unity プロジェクト エクスプローラー](../media/vs/unity-project-explorer.png)

> [!NOTE]
> Unity Project Explorer は、Visual Studio 2019 で使用できます。 Visual Studio for Mac では、Solution Pad の Unity プロジェクトに対する既定の動作は同様になります。追加のビューは必要ありません。

* [Visual Studio Tools for Unity の使用を開始する](getting-started-with-visual-studio-tools-for-unity.md)
