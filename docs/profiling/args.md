---
title: Args | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 20c35949-1f29-4282-ac75-4e6c237d71bc
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3b6d01a95b7e0872d6bb36c6d9f3917bc6a05b3b
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779819"
---
# <a name="args"></a>Args
VSPerfCmd.exe **Args** オプションは、**Launch** サブコマンドの対象アプリケーションに渡される引数のリストを指定します。

 **Args** は、コマンド ラインで **Launch** も指定された場合にのみ使用できます。 **Args** は、**Launch** を指定した場合のオプションです。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Launch:AppName /Args:Arguments [Options]
```

#### <a name="parameters"></a>パラメーター
 `Arguments` **Launch** コマンドのターゲット アプリケーションへの引数のリスト。

## <a name="required-options"></a>必須オプション
 **Launch:** `AppName` 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。

## <a name="example"></a>例
 次の例では、**Args** オプションを使用して引数を TestApp.exe に渡します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /Args:"123, 'Hello World'"
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
