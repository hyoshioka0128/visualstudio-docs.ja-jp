---
title: 64 ビット アプリケーションをデバッグする | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], 64-bit
- 64-bit debugging
ms.assetid: db648e5f-6375-4e2d-aa98-eb7261958927
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3a805942e85540b776ceacd972a09a71bb80cbb4
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911578"
---
# <a name="debug-64-bit-applications"></a>64 ビット アプリケーションをデバッグする
ローカル コンピューターまたはリモート コンピューターで実行されている 64 ビット アプリケーションをデバッグできます。

 リモート コンピューターで実行されている 64 ビット アプリケーションをデバッグするには、「 [Remote Debugging](../debugger/remote-debugging.md)」をご覧ください。

 ローカルで 64 ビット アプリケーションをデバッグする場合、Visual Studio では 64 ビット ワーカー プロセス (msvsmon.exe) を使用して、32 ビットの Visual Studio プロセス内で実行できない低水準の操作を実行します。

 .NET Framework version 3.5 以前を使用する 64 ビット プロセスでは、混合モードのデバッグはサポートされません。

## <a name="debug-a-64-bit-application"></a>64 ビット アプリケーションのデバッグ
 64 ビット アプリケーションのデバッグを実行するには次のことを行います。

1. C# コンソール アプリケーションなど、Visual Studio ソリューションを作成します。

2. 構成マネージャーを使用して、構成を 64 ビットに設定します。 詳細については、[プロジェクトを構成して対象プラットフォームを設定する](../ide/how-to-configure-projects-to-target-platforms.md)

3. この時点で、64 ビット バージョンのリモート デバッガー (msvsmon.exe) が起動します。 64 ビット構成のソリューションが開いている限り、これが実行されます。

4. デバッグを開始します。 操作は 32 ビット構成と変わりません。 エラーが発生した場合は、以下のトラブルシューティング セクションをご覧ください。

## <a name="troubleshooting-64-bit-debugging"></a>トラブルシューティング (64 ビット デバッグ)
 次のようなエラーが表示されることがあります。"64 ビット デバッグ操作に予想以上に時間がかかっています。" この場合、Visual Studio は 64 ビット バージョンの msvsmon.exe に要求を送信し、その要求の結果が返されるまでに長い時間がかかっています。

 このエラーの主な原因として次の 2 つがあります。

- ネットワーク スタックの信頼性を低下させるネットワーク セキュリティ ソフトウェアがコンピューターにインストールされており、localhost に向かうパケットがドロップされています。 すべてのネットワーク セキュリティ ソフトウェアを無効にしてみて、問題が解決するか確認します。 解決した場合は、ネットワーク セキュリティ ソフトウェア ベンダーに、ソフトウェアが localhost トラフィックに干渉していることを報告します。

- Visual Studio でハングまたはパフォーマンスに関する問題が発生しています。 問題が定期的に発生する場合は、Visual Studio (devenv.exe) とワーカー プロセス (msvsmon.exe) のダンプを収集して、Microsoft に送信できます。 問題の報告については、「 [How to Report a Problem with Visual Studio](../ide/how-to-report-a-problem-with-visual-studio.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [64 ビット アプリケーション](/dotnet/framework/64-bit-apps)
- [64 ビット用プログラムの構成](/cpp/build/configuring-programs-for-64-bit-visual-cpp)
- [Visual Studio IDE の 64 ビット サポート](../ide/visual-studio-ide-64-bit-support.md)
- [ダンプ ファイルの使用](../debugger/using-dump-files.md)
- [Remote Debugging](../debugger/remote-debugging.md)