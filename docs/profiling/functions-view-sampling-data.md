---
title: 関数ビュー - サンプリング データ | Microsoft Docs
description: プロファイリング実行中にサンプリングされた関数が一覧表示される、サンプリング プロファイル方式の関数レポート ビューについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method,Functions View
- Functions view
ms.assetid: 029d5ebb-e551-46b0-b64e-2c553d9dbb8e
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 82b48689b6348c7d003f5418224260b7939e907a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907355"
---
# <a name="functions-view---sampling-data"></a>関数ビュー - サンプリング データ
サンプリング プロファイル方式の関数のレポート ビューには、プロファイリング実行中にサンプリングされた関数が一覧表示されます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

|列|説明|
|------------|-----------------|
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|
|**プロセス名**|プロセスの名前です。|
|**モジュール名**|関数を含むモジュールの名前です。|
|**モジュール パス**|関数を含むモジュールのパスです。|
|**[転送元ファイル]**|この関数の定義を含むソース ファイルです。|
|**関数名**|関数の完全修飾名です。|
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|
|**関数アドレス**|関数のアドレス。|
|**サンプル数 (子を含む)**|この関数が実行されたときに収集されたサンプルの合計数。つまり、この関数が呼び出し履歴上にあったときに収集されたサンプルの数。 この数には、その関数によって呼び出された関数の実行中に収集されたサンプルが含まれます。|
|**包括サンプル %**|プロファイル実行のすべてのサンプルに対する、この関数の包括サンプルの割合。|
|**排他サンプル**|この関数の本文内のコードが実行されたとき、つまり、この関数が呼び出し履歴の一番上にあったときに収集されたサンプルの合計数。 この関数によって呼び出された関数で収集されたサンプルは含まれません。|
|**サンプル % (関数のみ)**|プロファイル実行のすべてのサンプルに対する、この関数の排他サンプルの割合。|

## <a name="see-also"></a>関連項目
- [方法: レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)
- [関数ビュー - インストルメンテーション](../profiling/functions-view-dotnet-memory-instrumentation-data.md)
- [関数ビュー - サンプリング](../profiling/functions-view-dotnet-memory-sampling-data.md)
- [関数 ビュー](../profiling/functions-view-instrumentation-data.md)
