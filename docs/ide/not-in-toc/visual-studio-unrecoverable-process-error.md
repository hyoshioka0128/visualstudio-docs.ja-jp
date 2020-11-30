---
title: プロセスで回復不能なエラーが発生しました
description: Visual Studio の通常の操作中に回復不能なエラーが発生する可能性があるプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 09/10/2020
ms.topic: troubleshooting
helpviewer_keywords:
- unrecoverable error
- error, process
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e44f96e0a8056a369b164e725aca6832b5a349cb
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95871484"
---
# <a name="visual-studio-unrecoverable-process-error"></a>Visual Studio の回復不能なプロセス エラー

Visual Studio では、アウト プロセスのプロセスをいくつか利用し、ライブ単体テストやコード アナライザーなど、必要なバックグラウンド タスクを実行します。 このようなプロセスはアウト プロセスで実行され、Visual Studio のパフォーマンスを改善します。たとえば、リソースを集中的に使用するジョブを長時間実行するとき、Visual Studio の応答が速くなります。 また、Visual Studio は 32 ビット プロセスのため、プロセスをアウト プロセスで実行すると、メモリを集中的に使用する作業にたくさんのメモリ領域が与えられます。

*ServiceHub.RoslynCodeAnalysisService.exe* または *ServiceHub.RoslynCodeAnalysisService32.exe* プロセスが何らかの理由で終了すると、ポップアップ情報バーが現れ、次のメッセージが表示されます。

**"Unfortunately, a process used by Visual Studio has encountered an unrecoverable error.We recommend saving your work, and then closing and restarting Visual Studio. (申し訳ございませんが、Visual Studio で使用されているプロセスに回復できないエラーが発生しました。作業を保存し、Visual Studio を再起動することをお勧めします。)"**

このメッセージが表示されたら、作業を保存し、Visual Studio を閉じ、再起動してください。

## <a name="list-of-processes"></a>プロセスの一覧

次は、Visual Studio で使用されるアウト プロセス プロセスの一覧です。 この一覧には、特定のワークフローまたはシナリオで起動するプロセスが含まれているため、多くの場合、これらすべてが同時に実行されることはありません。

- Microsoft.Alm.Shared.Remoting.RemoteContainer.dll
- Microsoft.CodeAnalysis.LiveUnitTesting.EntryPoint
- MSBuild.exe
- PerfWatson2.exe
- ScriptedSandbox64.exe
- ServiceHub.Host.CLR.x86.exe
- ServiceHub.Host.Node.x86.exe
- ServiceHub.IdentityHost.exe
- ServiceHub.RoslynCodeAnalysisService.exe
- ServiceHub.RoslynCodeAnalysisService32.exe
- ServiceHub.SettingsHost.exe
- ServiceHub.VSDetouredHost.exe
- VBCSCompiler.exe
- VsHub.exe
- vstest.discoveryengine.x86.exe
- WaAppAgent.exe
- WindowsAzureGuestAgent.exe
- WindowsAzureTelemetryService.exe

これらのプロセスのいずれかが突然終了した場合、Visual Studio 内の一部の機能が停止します。 機能の損失がそれほど重要でないプロセスもありますが、 それ以外のプロセスは、Visual Studio の安定性に影響を及ぼし、エラー メッセージが表示されます。

> [!NOTE]
> このページで言及されていない問題に遭遇した場合、[[問題の報告]](../../ide/how-to-report-a-problem-with-visual-studio.md) ツールでご報告ください。このツールは、Visual Studio インストーラーと Visual Studio IDE の両方に表示されます。
