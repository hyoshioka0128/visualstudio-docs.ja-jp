---
title: Sys (VSPerfCmd) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 294a6f9e-b49f-4c83-b322-5ac5411b66fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 435393ac536eb70f2f3f6d38b16eaab645848704
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778181"
---
# <a name="sys-vsperfcmd"></a>Sys (VSPerfCmd)
*VSPerfCmd.exe* の **Sys** オプションは、システム呼び出しイベント (プロファイリングされたアプリケーションからオペレーティング システムへの関数呼び出し) にサンプリングされるプロファイリング イベントを設定し、必要に応じて、サンプリング間隔のシステム呼び出し数を既定値の 10 から変更します。

 **Sys** は、**Launch** オプションまたは **Attach** オプションも含むコマンド ラインでのみ使用できます。

 既定では、プロファイラーのサンプリング イベントは、プロセッサのクロック サイクルに設定され、サンプリング間隔は 10,000,000 に設定されます。 **Timer**、**PF**、**Sys**、**Counter** の各オプションを使用すると、サンプリング イベントおよびサンプリング間隔を設定できます。 **GC** オプションは、割り当ておよびガベージ コレクション イベントが発生するたびに、.NET メモリ データを収集します。 コマンド ラインには、上記のオプションのいずれか 1 つだけを指定できます。

 サンプリング イベントおよびサンプリング間隔は、**Launch** オプションまたは **Attach** オプションを含む最初のコマンド ラインでのみ設定できます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe {/Launch:AppName|Attach:PID} /Sys[:Events] [Options]
```

#### <a name="parameters"></a>パラメーター
 `Events` サンプリング間隔におけるシステム呼び出しイベント数を指定する整数値。 ‎`Events` が指定されていない場合、間隔は 10 に設定されます。

## <a name="required-options"></a>必須オプション
 **Sys** には、次のオプションのいずれかが必要です。

 **Launch:** `AppName` プロファイラーと、`AppName` で指定されたアプリケーションを起動します。

 **Attach:** `PID` プロファイラーを `PID` で指定されたプロセスにアタッチします。

## <a name="invalid-options"></a>無効なオプション
 以下のオプションは、**Sys** と同じコマンド ラインには指定できません。

 **PF**[ **:** `Events`] サンプリング イベントをページ フォールトに設定します。オプションで、サンプリング間隔を `Events` に設定します。 既定の PF 間隔は 10 です。

 **Timer**[ **:** `Cycles`] サンプリング イベントをプロセッサのクロック サイクルに設定し、必要に応じてサンプリング間隔を `Cycles` に設定します。 既定の Timer 間隔は 10,000,000 です。

 **Counter:** `Name`[`,Reload`[`,FriendlyName`]] サンプリング イベントを、`Name` で指定された CPU パフォーマンス カウンターに設定し、サプリング間隔を `Reload` に設定します。

 **GC**[ **:** {**Allocation**&#124;**Lifetime**}] .NET メモリ データを収集します。 既定 (**Allocation**) では、データはメモリの割り当てイベントごとに収集されます。 **Lifetime** パラメーターが指定されている場合、ガベージ コレクション イベントごとのデータも収集されます。

## <a name="example"></a>例
 この例では、プロファイラーのサンプリング イベントをシステム呼び出しに設定し、サンプリング間隔をサンプルごとに 20 の呼び出しに設定する方法を示します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /Sys:20
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
