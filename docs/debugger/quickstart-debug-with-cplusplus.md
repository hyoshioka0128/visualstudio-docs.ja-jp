---
title: C++ をデバッグする
description: Visual Studio デバッガーを使用してネイティブ コードをデバッグする
ms.custom: mvc
ms.date: 08/06/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: 639e430b-6d2d-46bd-b738-8c60dfb384f1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: b619b2b6c93da8be399b2fc35d81ffe226f408ad
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "65679411"
---
# <a name="quickstart-debug-with-c-using-the-visual-studio-debugger"></a>クイック スタート: Visual Studio デバッガーを使用して C++ でデバッグする

Visual Studio デバッガーでは、アプリのデバッグに役立つ多くの強力な機能が提供されます。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

1. Visual Studio を開き、プロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**c++** 」と入力し、 **[テンプレート]** 、 **[新しいコンソール アプリ プロジェクトの作成]** の順に選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** の左側のウィンドウで、 **[Visual C++]** の下にある **[Windows デスクトップ]** を選択し、真ん中のウィンドウで **[Windows コンソール アプリケーション]** を選択します。 次に、「**MyDbgApp**」のような名前を入力し、 **[OK]** をクリックします。
    ::: moniker-end

    **[Windows コンソール アプリケーション]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 Visual Studio インストーラーが起動します。 **[C++ によるデスクトップ開発]** ワークロード、 **[変更]** の順に選択します。

    Visual Studio によってプロジェクトが作成されます。

1. MyDbgApp.cpp で次のコードを

    ```c++
    int main()
    {
        return 0;
    }
    ```

    このコードで置換します (`#include "stdafx.h"` は削除しないでください)。

    ```c++
    #include <list>
    #include <iostream>

    using namespace std;

    void doWork()
    {
        list <int> c1;

        c1.push_back(10);
        c1.push_back(20);

        const list <int> c2 = c1;
        const int &i = c2.front();
        const int &j = c2.front();
        cout << "The first element is " << i << endl;
        cout << "The second element is " << j << endl;

    }

    int main()
    {
        doWork();
    }
    ```

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

*ブレークポイント*は、Visual Studio で実行コードが中断される場所を示すマーカーです。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 これが、デバッグの最も基本的な機能です。

1. ブレークポイントを設定するには、`doWork` 関数呼び出しの左側の余白をクリックします (またはコード行を選択して、**F9** キーを押します)。

    ![ブレークポイントを設定する](../debugger/media/dbg-qs-set-breakpoint.png "ブレークポイントの設定")

2. ここで **F5** キーを押します (または **[デバッグ] > [デバッグの開始]** の順に選択します)。

    ![ブレークポイントに到達する](../debugger/media/dbg-qs-hit-breakpoint.png "ブレークポイントに到達する")

    ブレークポイントを設定した場所でデバッガーが一時停止します。 デバッガーとアプリの実行が一時停止されているステートメントが、黄色の矢印で示されます。 `doWork` 関数呼び出しがある行はまだ実行されていません。

    > [!TIP]
    > ループまたは再帰処理の中にブレークポイントがある場合、または頻繁にステップ実行するブレークポイントが数多くある場合、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を使用して、特定の条件が満たされる場合にのみコードが中断されるようにしてください。 条件付きブレークポイントでは時間が節約され、再現が難しい問題をより簡単にデバッグすることもできます。

    C++ でメモリ関連エラーのデバッグを試みる場合、ブレークポイントを使用して、アドレス値 (NULL を検索) と参照カウントを検査することもできます。

## <a name="navigate-code"></a>コード間の移動

続行するようにデバッガーに指示するためのさまざまなコマンドがあります。 ここでは、Visual Studio 2017 以降で使用できる便利なコード ナビゲーション コマンドを示します。

ブレークポイントで一時停止している間に、緑色の **[クリックで実行]** ボタン ![[クリックで実行]](../debugger/media/dbg-tour-run-to-click.png "RunToClick") が表示されるまでステートメント `c1.push_back(20)` をポイントし、表示されたら **[クリックで実行]** ボタンを押します。

![クリックで実行](../debugger/media/dbg-qs-run-to-click.png "クリックで実行")

アプリは引き続き実行され、`doWork` が呼び出され、ボタンをクリックしたコード行で一時停止します。

コードのステップ実行に使用される一般的なキーボード コマンドには、**F10** と **F11** が含まれます。 詳しい手順については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」をご覧ください。

## <a name="inspect-variables-in-a-datatip"></a>データヒントの変数を検査する

1. (黄色の実行ポインターでマークされた) コードの現在の行で、`c1` オブジェクトをマウスでポイントしてデータヒントを表示します。

    ![データヒントを表示する](../debugger/media/dbg-qs-data-tip.png "データヒントを表示する")

    データヒントでは、`c1` 変数の現在の値が示され、そのプロパティを検査することができます。 デバッグ中に、予期しない値が表示される場合は、先行するコード行または呼び出しているコード行にバグがある可能性があります。

2. データヒントを展開して、`c1` オブジェクトの現在のプロパティ値を確認します。

3. コードを実行している間に `c1` の値を引き続き表示できるようにデータヒントをピン留めする場合は、小さいピン アイコンをクリックします (ピン留めしたデータヒントを任意の場所に移動することができます)。

## <a name="edit-code-and-continue-debugging"></a>コードを編集してデバッグを続行する

デバッグ セッションの途中にコードでテストする変更を識別する場合は、そのようにすることもできます。

1. `c2.front()` の 2 番目のインスタンスをクリックし、`c2.front()` を `c2.back()` に変更します。

2. **F10** キー (または **[デバッグ] > [ステップ オーバー]** ) を数回押して、デバッガーを進めて編集したコードを実行します。

    ![エディット コンティニュ](../debugger/media/dbg-qs-edit-and-continue.gif "エディット コンティニュ")

    **F10** キーでは、デバッガーは一度に 1 ステートメントずつ進みますが、関数をステップインするのではなく、ステップ オーバーします (スキップしたコードがまだ実行される)。

エディット コンティニュの使用および機能制限の詳細については、[エディット コンティニュ](../debugger/edit-and-continue.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、デバッガーを起動する方法、コードをステップ実行する方法、変数を確認する方法について学習しました。 必要に応じて、デバッガー機能の概要と、詳細情報へのリンクを取得します。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
