---
title: Detach | Microsoft Docs
description: VSPerfCmd.exe の Detach オプションを使用すると、指定したプロセスから、または何も指定しない場合はすべてのプロセスから、プロファイラーが切断されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: d9d1b52c-7f28-467d-b1e0-512afc4e46c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 45225e4478b0a1a3cddc7f74ae223c437bf4226e
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686598"
---
# <a name="detach"></a>Detach
VSPerfCmd.exe **Detach** オプションは、何も指定されていない場合、プロファイラーを指定のプロセスまたはすべてのプロセスから切断します。 サンプリング方法を利用し、プロファイリングを初期化しておく必要があります。

 **Launch** オプションまたは **Attach** オプションを指定して開始したプロファイリングは、**Detach** で切断できます。 その後、**Attach** コマンドを使用すればプロファイラーを再接続できます。

 **Detach** では、プロファイリング データ ファイルは閉じられません。 プロファイリングを終了し、データ ファイルを閉じるには、**Shutdown** オプションを使用します。

> [!NOTE]
> **Start** オプションを **Crosssession** オプションと共に指定した場合、**VSPerfCmd /Attach** または **VSPerfCmd /Detach** を呼び出すには **Crosssession** も指定する必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Detach[:PIDs|ProcessNames]
```

#### <a name="parameters"></a>パラメーター
 `PIDs|ProcessNames` `PID` - 1 つまたは複数のプロセスの数字のシステム識別子。

 `ProcessNames` - プロセスの名前。 名前付きプロセスの複数のインスタンスが実行されている場合、結果は予想できません。

 複数のプロセスを指定するときは、コンマで区切ります。

 プロセスが指定されていない場合、プロファイリングされているすべてのプロセスからプロファイラーが切断されます。

## <a name="valid-options"></a>有効なオプション
 **Attach** オプションと組み合わせて単一コマンド ラインで指定できる **VSPerfCmd** オプションを以下に示します。

 **Crosssession** ログオン セッション以外のセッションでプロファイリング アプリケーションを有効にします。 **Start** オプションが **Crosssession** オプションと共に指定された場合、必須です。

## <a name="example"></a>例
 この例では、**Detach** コマンドはプロファイリングを一時停止します。**Shutdown** コマンドはプロファイラー データ ファイルを閉じます。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
;REM Excercise the application
VSPerfCmd.exe /Detach
VSPerfCmd.exe /Shutdown
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
