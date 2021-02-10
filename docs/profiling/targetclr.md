---
title: TargetCLR | Microsoft Docs
description: アプリケーションに複数のバージョンの共通言語ランタイムが読み込まれている場合に、TargetCLR オプションを使用してプロファイリングを行う CLR のバージョンを指定する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f9732480-287f-40f1-a4ff-b112e143b940
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 76454a77a895a44d4c6871ad5061ee4b6079e604
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99868193"
---
# <a name="targetclr"></a>TargetCLR
**TargetCLR** オプションでは、アプリケーションに複数のバージョンの CLR (共通言語ランタイム) が読み込まれている場合に、プロファイリングを行う CLR のバージョンを指定します。

 既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールはアプリケーションによって読み込まれる最初の CLR のバージョンを対象とします。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe {/Launch:AppName | /Attach:PID} /TargetCLR[:ClrVersion] [Options]
```

#### <a name="parameters"></a>パラメーター
 `ClrVersion` CLR のバージョン番号。 **vN.N.NNNNN** のバージョン形式を使用します。

## <a name="required-options"></a>必須オプション
 **TargetCLR** オプションは、**Launch** オプションまたは **Attach** オプションと共に指定する場合にのみ使用できます。

 **Launch:** `AppName` 指定したアプリケーションを起動し、プロファイリングを開始します。

 **Attach:** `PID` 指定したプロセスのプロファイリングを開始します。

## <a name="example"></a>例
 この例では、TargetCLR オプションを使用して、CLR バージョン 4.0.11003 がプロファイリングされることを確認します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /TargetCLR:v4.0.11003
```
