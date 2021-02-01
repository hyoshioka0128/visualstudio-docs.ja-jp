---
title: QueryCounters | Microsoft Docs
description: QueryCounters オプションを使用して、コンピューターに対して使用できる CPU (ハードウェア) パフォーマンス カウンターを一覧表示する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8059d4b2-af61-4a47-a6c2-8da5c0741c74
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d33b6fe42f786218bf78825a356a25edff2b31ae
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720437"
---
# <a name="querycounters"></a>QueryCounters
**QueryCounters** オプションは、コンピューターで使用可能な CPU (ハードウェア) パフォーマンス カウンターをリストします。

 **QueryCounters** は、コマンド ラインで唯一のオプションである必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /QueryCounters
```

#### <a name="parameters"></a>パラメーター
 なし

## <a name="remarks"></a>解説
 インストルメンテーション メソッドを使用している場合、プロファイラーは各データ コレクション イベントで 1 つ以上の CPU パフォーマンス カウンターの値を収集できます。 サンプリング プロファイル方法を使用している場合、1 つのカウンター イベントとサンプリング間隔として使用されるイベント出現回数を指定できます。

 プロセッサごとに異なる CPU パフォーマンス カウンターが公開されます。 プロファイラーは、ほぼすべてのプロセッサで使用できる一連の汎用カウンターを定義します。 **QueryCounters** オプションでは、汎用カウンター名と、プロセッサに固有のカウンター名の両方をリストします。

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
