---
title: Args | Microsoft Docs
description: VSPerfCmd.exe の ARGS オプションを使用し、Launch サブコマンドの対象アプリケーションに引数リストを渡します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 20c35949-1f29-4282-ac75-4e6c237d71bc
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 44e68822ebd444b8683b85b2df0c49b14d78bcaa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901070"
---
# <a name="args"></a>Args
VSPerfCmd.exe **Args** オプションは、**Launch** サブコマンドの対象アプリケーションに渡される引数のリストを指定します。

 **Args** は、コマンド ラインで **Launch** も指定された場合にのみ使用できます。 **Args** は、**Launch** を指定した場合のオプションです。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Launch:AppName /Args:Arguments [Options]
```

#### <a name="parameters"></a>パラメーター
 `Arguments`**Launch** コマンドのターゲット アプリケーションへの引数のリスト。

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
