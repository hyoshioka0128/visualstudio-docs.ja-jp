---
title: Shutdown | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a1e37500-4ad1-4670-9737-3d9a20536386
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 89a08808387067b934bfd826feb2dcfbcf949aab
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778285"
---
# <a name="shutdown"></a>シャットダウン
**Shutdown** オプションは、現在プロファイル中のプロセスが終了するかデタッチされるまで待機して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **Shutdown** オプションは、プロファイル実行の最後のコマンドである必要があります。

 タイムアウト パラメーターが指定されていない場合、**Shutdown** オプションは無期限に待機します。 タイムアウト パラメーターが指定されている場合、指定された秒数の経過後にオプションから制御が戻りますが、プロファイラーはオフにされず、データ ファイルも閉じられません。

 コマンド ラインで指定するオプションは **Shutdown** オプションのみにする必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Shutdown[:Timeout]
```

#### <a name="parameters"></a>パラメーター
`Timeout`
- (省略可能) 指定した場合は、指定した秒数の経過後にオプションから制御が戻りますが、プロファイラーはオフにされず、プロファイル データ ファイルも閉じられません。

## <a name="see-also"></a>参照
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
