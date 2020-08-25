---
title: コマンド ラインからのパフォーマンスの測定
description: アプリケーションの CPU パフォーマンスとマネージド メモリ使用量をコマンド ラインから測定します。
ms.custom: ''
ms.date: 02/21/2020
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, command-line
- Diagnostics Tools, command-line
- CPU Usage, command-line
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 56007fcb3b951f9b313a25092e89c234d52eb15e
ms.sourcegitcommit: 8e5b0106061bb43247373df33d0850ae68457f5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88508000"
---
# <a name="measure-application-performance-from-the-command-line"></a>コマンド ラインからアプリケーションのパフォーマンスを測定する

コマンドライン ツールを使用して、アプリケーションに関するパフォーマンス情報を収集できます。

この記事に記載されている例では、Microsoft メモ帳のパフォーマンス情報を収集しますが、同じ方法を使用して任意のプロセスをプロファイルすることができます。

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio 2019 以降のバージョン

* コマンドライン ツールに関する知識

* Visual Studio がインストールされていない状態でリモート マシン上のパフォーマンス情報を収集するには、リモート マシンに [Visual Studio 用のパフォーマンス ツール](https://visualstudio.microsoft.com/downloads#remote-tools-for-visual-studio-2019)をインストールします。 ツールのバージョンは、使用している Visual Studio のバージョンと一致している必要があります。

## <a name="collect-performance-data"></a>パフォーマンス データを収集する

Visual Studio Diagnostics CLI ツールを使用したプロファイリングは、プロファイリング ツールを 1 つのコレクター エージェントと共にプロセスにアタッチすることで機能します。 プロファイリング ツールをアタッチすると、ツールが停止するまでプロファイリング データをキャプチャして保存する診断セッションが開始されます。ツールが停止した時点で、そのデータは *.diagsession* ファイルにエクスポートされます。 このファイルは、Visual Studio で開いて結果を分析できます。

1. メモ帳を起動し、タスク マネージャーを開いてプロセス ID (PID) を取得します。 タスク マネージャーの **[詳細]** タブで PID を見つけます。

1. コマンド プロンプトを開き、実行可能な収集エージェントがあるディレクトリ (通常は次のディレクトリ) に移動します (Visual Studio Enterprise の場合)。

   ```<Visual Studio installation folder>\2019\Enterprise\Team Tools\DiagnosticsHub\Collector\```

1. 次のコマンドを入力して *VSDiagnostics.exe* を起動します。

   ```cmd
   VSDiagnostics.exe start <id> /attach:<pid> /loadConfig:<configFile>
   ```

   含める必要がある引数は次のとおりです。

   * \<*id*>。収集セッションを識別します。 ID は常に 1 - 255 の数字です。
   * \<*pid*>。プロファイルするプロセスの PID。この場合は手順 1 で見つけた PID です。
   * \<*configFile*>。起動する収集エージェントの構成ファイル。 詳細については、[エージェントの構成ファイル](#config_file)に関するセクションを参照してください。

   たとえば、前に説明したように *pid* の置換することで CPUUsageBase エージェントに次のコマンドを使用できます。

   ```cmd
   VSDiagnostics.exe start 1 /attach:<pid> /loadConfig:AgentConfigs\CPUUsageLow.json
   ```

1. メモ帳のサイズを変更するか、興味深い何らかの入力プロファイリング情報が確実に収集されるようにメモ帳に何かを入力します。

1. 次のコマンドを入力して、収集セッションを停止し、ファイルに出力を送信します。

   ```cmd
   VSDiagnostics.exe stop <id> /output:<path to file>
   ```

1. 前のコマンドから出力された *.diagsession* ファイルを見つけ、Visual Studio でそれを開いて ( **[ファイル]** 、 **[開く]** )、収集された情報を調べます。

   結果を分析するには、該当するパフォーマンス ツールのドキュメントを参照してください。 たとえば、[CPU 使用率](../profiling/cpu-usage.md)、[.NET オブジェクト割り当てツール](../profiling/dotnet-alloc-tool.md)、または[データベース](../profiling/analyze-database.md) ツールがあります。

## <a name="agent-configuration-files"></a><a name="config_file"></a> エージェントの構成ファイル

収集エージェントは、測定対象が何かに応じて、さまざまな種類のデータを収集する交換可能なコンポーネントです。

便宜上、その情報をエージェント構成ファイルに保管することができます。 構成ファイルは、少なくとも *.dll* の名前とその COM CLSID を含む *.json* ファイルです。 以下は、次のフォルダー内にある構成ファイルの例です。

```<Visual Studio installation folder>Team Tools\DiagnosticsHub\Collector\AgentConfigs\```

エージェントの構成ファイルをダウンロードして表示するには、以下のリンクを参照してください。

- https://aka.ms/vs/diaghub/agentconfig/cpubase
- https://aka.ms/vs/diaghub/agentconfig/cpuhigh
- https://aka.ms/vs/diaghub/agentconfig/cpulow
- https://aka.ms/vs/diaghub/agentconfig/database
- https://aka.ms/vs/diaghub/agentconfig/dotnetasyncbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetallocbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetalloclow

[CPU 使用率](../profiling/cpu-usage.md)プロファイル ツールについて収集されたデータに対応する CpuUsage 構成 (Base/High/Low)。
[.NET オブジェクト割り当てツール](../profiling/dotnet-alloc-tool.md)について収集されたデータに対応する DotNetObjectAlloc 構成 (Base/Low)。

Base/Low/High 構成はサンプリング レートを表します。 たとえば、Low は 100 サンプル/秒、High は 4,000 サンプル/秒です。

*VSDiagnostics.exe* ツールを収集エージェントと連携させるには、適切なエージェントの DLL と COM CLSID の両方が必要です。また、エージェントに追加の構成オプションが存在する場合があります。 構成ファイルなしでエージェントを使用する場合は、次のコマンドでこの形式を使用してください。

```cmd
VSDiagnostics.exe start <id> /attach:<pid> /loadAgent:<agentCLSID>;<agentName>[;<config>]
```

## <a name="permissions"></a>アクセス許可

昇格されたアクセス許可が必要なアプリケーションをプロファイルするには、昇格されたコマンド プロンプトから実行する必要があります。
