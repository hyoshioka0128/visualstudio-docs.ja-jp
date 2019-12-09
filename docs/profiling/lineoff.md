---
title: LineOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 76082063-20ef-47ae-ad64-81b43b654865
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ac671c3b0ba40c462403b2afa850c3936156d6d2
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74774127"
---
# <a name="lineoff"></a>LineOff
既定では、サンプリング プロファイル方法を使用するときに、プロファイラーがソース コードの行番号と行番号オフセットのデータを収集します。 VSPerfCmd **LineOff** オプションを指定すると、VSPerfCmd を使用してアプリケーションを起動するときに、行番号データの収集が無効になります。 **LineOff** が指定されている場合、プロファイル データは関数レベルで収集されます。

 **LineOff** は、**Start**:**Sample** オプションを使用してサンプリングするようにプロファイラーが初期化されている場合にのみ、**Launch** オプションと共にのみ使用できます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Launch:AppName /LineOff [Options]
```

#### <a name="parameters"></a>パラメーター
 なし

## <a name="required-options"></a>必須オプション
 **LineOff** オプションは、**Launch** オプションを含むコマンド ラインでのみ使用できます。

 **Launch:** `AppName` 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。

## <a name="example"></a>例
 この例ではアプリケーションとプロファイラーを起動し、行レベルのサンプリングを無効にします。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /LineOff
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
