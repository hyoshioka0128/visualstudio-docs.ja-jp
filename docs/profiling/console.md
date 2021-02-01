---
title: コンソール | Microsoft Docs
description: VSPerfCmd.exe の Console オプションを使用し、新しいコマンド プロンプト ウィンドウで指定のアプリケーションを開始します。 Launch オプションと共に使用する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e825ba66-1383-46ad-8712-396bc9c14036
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 93c39bfb503bec9858e33b7acf04e0f0433264b9
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720906"
---
# <a name="console"></a>コンソール
VSPerfCmd.exe で **Console** オプションを指定すると、新しいコマンド プロンプト ウィンドウで指定のアプリケーションが開始します。 **Console** オプションは、VSPerfCmd の **Launch** オプションとの併用でのみ使用できます。 アプリケーションがコマンドライン アプリケーションではない場合、**Console** を指定しても何も起こりません。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Launch:AppName /Console
```

#### <a name="parameters"></a>パラメーター
 None

## <a name="required-options"></a>必須オプション
 **Console** オプションは、**Launch** オプションも含むコマンド ラインでのみ指定できます。

 **Launch:** `AppName` プロファイラーと、`AppName` で指定されたアプリケーションを起動します。

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
