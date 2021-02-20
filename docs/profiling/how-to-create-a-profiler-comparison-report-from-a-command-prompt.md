---
title: プロファイラー比較レポートを作成する (コマンド ライン)
description: コマンドラインから VSPerfReport を使用して、2 つのプロファイラー データ ファイルの結果を比較できます。 この比較では、プロファイル セッション間の違いが示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 00548d16-eb5b-46f7-8a65-862f98a43831
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 38303a091838fae6fdc86ab91eb1ee95dfb429ca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911699"
---
# <a name="how-to-create-a-profiler-comparison-report-from-a-command-prompt"></a>方法: コマンド プロンプトからプロファイラー比較レポートを作成する
2 つのプロファイリング データ (.*vsp* または .*vsps*) ファイルのパフォーマンス データを比較する [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツール レポートを生成できます。 このレポートでは、プロファイリング セッションを比較し、その違い、パフォーマンスの低下、改善を示します。 レポート内の値は、指定された最初のファイルを基準とし、差分 (変化分) を表します。 この差分は、古い値、基準値と、新しい分析による結果の値との違いを測定して計算されます。 プロファイラーのデータの比較は、コード内の関数、アプリケーション内のモジュール、行、命令ポインター (IP)、および種類に基づいて作成できます。

 比較のカテゴリとフィールドの識別子を一覧表示するには、次のコマンド ラインを入力します。

 **VSPerfReport /querydifftables**  *VspFileName1* *VspFileName2*

 比較レポートを作成するには、次の構文を使用します。

 **VSPerfReport /diff**  `VspFileName1` *VspFileName2* [ **/** `Options`]

 次の表のオプションを **VSPerfReport /diff** コマンド ラインに追加できます。

|オプション|説明|
|------------|-----------------|
|**DiffThreshold:** [*Value*]|このパーセンテージしきい値を下回る場合、差異を無視します。 また、このしきい値を下回る新しいデータは表示されません。|
|**DiffTable:** *TableName*|このテーブルを使用してファイルを比較します。 既定では、関数テーブルが使用されます。 **VSPerfReport /querydifftables** の一覧にある識別子を指定します。|
|**DiffColumn:** *ColumnName*|この列を使用して値を比較します。 既定では、排他サンプルのパーセント列が使用されます。 **VSPerfReport /querydifftables** の一覧にある識別子を指定します。|
