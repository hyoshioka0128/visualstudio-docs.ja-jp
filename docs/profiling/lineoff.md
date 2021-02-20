---
title: LineOff | Microsoft Docs
description: VSPerfCmd LineOff オプションを指定すると、VSPerfCmd を使用してアプリケーションを起動するときに、行番号データの収集が無効になります。そのしくみについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 76082063-20ef-47ae-ad64-81b43b654865
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a141e713dd03f99db6ce47224c64236a0219cdd5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917897"
---
# <a name="lineoff"></a>LineOff
既定では、サンプリング プロファイル方法を使用するときに、プロファイラーがソース コードの行番号と行番号オフセットのデータを収集します。 VSPerfCmd **LineOff** オプションを指定すると、VSPerfCmd を使用してアプリケーションを起動するときに、行番号データの収集が無効になります。 **LineOff** が指定されている場合、プロファイル データは関数レベルで収集されます。

 **LineOff** は、**Start**:**Sample** オプションを使用してサンプリングするようにプロファイラーが初期化されている場合にのみ、**Launch** オプションと共にのみ使用できます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Launch:AppName /LineOff [Options]
```

#### <a name="parameters"></a>パラメーター
 None

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
