---
title: IntelliTrace を使用して以前のアプリ状態を参照する
description: スナップショットの作成方法、および IntelliTrace ステップ バックを使用したスナップショットの表示方法について説明します
ms.custom: seodec18
ms.date: 09/19/2018
ms.topic: tutorial
ms.assetid: 7c60d929-d993-49dc-9db3-43b30be9912b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f1ab54ccb3820b3a03724c30d16f08b3e8a45493
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933103"
---
# <a name="inspect-previous-app-states-using-intellitrace-step-back-in-visual-studio-visual-studio-enterprise"></a>Visual Studio の IntelliTrace のステップ バックを使用して以前のアプリケーション状態を調べる (Visual Studio Enterprise)

IntelliTrace のステップ バックでは、ブレークポイントとデバッガー ステップ イベントごとにアプリケーションのスナップショットを自動作成します。 記録されたスナップショットにより、前のブレークポイントまたはステップに戻り、過去の時点でのアプリケーションの状態を確認できるようになります。 IntelliTrace ステップ バックでは、以前のアプリケーションの状態を確認したいが、デバッグの再開や必要なアプリ状態の再作成は必要でない場合に時間を節約できます。

IntelliTrace のステップ バックは、Visual Studio Enterprise 2017 バージョン 15.5 以降から使用できます。これでは Windows 10 Anniversary Update 以降が必要です。 現在、この機能は ASP.NET、WinForms、WPF、マネージド コンソール アプリ、マネージド クラス ライブラリのデバッグでサポートされています。 この機能は、Visual Studio 2017 Enterprise バージョン 15.7 以降では、ASP.NET Core と .NET Core でもサポートされています。 この機能は、Visual Studio 2017 Enterprise バージョン 15.9 プレビュー 2 では、Windows のネイティブ アプリでもサポートされています。 UWP アプリケーションのデバッグは現在サポートされていません。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * IntelliTrace イベントとスナップショットの有効化
> * ステップ バックおよび次へ進むコマンドを使用したイベント間の移動
> * イベントのスナップショットの参照

## <a name="enable-intellitrace-events-and-snapshots-mode"></a>IntelliTrace イベントとスナップショット モードの有効化

1. Visual Studio Enterprise でプロジェクトを開きます。

1. **[ツール]**  >  **[オプション]**  >  **[IntelliTrace]** 設定を開き、 **[IntelliTrace events and snapshots]\(IntelliTrace のイベントとスナップショット\)** のオプションを選択します。

    Visual Studio 2017 Enterprise バージョン 15.9 プレビュー 2 以降では、このオプションは **[IntelliTrace snapshots (managed and native)]** \(IntelliTrace スナップショット (マネージドおよびネイティブ)\) になっています。

    ![IntelliTrace イベントとスナップショット モードの有効化](../debugger/media/intellitrace-enable-snapshots.png "IntelliTrace イベントとスナップショット モードの有効化")

1. 例外のスナップショットを表示するオプションを構成する場合、 **[オプション]** ダイアログ ボックスの **[IntelliTrace]**  >  **[詳細]** の順に選択します。

    これらのオプションは、Visual Studio 2017 Enterprise バージョン 15.7 以降にあります。

    ![例外時のスナップショットの動作の構成](../debugger/media/intellitrace-enable-snapshots-on-exceptions.png)

    イベントとスナップショットを有効にすると、例外でもスナップショットの作成が既定で有効になります。 **[Collect snapshots on exception events]** \(例外イベントでスナップショットを収集する\) をオフにすると、例外でのスナップショットを無効にできます。 この機能を有効にすると、未処理の例外でスナップショットが作成されます。 処理済みの例外の場合、スローされた例外が既にスローされている例外の再スローでない場合のみ、スナップショットは作成されます。 ドロップダウン リストから値を選択すると、例外時のスナップショットの最大数を設定することができます。 これは、(アプリがブレークポイントにヒットしたときなど) アプリがブレーク モードに入るたびの最大数です。

    > [!NOTE]
    > スナップショットは、IntelliTrace が記録する例外イベントのみに作成されます。 マネージド コードで IntelliTrace が記録するイベントを指定するには、 **[ツール]**  >  **[オプション]**  >  **[IntelliTrace イベント]** の順に選択します。

1. プロジェクトで、1 つ以上ブレークポイントを設定し、デバッグを開始 (**F5** キーを押します) するか、コードをステップ実行してデバッグを開始します (**F10** または **F11**)。

    IntelliTrace は、アプリケーションの手順のデバッガーのステップ実行、ブレークポイント イベント、未処理の例外イベントごとにスナップショットを作成します。 これらのイベントは、 **[診断ツール]** ウィンドウの **[イベント]** タブに、その他の IntelliTrace のイベントと共に記録されます。 ウィンドウを開くには、 **[デバッグ]**  >  **[Windows]**  >  **[診断ツールの表示]** の順に選択します。

    スナップショットがあるイベントの横にはカメラ アイコンが表示されます。

    ![[イベント] タブとスナップショット](../debugger/media/intellitrace-events-tab-with-snapshots.png "ブレークポイントとステップのスナップショットを含む [イベント] タブ")

    パフォーマンス上の理由から、非常に迅速にステップ実行された場合、スナップショットは作成されません。 ステップの横にカメラ アイコンが表示されない場合は、ステップ実行をもっとゆっくり実行してみてください。

## <a name="navigate-and-view-snapshots"></a>スナップショット間の移動と参照

1. イベント間を移動するには、デバッグ ツールバーの **[前に戻る]** (Alt + [) ボタンと **[次へ進む]** (Alt + ]) ボタンを使用します。

    これらのボタンを使用すると、 **[診断ツール]** ウィンドウの **[イベント]** タブに表示されるイベント間を移動できます。 あるイベントに戻るまたは進むと、選択したイベントの[デバッグ履歴](../debugger/historical-debugging.md)が自動的に有効になります。

    ![[前に戻る] ボタンと [次へ進む] ボタン](../debugger/media/intellitrace-step-back-icons-description.png "[前に戻る] ボタンと [次へ進む] ボタン")

    前に戻ったり、次へ進んだりすると、Visual Studio はデバッグ履歴モードになります。 このモードでは、選択しているイベントが記録されたときにデバッガーのコンテキストが切り替わります。 ポインターも、Visual Studio によりソース ウィンドウの対応するコード行に移動します。

    このビューでは、値を **[呼び出し履歴]** 、 **[ローカル]** 、 **[自動変数]** および **[Watch]** ウィンドウで確認できます。 また、変数の上にマウスを置き、[データヒント] を表示して、式の評価を **[イミディエイト]** ウィンドウで実行できます。 表示されるデータは、アプリケーションのプロセスの時点で作成されたスナップショットからのものです。

    そのため、たとえばブレークポイントにヒットし、ステップを実行した場合 (**F10**)、 **[前に戻る]** ボタンにより Visual Studio は、ブレークポイントに対応するコード行で履歴モードになります。

    ![スナップショットがあるイベントで履歴モードをアクティブにする](../debugger/media/intellitrace-historical-mode-with-snapshot.png "スナップショットがあるイベントで履歴モードをアクティブにする")

2. ライブ実行に戻るには、 **[続行] (F5)** を選択するか、情報バーの **[Return to Live Debugging]** \(ライブ デバッグに戻る\) リンクをクリックします。

3. スナップショットは、 **[イベント]** タブで確認することも可能です。これを実行するには、スナップショットがあるイベントを選択し、 **[デバッグ履歴の有効化]** をクリックします。

    ![イベントの [デバッグ履歴の有効化]](../debugger/media/intellitrace-activate-historical-debugging.png "イベントの [デバッグ履歴の有効化]")

    **[次のステートメントの設定]** コマンドとは異なり、スナップショットを表示してもコードは再実行されません。過去にそれが起こった時点のアプリケーション状態の静的なビューが表示されます。

    ![IntelliTrace のステップ バックの概要](../debugger/media/intellitrace-step-back-overview.png "IntelliTrace のステップ バックの概要")

    Visual Studio で変数を確認する方法の詳細については、[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)に関するページを参照してください。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

#### <a name="how-is-intellitrace-step-back-different-from-intellitrace-events-only-mode"></a>IntelliTrace のステップ バックは IntelliTrace のイベント限定モードとどのように違いますか?

IntelliTrace のイベント限定モードでは、デバッガーのステップ実行とブレークポイントでデバッグ履歴を有効にできます。 ただし、IntelliTrace はウィンドウが開いている場合の **[ローカル]** および **[自動変数]** ウィンドウのデータしかキャプチャしません。そしてキャプチャされるのは、展開されて表示されているもののみです。 イベント限定モードでは、多くの場合、変数の完全なビューと複合オブジェクトがありません。 また、 **[ウォッチ]** ウィンドウでの式の評価とデータの参照はサポートされていません。

イベントおよびスナップショット モードでは、IntelliTrace は複合オブジェクトを含むアプリケーションのプロセスのスナップショット全体をキャプチャします。 コード行では、ブレークポイントで停止したのと同じ状態で同じ情報が表示されます (これは以前情報を開いたかどうかには関係しません)。 スナップショットを参照するとき、式の評価もサポートされます。  

#### <a name="what-is-the-performance-impact-of-this-feature"></a>この機能はパフォーマンスにどのような影響を与えますか? 

ステップ実行がパフォーマンス全体に与える影響は、アプリケーションによって異なります。 スナップショットの作成にかかるオーバーヘッドは、約 30 ミリ秒です。 スナップショットが作成されると、アプリのプロセスがフォークされ、フォークされたコピーが中断されます。 スナップショットを参照するとき、Visual Studio はプロセスのフォークされたコピーにアタッチされています。 Visual Studio は各スナップショットで、ページ テーブルのみをコピーし、ページをコピー オン ライトとして設定します。 関連付けられているスナップショットがあるデバッガーのステップ間でヒープのオブジェクトが変わる場合、該当するページ テーブルがコピーされるので、メモリのコストはわずかになります。 Visual Studio がスナップショットを作成するのに十分なメモリがないと判断した場合、作成されません。

## <a name="known-issues"></a>既知の問題
* Windows 10 Fall Creators Update (RS3) より後のバージョンの Windows で IntelliTrace のイベントとスナップショット モードを使用しており、アプリケーションのデバッグ プラットフォーム ターゲットが x86 に設定されている場合、IntelliTrace ではスナップショットを作成しません。

    回避策:
  * Windows 10 Anniversary Update (RS1) のバージョン 10.0.14393.2273 未満を使用している場合、[KB4103720 をインストール](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)します。
  * Windows 10 Creators Update (RS2) のバージョン 10.0.15063.1112 未満を使用している場合、[KB4103722 をインストール](https://support.microsoft.com/help/4103722/windows-10-update-4103722)します。
  * Windows 10 Fall Creators Update (RS3) をインストールするか、これにアップグレードします。
  * または、次のようにします。
    1. Visual Studio インストーラーからデスクトップ (x86、x64) コンポーネント用の VC++ 2015.3 v140 ツールセットをインストールします。
    2. 対象アプリケーションをビルドします。
    3. コマンド ラインで editbin ツールを使って、ターゲット実行可能ファイルの `Largeaddressaware` フラグを設定します。 たとえば、(パスのアップデート後) 次のコマンドを使用します。"C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise\VC\Tools\MSVC\14.12.25718\bin\Hostx86\x86\editbin.exe" /Largeaddressaware "C:\Path\To\Application\app.exe"
    4. デバッグを開始するには、**F5** キーを押します。 これで、デバッガーのステップ実行とブレークポイントでスナップショットが作成されるようになります。

       > [!Note]
       > `Largeaddressaware` フラグは、実行可能ファイルが変更され再構築されるたびに設定する必要があります。

* アプリケーションのプロセスのスナップショットが永続化メモリにマップされたファイルを使用するアプリケーションで作成された場合、(親プロセスでロックがリリースされた場合も) そのスナップショットのプロセスがメモリでマップされたファイルの排他的ロックを保持します。 その他のプロセスは、依然メモリにマップ済みのファイルを読み取ることはできますが、書き込むことはできません。

  対応策 :
  * デバッグ セッションを終了して、すべてのスナップショットをクリアします。

* 多数の DLL を読み込むアプリケーションなど、そのプロセスに一意のメモリ領域が多数あるアプリケーションをデバッグする場合、スナップショットが有効なステップ実行のパフォーマンスに影響がある場合があります。 この問題は、Windows の今後のバージョンで対処される予定です。 この問題が発生している場合は、stepback@microsoft.com までご連絡ください。

* イベントおよびスナップショット モードで **[デバッグ] > [IntelliTrace] > [IntelliTrace セッションを保存する]** でファイルを保存する場合、スナップショットからキャプチャしたその他のデータは .itrace ファイルにはありません。 ブレークポイントやステップ イベントでは、IntelliTrace イベントのみモードでファイルを保存したのと同じ情報が表示されます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、IntelliTrace でステップ バックの使用方法を学習しました。 他の IntelliTrace の機能の詳細については、以下を参照してください。

> [!div class="nextstepaction"]
> [IntelliTrace の機能](../debugger/intellitrace-features.md)
