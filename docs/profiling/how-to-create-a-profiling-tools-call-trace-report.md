---
title: プロファイル ツールのコール トレース レポートを作成する | Microsoft Docs
description: パフォーマンス ツールのコール トレース レポートを作成し、お使いの関数およびお使いの関数の関数呼び出しのタイミング情報を参照できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, viewing ETW data
- ETW [Visual Studio ALM], viewing data
ms.assetid: 7640520a-7d3c-456c-b184-872a5d2f82f3
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 12d294202c3cea2c19f4f88ca4e7bd1dfd62df67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860829"
---
# <a name="how-to-create-a-profiling-tools-call-trace-report"></a>方法: プロファイリング ツールのコール トレース レポートを作成する
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールの *コール トレース レポート* は、アプリケーションの関数に対する各エントリ ポイントと終了ポイント、および実行中の関数から他の関数に対する各呼び出しのタイミング情報を一覧表示します。 コール トレース レポートをデータのプロファイリングに使用できるのは、インストルメンテーション メソッドで収集された場合だけです。

> [!NOTE]
> コール トレース レポートを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で表示することはできません。 コンマ区切り値 (.*csv*) ファイルまたは .*xml* ファイルを生成するには、**VSPerfReport** のコマンド ライン ツールを使用する必要があります。 このツールの詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。

### <a name="to-create-a-call-trace-report"></a>コール トレース レポートを作成するには

1. **コマンド プロンプト** ウィンドウを開きます。

2. コマンド プロンプトに次のコマンドを入力します。

     *ToolsPath* **VSPerfReport** *VSPFile*  **/CallTrace [/Xml]**

    |アイテム|説明|
    |-|-|
    |*ToolsPath*|プロファイル ツールのコマンド ライン ツールのパス。 詳細については、「[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)」をご覧ください。|
    |*VSPFile*|プロファイル データ (.*vsp* または .*vsps*) ファイル。 完全パスまたは部分パスで指定できます。|
    |Xml|XML 形式のレポートを生成します。|

## <a name="see-also"></a>関連項目
- [方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)
- [プロファイル ツールの API](../profiling/profiling-tools-apis.md)
