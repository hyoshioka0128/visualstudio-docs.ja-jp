---
title: UWP アプリを更新する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- JavaScript debugging, refreshing pages [UWP apps]
- debugging, refreshing pages [UWP apps]
- DOM Explorer, Refresh [UWP apps]
- Refresh [UWP apps]
ms.assetid: fd99ee60-fa94-46df-8b17-369f60bfd908
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: dd38a758a69b2e19079a2bc2511e7edf5cbfb0ab
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348159"
---
# <a name="refresh-a-uwp-app-in-visual-studio"></a>Visual Studio で UWP アプリを更新する

 デバッグ中にコードを変更し、 **[デバッグ]** ツール バーの **[Windows アプリケーションの更新]** を選択することで、JavaScript を使用する UWP アプリを更新できます。 このボタンを選択すると、デバッガーを停止したり再起動したりせずにアプリが再度読み込まれます。 更新機能によって、HTML、CSS、および JavaScript コードを変更し、その結果をすばやく確認できます。 この機能は UWP アプリに対してサポートされています。

 更新では、アプリの状態は保持されません。また、アプリに対する次の変更は反映されません。

- パッケージ マニフェストに指定されたイメージの変更を含むパッケージ マニフェスト ファイルの変更。

- SDK 参照の追加や削除などの参照の変更、または Windows ランタイム コンポーネント (.winmd ファイル) の変更。

- .resjson ファイル内の文字列の変更などのリソースの変更。

- パス名の変更、新しいプロジェクト ファイル、または削除ファイルが発生するプロジェクト ファイルの変更。

- 選択したデバッグ デバイスの変更などのプロジェクトおよび項目プロパティの変更、またはファイルのパッケージ操作の変更 ([プロパティ] ウィンドウ内)。

> [!IMPORTANT]
> 参照やパッケージ マニフェストの変更など、上記の項目の変更を行った場合、HTML、CSS、および JavaScript のソース ファイルを更新するには、デバッガーを停止して再起動する必要があります。

### <a name="to-refresh-an-app"></a>アプリを更新するには

1. Visual Studio で UWP プロジェクトを開いた状態で、デバッグ ターゲットとして **[ローカル コンピューター]** を選択します。

     ![デバッグ ターゲット選択リスト](../debugger/media/js_select_target.png "JS_Select_Target")

3. F5 キーを押して、アプリをデバッグ モードで実行します。

4. Visual Studio に切り替えます

5. UWP アプリのホーム ページで、いくつかの HTML を編集します。

7. 次のような **[Windows アプリの更新]** ボタンをクリックします: ![[Windows アプリの更新] ボタン](../debugger/media/js_refresh.png "JS_Refresh") (または F4 キーを押します)。

8. アプリに切り替えます。 アプリが再読み込みされ、更新された HTML を使用してアプリがレンダリングされます。

## <a name="see-also"></a>関連項目
- [クイック スタート:HTML および CSS のデバッグ](../debugger/quickstart-debug-html-and-css.md)