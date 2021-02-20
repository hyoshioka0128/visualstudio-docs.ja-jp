---
title: 命令ポインター (IP) ビュー - サンプリング データ | Microsoft Docs
description: サンプリング データの IP ビューには、プロファイルを実行してサンプルを収集したときに直接実行したアセンブリ命令のパフォーマンス データが一覧表示されます。そのしくみについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: c7f647bb-c5a3-4708-9f9d-33c0fd6e2e96
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ee8ae3082dc4dd19bb67c9374766b0d8f702fc9b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906821"
---
# <a name="instruction-pointers-ips-view---sampling-data"></a>命令ポインター (IP) ビュー - サンプリング データ
サンプリング データの IP ビューには、プロファイルを実行してサンプルを収集したときに直接実行したアセンブリ命令のパフォーマンス データが一覧表示されます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

|列|説明|
|------------|-----------------|
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|
|**プロセス名**|プロセスの名前です。|
|**モジュール名**|命令を含むモジュールの名前。|
|**モジュール パス**|命令を含むモジュールのパスです。|
|**[転送元ファイル]**|命令を含むソース ファイル。|
|**関数名**|命令を含む関数の名前。|
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|
|**関数アドレス**|読み込まれたバイナリ内の関数の開始メモリ アドレス。|
|**ソース開始行**|このサンプルが収集されたソース ファイル内の開始行番号です。|
|**ソース終了行**|このサンプルが収集されたソース ファイル内の終了行番号です。|
|**ソース開始文字番号**|このサンプルが収集されたソース ファイル行内の開始文字のオフセットです。|
|**ソース終了文字番号**|このサンプルが収集されたソース ファイル行内の終了文字のオフセットです。|
|**命令ポインター アドレス**|読み込まれたバイナリ内の命令のアドレスです。|
|**排他サンプル**|命令を実行していたときに収集されたサンプルの合計数です。|
|**サンプル % (関数のみ)**|命令を実行していたときに収集された、プロファイル実行内のすべてのサンプルの割合です。|

## <a name="see-also"></a>関連項目
- [命令ポインター (IP) ビュー - サンプリング](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)
