---
title: Visual Studio での拡張 UI 遅延の診断 |Microsoft Docs
description: 拡張機能によって UI の遅延が発生する可能性がある場合は、Visual Studio によって通知されます。 拡張コードで UI の遅延が発生している内容を診断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: conceptual
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload: multiple
ms.openlocfilehash: 7bc43d806595c7653421daec6efabb087cc1071c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171358"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>方法: 拡張機能による診断 UI の遅延

UI が応答しなくなると、Visual Studio は、リーフから開始し、ベースに向かって動作する UI スレッドのコールスタックを調べます。 Visual Studio で、コールスタックフレームがインストール済みで有効な拡張機能の一部であるモジュールに属していると判断された場合、通知が表示されます。

![UI 遅延 (無応答) 通知](media/ui-delay-notification-in-vs.png)

この通知は、UI の遅延 (UI の無応答) が拡張機能からのコードの結果である可能性があることをユーザーに通知します。 また、その拡張機能に対する拡張機能または今後の通知を無効にするオプションをユーザーに提供します。

このドキュメントでは、UI 遅延通知の原因となっている拡張機能コードの内容を診断する方法について説明します。

> [!NOTE]
> UI の遅延を診断するために、Visual Studio の実験的なインスタンスを使用しないでください。 UI 遅延通知に必要なコールスタック分析の一部は、実験用インスタンスの使用時にオフになります。つまり、UI 遅延通知が表示されないことがあります。

診断プロセスの概要は次のとおりです。
1. トリガーのシナリオを特定します。
2. アクティビティログ記録を使用して VS を再起動します。
3. ETW トレースを開始します。
4. 通知が再度表示されるようにトリガーします。
5. ETW トレースを停止します。
6. アクティビティログを調べて、遅延 ID を取得します。
7. 手順 6. の遅延 ID を使用して ETW トレースを分析します。

以下のセクションでは、これらの手順について詳しく説明します。

## <a name="identify-the-trigger-scenario"></a>トリガーのシナリオを特定する

UI の遅延を診断するには、まず、Visual Studio が通知を表示する (アクションのシーケンス) 内容を識別する必要があります。 これは、ログ記録が有効になっている通知を後でトリガーできるようにするためです。

## <a name="restart-vs-with-activity-logging-on"></a>アクティビティログをオンにして VS を再起動する

Visual Studio では、問題をデバッグするときに役立つ情報を提供する "アクティビティログ" を生成できます。 Visual Studio でアクティビティログをオンにするには、[コマンドライン] オプションを使用して Visual Studio を開き `/log` ます。 Visual Studio が起動すると、アクティビティログは次の場所に格納されます。

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

VS インスタンス ID を見つける方法の詳細については、「 [Visual Studio インスタンスを検出および管理するためのツール](../install/tools-for-managing-visual-studio-instances.md)」を参照してください。 このアクティビティログは後で使用して、UI の遅延と関連する通知に関する詳細情報を確認します。

## <a name="starting-etw-tracing"></a>ETW トレースの開始

[Perfview](https://github.com/Microsoft/perfview/)を使用すると、ETW トレースを収集できます。 PerfView には、ETW トレースの収集と分析のための使いやすいインターフェイスが用意されています。 トレースを収集するには、次のコマンドを使用します。

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

これにより、"VisualStudio" プロバイダーが有効になります。これは、Visual Studio が UI 遅延通知に関連するイベントに対して使用するプロバイダーです。 また、PerfView が **スレッド時間スタック** ビューを生成するために使用できるカーネルプロバイダーのキーワードも指定します。

## <a name="trigger-the-notification-to-appear-again"></a>通知が再度表示されるようにトリガーする

PerfView がトレースコレクションを開始したら、通知を再度表示するために、(手順1の) トリガーアクションシーケンスを使用できます。 通知が表示されたら、PerfView のトレースコレクションを停止して、出力トレースファイルを処理および生成できます。

## <a name="stop-etw-tracing"></a>ETW トレースの停止

トレースコレクションを停止するには、[PerfView] ウィンドウの [ **コレクションの停止** ] ボタンを使用します。 トレースコレクションを停止すると、PerfView によって ETW イベントが自動的に処理され、出力トレースファイルが生成されます。

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>アクティビティログを調べて遅延 ID を取得します

既に説明したように、 *%APPDATA%\Microsoft\VisualStudio \<vs_instance_id>\ActivityLog.xml* でアクティビティログを見つけることができます。 Visual Studio は、拡張 UI の遅延を検出するたびに、ソースとしてを使用して、アクティビティログにノードを書き込み `UIDelayNotifications` ます。 このノードには、UI の遅延に関する4つの情報が含まれています。

- UI 遅延 ID。 VS セッションで UI 遅延を一意に識別するための連続した数値です。
- 開始から終了までの Visual Studio セッションを一意に識別するセッション ID。
- UI の遅延について通知が表示されたかどうか
- UI の遅延の原因と考えられる拡張機能

```xml
<entry>
  <record>271</record>
  <time>2018/02/03 12:02:52.867</time>
  <type>Information</type>
  <source>UIDelayNotifications</source>
  <description>A UI delay (Delay ID = 0) has been detected. (Session ID=16e49d4b-26c2-4247-ad1c-488edeb185e0; Blamed extension="UIDelayR2"; Notification shown? Yes.)</description>
</entry>
```

> [!NOTE]
> すべての UI の遅延によって通知が発生するわけではありません。 そのため、適切な UI 遅延を正しく識別するには、 **[通知]** の値を常に確認してください。

アクティビティログで正しい UI 遅延を見つけたら、ノードに指定されている UI 遅延 ID を書き留めます。 次の手順で、ID を使用して対応する ETW イベントを検索します。

## <a name="analyze-the-etw-trace"></a>ETW トレースの分析

次に、トレースファイルを開きます。 これを行うには、PerfView の同じインスタンスを使用するか、新しいインスタンスを開始し、ウィンドウの左上にある現在のフォルダーパスをトレースファイルの場所に設定します。

![Perfview でのフォルダーパスの設定](media/perfview-set-path.png)

次に、左側のウィンドウでトレースファイルを選択し、右クリックまたはコンテキストメニューから [ **開く** ] を選択して開きます。

> [!NOTE]
> 既定では、PerfView は Zip アーカイブを出力します。 *trace.zip* を開くと、アーカイブが自動的に圧縮解除され、トレースが開きます。 トレースの収集中に [ **Zip** ] ボックスをオフにすることで、これをスキップできます。 ただし、異なるコンピューター間でトレースを転送して使用する場合は、 **Zip** ボックスをオフにしないことを強くお勧めします。 このオプションを指定しない場合、Ngen アセンブリに必要な Pdb はトレースに含まれないため、Ngen アセンブリからのシンボルは対象のコンピューターで解決されません。 (Ngen アセンブリの Pdb の詳細については、こちらの [ブログ投稿](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/) を参照してください。)

PerfView がトレースを処理して開くには、数分かかることがあります。 トレースが開かれると、その下にさまざまな "ビュー" の一覧が表示されます。

![PerfView トレースの概要ビュー](media/perfview-summary-view-events-selected.png)

まず、 **イベント** ビューを使用して、UI 遅延の時間範囲を取得します。

1. トレースの下にあるノードを選択 `Events` し、右クリックまたはコンテキストメニューから [**開く**] を選択して、イベントビューを開きます。
2. 左側のウィンドウで [] を選択し `Microsoft-VisualStudio/ExtensionUIUnresponsiveness` ます。
3. Enter キーを押す

選択内容が適用され、すべての `ExtensionUIUnresponsiveness` イベントが右ペインに表示されます。

![イベントビューでのイベントの選択](media/perfview-event-selection.png)

右ペインの各行は、UI の遅延に対応しています。 イベントには、ステップ6のアクティビティログの遅延 ID と一致する "遅延 ID" 値が含まれます。 `ExtensionUIUnresponsiveness`は ui の遅延の最後に発生するため、イベントのタイムスタンプ (ほぼ) は ui の遅延の終了時刻を示します。 イベントには、遅延時間も含まれます。 終了タイムスタンプから期間を減算して、UI の遅延が開始されたときのタイムスタンプを取得できます。

![UI 遅延時間範囲の計算](media/ui-delay-time-range.png)

たとえば、前のスクリーンショットでは、イベントのタイムスタンプは12125.679 であり、遅延時間は 6143.085 (ms) です。 したがって
* 遅延開始は 12125.679-6143.085 = 5982.594 です。
* UI 遅延時間の範囲は 5982.594 ~ 12125.679 です。

時間範囲を設定したら、[ **イベント** ] ビューを閉じて、[ **スレッド時間 (startstop アクティビティを含む)] スタック** ビューを開くことができます。 このビューは特に便利です。なぜなら、UI スレッドをブロックしている拡張機能は、他のスレッドまたは i/o バインド操作を待機しているだけなのです。 そのため、ほとんどの場合、[ **Cpu スタック** ] ビューは、その時間に cpu を使用していないためにスレッドがブロックする時間をキャプチャしない可能性があります。 **スレッド時間スタック** は、ブロック時間を適切に表示することで、この問題を解決します。

![PerfView 概要ビューのスレッド時間 (StartStop アクティビティを含む) スタックノード](media/perfview-thread-time-with-startstop-activities-stacks.png)

**スレッド時間スタック** ビューを開くときに、分析を開始する **devenv** プロセスを選択します。

![UI 遅延分析のスレッド時間スタックビュー](media/ui-delay-thread-time-stacks.png)

ページの左上にある **スレッド時間スタック** ビューでは、前の手順で計算した値に時間範囲を設定し、 **enter** キーを押すと、その時間範囲にスタックが調整されます。

> [!NOTE]
> Visual Studio が既に開いているときにトレースコレクションが開始されている場合は、どのスレッドが UI (スタートアップ) スレッドであるかを判断することができます。 ただし、UI (スタートアップ) スレッドのスタック上の最初の要素は、ほとんどの場合、オペレーティングシステム Dll (*ntdll.dll* および *kernel32.dll*) の後にが続き、その後にが続き `devenv!?` `msenv!?` ます。 このシーケンスは、UI スレッドを識別するのに役立ちます。

 ![スタートアップスレッドの識別](media/ui-delay-startup-thread.png)

また、パッケージのモジュールを含むスタックだけを含めることで、このビューをフィルター処理できます。

* 既定で追加されたグループを削除するには、 **Groupて s** を空のテキストに設定します。
* 既存のプロセスフィルターに加えて、アセンブリ名の一部を含めるよう **に設定し** ます。 この場合は、devenv にする必要があり **ます。UIDelayR2**。

![スレッド時間スタックビューでの GroupPath とインシデントパスの設定](media/perfview-tts-group-path-inc-path.png)

PerfView には、コードのパフォーマンスのボトルネックを特定するために使用できる [ **ヘルプ** ] メニューの詳細なガイダンスがあります。 さらに、Visual Studio のスレッド Api を使用してコードを最適化する方法の詳細については、次のリンク先を参照してください。

* [https://github.com/Microsoft/vs-threading/blob/master/doc/index.md](https://github.com/Microsoft/vs-threading/blob/master/doc/index.md)
* [https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md)

新しい Visual Studio の拡張機能の静的アナライザー ( [ここで](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)は NuGet パッケージ) を使用して、効率的な拡張機能を記述するためのベストプラクティスに関するガイダンスを提供することもできます。 [VS SDK アナライザー](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md)と[スレッドアナライザー](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md)の一覧については、「」を参照してください。

> [!NOTE]
> 制御できない依存関係が原因で無応答に対処できない場合 (たとえば、拡張機能が UI スレッドで同期 VS services を呼び出す必要がある場合)、そのことを知りたいと考えています。 Visual Studio パートナープログラムのメンバーである場合は、developer support の要求を送信してお問い合わせください。 それ以外の場合は、[問題の報告] ツールを使用してフィードバックを送信し、 `"Extension UI Delay Notifications"` タイトルに含めます。 また、分析の詳細な説明も含めてください。
