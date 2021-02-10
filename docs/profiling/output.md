---
title: Output | Microsoft Docs
description: Output オプションを使用して、パフォーマンス セッションにプロファイル データ ファイルの名前を指定する方法について学習します。 Output は Start オプションと共に使用する必要があります。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5e286e61-4548-42cf-a635-e608c5edbe2b
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: de3edb5e9b9c04b53d6b669828020c0999d218e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922403"
---
# <a name="output"></a>出力
**Output** オプションでは、パフォーマンス セッションのプロファイル データ ファイルの名前を指定します。 **Output** は **Start** オプションと共に使用する必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName [Options]
```

#### <a name="parameters"></a>パラメーター
 `FileName` データ ファイルの名前。 完全パスまたは部分パスで指定できます。 パスが指定されていない場合、ファイルは現在のディレクトリに作成されます。

## <a name="required-options"></a>必須オプション
 **Output** オプションは、**Start** オプションと共に使用する必要があります。

 **Start:** `Method` 出力ファイル名を指定します。

## <a name="example"></a>例
 次の例では、現在のディレクトリにプロファイル データ ファイルが作成されます。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
