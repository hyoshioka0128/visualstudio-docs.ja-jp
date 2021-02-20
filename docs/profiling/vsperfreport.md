---
title: VSPerfReport | Microsoft Docs
description: VSPerfReport コマンドライン ツールを使用し、Visual Studio プロファイル ツールのプロファイル データ ファイルを使用してレポートを作成する方法について学習します。
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- command-line tools, VSPerfReporttool
- performance tools, VSPerfReport tool
- profiling tools,VSPerfReport
- VSPerfReport tool
- command line, tools
- instrumentation, VSPerfReporttool
ms.assetid: dbfd8d91-4430-4b82-81b9-97ac61412a6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 507ea5a90aa17ba252a95714f488f5ea22dff4f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911503"
---
# <a name="vsperfreport"></a>VSPerfReport
VSPerfReport コマンド ライン ツールは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのプロファイル データ ファイルを使用してレポートを作成するために使用されます。 既定のレポート形式は .*csv* ファイルです。

 VSPerfReport では次の構文が使用されます。

```cmd
VSPerfReport [/U] vspfilename [/options]
```

 `filename` は有効な .*vsp* ファイルまたは .*vsps* ファイルである必要があることに注意してください。

 .*vsp* ファイルまたは .*vsps* ファイルの比較には、VSPerfReport コマンド ライン ツールも使用されます。 相違点 ("diff") レポートを生成するには、次の構文を使用します。

```cmd
VSPerfReport [/U] /diff vspfilename1 vspfilename2 [/options]
```

 `vspfilename1 and vspfilename2` は有効な .*vsp* ファイルまたは .*vsps* ファイルである必要があります。

## <a name="symbol-files"></a>シンボル ファイル
 関数名や行番号などのシンボル情報を表示するには、VSPerfReport が、プロファイルしたコンポーネントのシンボル (.pdb) ファイルおよび Windows シンボル ファイルにアクセスできる必要があります。 詳細については、「[方法:コマンド ラインからシンボル ファイルの場所を指定する](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)」を参照してください。

## <a name="general-report-options"></a>一般的なレポート オプション
 次の表では、一般的なレポートの書式指定オプションと、報告対象のデータを選択するためのオプションについて説明します。

|Options|説明|
|-------------|-----------------|
|**U**|レポート出力とリダイレクトされたコンソール出力は Unicode として書き込まれます。 このオプションは最初に指定する必要があります。|
|**Summary:**[*types*]|1 つ以上の種類のレポートを作成します。<br /><br /> -   `All` - すべての種類のレポートが生成されます。<br />-   `CallerCallee` - 関数間の親子関係。<br />-   `Function` - 呼び出された関数。<br />-   `CallTree` - 呼び出された関数の階層。<br />-   `Counter` - すべてのマークと Windows パフォーマンス カウンター値。<br />-   `Ip` - プロファイルされた命令。<br />-   `Life` - (割り当てデータが収集されたときに使用可能な) 割り当てられたオブジェクトの有効期間。<br />-   `Line` - ソース コード行のプロファイル データ。<br />-   `Header` - レポートにファイル ヘッダー情報が含まれます。<br />-   `Mark` - すべてのマーク。<br />-   `Module` - プロファイルされたモジュール。<br />-   `Process` - プロファイルされたプロセス。<br />-   `Thread` - プロファイルされたスレッド。<br />-   `Type` - 割り当てられた型。<br />-   `Contention` - リソースの競合。<br />-   `RuleWarnings` - パフォーマンス規則の問題<br />-   `ETW` - プロファイル実行で収集されたすべての Windows イベント トレーシング (ETW) イベント。 .etl データ ファイルは、その元の場所か、.vsp または .vsps ファイルを含むディレクトリにある必要があります。|
|**Xml**|レポートを XML 形式で出力します。|
|**CallTrace**|関数の開始と終了、ETW イベント、およびマークのリストを作成します。|
|**ClearPackedSymbols**|プロファイラー データ ファイルから以前に埋め込まれたシンボルを削除します。 PackSymbols を 2 回目に実行する前にこのコマンドを実行します。|
|**SymbolPath:** `path`|プロファイラー データ ファイルのシンボルを含む 1 つ以上の検索パスまたはシンボル サーバーを指定します。|
|**DebugSymPath**|シンボルが検索された場所、およびシンボルが見つかったかどうかを示します。 このオプションは、シンボル解決の問題を解決するのに便利です。|
|**PackSymbols**|シンボルをプロファイル データ (.vsp) ファイルに保存して、シンボル (.*pdb*) ファイルが分析に不要になるようにします。|
|**Output:** *path*&#124;*filename*|生成されたレポート ファイルの代替の場所を指定します。 既定では、レポートは現在のディレクトリに作成されます。|
|**SummaryFile**|分析を行い、分析情報を .vsps 概要ファイルに保存します。|
|**PrintMarks**|指定されたレポート ファイル内のすべてのマークについて、名前とタイムスタンプを表示します。|
|**?**|使用情報を表示します。|
|**NoLogo**|レポートの実行時にバージョン情報を非表示にします。|
|**UserRulesDirectory**|ユーザー定義のパフォーマンス規則を含むディレクトリを指定します (まだ実装されていません)。|

## <a name="filter-options"></a>フィルター オプション
 次の表では、使用できるデータをフィルター処理するためのオプションについて説明します。

|Options|説明|
|-------------|-----------------|
|**JustMyCode**[ **:** [`caller`][,`callee`]]|ユーザー アプリケーションの関数呼び出しのみを表示し、システム呼び出しは非表示にします。<br /><br /> -   パラメーターなし - すべてのシステム関数を非表示にします。<br />-   `caller` - アプリケーション関数を呼び出すシステム関数の 1 つのレベルを表示します。<br />-   `callee` - ユーザー アプリケーション関数で呼び出されるシステム関数の 1 つのレベルを表示します。|
|**StartTime:** [*value*]|ミリ秒単位の時間 (value) よりも後に収集されたデータのみを表示します。|
|**EndTime:** [*value*]|ミリ秒単位の時間 (value) よりも前に収集されたデータのみを表示します。|
|**FilterFile:** `VSPFFile`|Visual Studio の [パフォーマンス レポート] ウィンドウから生成されたフィルター ファイルの場所を指定します。|
|**MsFilter:** [*starttime,duration*]|開始時刻 (`starttime`) からミリ秒単位の時間 (`duration`) 内のみのデータを表示します。|
|**Process:** [*pid*]|指定されたプロセスのデータのみを表示します。|
|**Thread:** [*threadid*]|指定されたスレッドのデータのみを表示します。|
|**Thread:** [*threadid,processid*]|指定されたプロセスに関連付けられている指定されたスレッドのデータのみを表示します。|

## <a name="difference-report-options"></a>相違点レポートのオプション
 次の表では、レポート ファイルを比較するためのオプションについて説明します。

|Options|説明|
|-------------|-----------------|
|**[Diff]**  `vspfile1 vspfile2`|2 つレポート ファイル (.*vsp* または .*vsps*) を比較します。 diff オプションを使用すると Summary オプションは無視されます。|
|**Diff:**[*value*]|このしきい値を下回ると、2 つの値の相違は無視されます。 また、値がこのしきい値を下回る新しいデータは表示されません。|
|**DiffTable:**[*tablename*]|このテーブルを使用して、ファイルを比較します。 既定では関数テーブルが使用されます。|
|**DiffColumn:**[*columnname*]|この列を使用して、値を比較します。 既定では排他サンプルのパーセント列が使用されます。|
|**QueryDiffTables**|指定された 2 つのレポート ファイルに関する有効なテーブルおよび列をリストします。|

## <a name="see-also"></a>関連項目
- [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)
