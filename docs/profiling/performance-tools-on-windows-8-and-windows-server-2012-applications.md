---
title: Windows 8 および Windows Server 2012 アプリでのパフォーマンス ツール
ms.date: 06/19/2017
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3938e7dc1b3ec33c8a4cf74b6957067bbdfd6185
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778428"
---
# <a name="performance-tools-on-windows-8-and-windows-server-2012-applications"></a>Windows 8 と Windows Server 2012 アプリケーションのパフォーマンス ツール

Windows 8 および Windows Server 2012 から強化されたセキュリティ機能によって、Visual Studio パフォーマンス ツールがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 このトピックでは、Windows 8 および Windows Server 2012 プラットフォームからのパフォーマンス ツールの変更点について説明します。

> [!NOTE]
> その他のサポートされている Windows バージョン (Windows 7、Windows Server 2008 R2) でのパフォーマンス ツールに変更点はありません。

## <a name="collect-data-on-uwp-apps-from-the-visual-studio-ide"></a>Visual Studio IDE から UWP アプリ上のデータを収集する

JavaScript および HTML 5 で記述された UWP アプリのプロファイリングを行う場合は、JavaScript コードのインストルメンテーション データを収集します。 Visual C++、Visual C#、または Visual Basic で記述された UWP アプリまたはコンポーネントのプロファイリングを行う場合は、ネイティブ コードおよびマネージド コードのサンプリング データを収集します。 ローカル コンピューターまたはリモート コンピューター上のアプリをプロファイリングすることもできます。

UWP アプリのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。

- サンプリング メソッドを使用した JavaScript アプリのプロファイリング。
- インストルメンテーション メソッドを使用したマネージド コードおよびネイティブ コードのプロファイリング。
- コンカレンシー プロファイル
- .NET メモリ プロファイル。
- 階層相互作用プロファイリング (TIP)。
- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。
- パフォーマンス カウンター データや Windows カウンター データの収集、追加のコマンド ライン オプションの指定などのインストルメンテーション オプション。

UWP アプリのプロファイリングの詳細については、次の記事をご覧ください。

- [ローカル コンピューターで UWP アプリを実行する](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)
- [リモート コンピューターで UWP アプリを実行する](../debugger/run-windows-store-apps-on-a-remote-machine.md)
- [プロファイル ツールの概要](profiling-feature-tour.md)
- [JavaScript メモリ](../profiling/javascript-memory.md)
- [ローカル コンピューターでの UWP アプリの Visual C++、Visual C#、および Visual Basic コードのプロファイリング](https://msdn.microsoft.com/2d0c939e-0bac-48c5-b727-46f6c6113060)
- [リモート デバイスでの UWP アプリの Visual C++、Visual C#、および Visual Basic コードのプロファイリング](https://msdn.microsoft.com/b932a2be-11b0-40fd-b996-75c6b6a79d22)
- [UWP アプリの Visual C++、Visual C#、および Visual Basic コードのパフォーマンス データの分析](https://msdn.microsoft.com/5de4a413-d924-425f-afc4-e1ecfb0fca18)

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-from-the-visual-studio-ide"></a>Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE から収集する

インストルメンテーション メソッドを使用したプロファイリングについては、Windows 8 での変更点はありません。

サンプリング メソッドを使用した階層相互作用プロファイリング (TIP) は、サポートされていません。

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-by-using-sampling-from-the-visual-studio-ide"></a>Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE からサンプリングを使用して収集する

サンプリング メソッドを使用して Windows 8 デスクトップ アプリケーションまたは Windows Server 2012 アプリケーションのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。

- 階層相互作用プロファイリング (TIP)。 インストルメンテーションを使用した TIP データの収集はサポートされます。

- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。

## <a name="profile-from-the-command-line"></a>コマンド ラインからのプロファイリング

Visual Studio がインストールされていないデバイスを含めて、Windows 8 デバイスおよび Windows Server 2012 デバイスでプロファイル データを収集するには、次の 2 つのコマンド ライン ツールを使用します。

|ツール名|説明|
|---------------|-----------------|
|[VSPerf](../profiling/vsperf.md)|UWP アプリからプロファイル データを収集し、Windows 8 デスクトップ アプリケーションおよび Windows Server 2012 アプリケーションからサンプル プロファイル データを収集します。|
|[VSPerfCmd](../profiling/vsperfcmd.md)|Windows 8 デスクトップまたは Windows Server 2012 で実行されるアプリから、インストルメンテーション、コンカレンシー、および階層相互作用プロファイル データを収集します。 以前のバージョンの Windows からすべてのタイプのプロファイル データを収集します。|

これらのツールはどちらも、Visual Studio と共にローカル コンピューターにインストールされます。

Visual Studio がインストールされていないデバイスでアプリケーションをプロファイリングするには、次のいずれかを実行します。

- [MSDN Web サイト](https://visualstudio.microsoft.com/#downloads+d-additional-software)から、Visual Studio 用のリモート ツールの一部としてツールをダウンロードします。

- 既存の Visual Studio コンピューターから、スタンドアロンのプロファイラー ツール インストール プログラムをコピーして実行します。 プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 リモート コンピューターのオペレーティング システム (x86/x64) に対応するセットアップ プログラムを選択します。

> [!NOTE]
> TIP プロファイル データを収集するには、Visual Studio コンピューターにあるスタンドアロン プロファイラーをリモート コンピューターにインストールする必要があります。

コマンド ラインから Windows 8 アプリケーションおよび Windows Server 2012 アプリケーションのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。

- [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md)でサンプリング モードを使用して、Windows 8 と Windows Server 2012 の Web アプリからデータを収集します。

- VsPerfCmd.exe を使用したサンプリング データの収集。

- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。

## <a name="collect-tier-interaction-tip-data"></a>階層の相互作用 (TIP) データを収集する

階層相互作用プロファイリングにより、ADO.NET サービスを通じてデータベースと通信する多階層アプリケーションの関数の実行時間に関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。

**Visual Studio のエディション**

階層相互作用プロファイル データは、Visual Studio の任意のエディションを使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、Visual Studio Enterprise のみです。

**Windows 8 と Windows Server 2012**

1. Windows 8 デスクトップまたは Windows Server 2012 で実行されるアプリから相互作用データを収集するには、インストルメンテーション メソッドを使用する必要があります。

2. UWP アプリの階層相互作用データを収集することはできません。

3. 階層相互作用データは、サポートされている他のバージョンの Windows で、すべてのプロファイル方法に含めることができます。

**パフォーマンス ウィザードとパフォーマンス エクスプローラー**

パフォーマンス エクスプローラーから、階層相互作用データの収集オプションをプロファイリング実行に追加する必要があります。 また、パフォーマンス エクスプローラーのターゲット ノードに、プロジェクト、実行可能ファイル、または Web サイトを追加する必要があります。 [階層相互作用データを収集する](../profiling/collecting-tier-interaction-data.md)方法に関するページを参照してください。

**リモート コンピューターでの TIP データの収集**

リモート コンピューターで階層相互作用データを収集するには、Visual Studio コンピューターの *%VSInstallDir%\Team Tools\Performance Tools\Setups* フォルダーから **vs\_profiler\_** _\<プラットフォーム>_ **\_** _\<言語>_ **.exe** ファイルをリモート コンピューターにコピーしてインストールする必要があります。 [リモート デバッグ](../debugger/remote-debugging.md)のダウンロード パッケージにあるプロファイリング ツールを使用することはできません。

プロファイル データを収集するには、[VSPerfCmd](../profiling/vsperfcmd.md) または [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) を使用できます。

**TIP レポート**

階層相互作用データは、Visual Studio Enterprise でのみ表示できます。 [VSPerfReport](../profiling/vsperfreport.md) の使用による、ファイル ベースの階層相互作用レポートは利用できません。

## <a name="see-also"></a>関連項目

[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)
[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
