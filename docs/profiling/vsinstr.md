---
title: VSInstr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- performance tools, instrumentation
- instrumentation, VSInstr tool
- profiling tools,VSInstr
- command-line tools, instrumentation
- command line, tools
- VSInstr
- VSInstr tool
- performance tools, VSInstr tool
ms.assetid: 7b1334f7-f9b0-4a82-a145-d0607bfa8467
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fc68ad7da06a1710e3c34ddb601155fc3d0b1182
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330509"
---
# <a name="vsinstr"></a>VSInstr
VSInstr ツールは、バイナリをインストルメント化するために使用します。 VSInstr ツールは、次の構文を使用して起動します。

```cmd
VSInstr [/U] filename [/options]
```

 VSInstr ツールのオプションの説明を次の表に示します。

|オプション|説明|
|-------------|-----------------|
|**Help** または **?**|ヘルプを表示します。|
|**U**|リダイレクトされたコンソール出力を Unicode で書き込みます。 これは、最初に指定する必要があるオプションです。|
|`@filename`|1 行につき 1 つのコマンド オプションを含む応答ファイルの名前を指定します。  引用符は使用しないでください。|
|**OutputPath** `:path`|インストルメント化されたイメージの保存先ディレクトリを指定します。 出力パスを指定しなかった場合、元のバイナリは同じディレクトリ内で "Orig" という文字列を付け加えたファイル名に変更され、バイナリのコピーがインストルメント化されます。|
|**Exclude:** `funcspec`|プローブによるインストルメンテーションから除外する関数の仕様を指定します。 このオプションは、関数へのプロファイリング プローブの挿入によって予測不可能な結果や好ましくない結果が引き起こされる場合に便利です。<br /><br /> 同じバイナリ内の関数を参照する **Exclude** オプションと **Include** オプションは併用しないでください。<br /><br /> 別個の **Exclude** オプションを使用して複数の関数の仕様を指定できます。<br /><br /> `funcspec` は次のように定義されます。<br /><br /> [namespace\<separator1>] [class\<separator2>]function<br /><br /> \<separator1> はネイティブ コードの場合は `::`、マネージド コードの場合は `.` です。<br /><br /> \<separator2> は常に `::` です<br /><br /> **Exclude** は、コード カバレッジでサポートされています。<br /><br /> ワイルドカード文字 \* がサポートされています。 たとえば、名前空間のすべての関数を除外するには、次を使用します。<br /><br /> MyNamespace::\*<br /><br /> **VSInstr /DumpFuncs** を使用して、指定したバイナリ内の関数の完全な名前を一覧表示できます。|
|**Include:** `funcspec`|プローブでインストルメント化するバイナリ内の関数の仕様を指定します。 バイナリ内の他のすべての関数はインストルメント化されません。<br /><br /> 別個の **Include** オプションを使用して複数の関数の仕様を指定できます。<br /><br /> 同じバイナリ内の関数を参照する **Include** オプションと **Exclude** オプションは併用しないでください。<br /><br /> **Include** は、コード カバレッジでサポートされていません。<br /><br /> `funcspec` は次のように定義されます。<br /><br /> [namespace\<separator1>] [class\<separator2>]function<br /><br /> \<separator1> はネイティブ コードの場合は `::`、マネージド コードの場合は `.` です。<br /><br /> \<separator2> は常に `::` です<br /><br /> ワイルドカード文字 \* がサポートされています。 たとえば、名前空間のすべての関数を含めるには、次を使用します。<br /><br /> MyNamespace::\*<br /><br /> **VSInstr /DumpFuncs** を使用して、指定したバイナリ内の関数の完全な名前を一覧表示できます。|
|**DumpFuncs**|指定したイメージ内の関数を一覧表示します。 インストルメンテーションは実行されません。|
|**ExcludeSmallFuncs**|小規模関数 (関数呼び出しを行わない短い関数) をインストルメンテーションから除外します。 **ExcludeSmallFuncs** オプションを指定すると、インストルメンテーション オーバーヘッドが軽減されてインストルメンテーションの速度が向上します。<br /><br /> 小規模関数を除外すると、.*vsp* ファイルのサイズが小さくなり、解析に要する時間も短くなります。|
|**Mark:** {**Before**\|**After**\|**Top**\|**Bottom**}`,funcname,markid`|.vsp レポート ファイル内のデータ範囲の先頭または末尾を識別するために使用できるプロファイル マーク (レポート内のデータを区切るために使用する識別子) を挿入します。<br /><br /> **Before** - 対象の関数に入る直前。<br /><br /> **After** - 対象の関数が終了した直後。<br /><br /> **Top** - 対象の関数に入った直後。<br /><br /> **Bottom** - 対象の関数の各復帰の直前。<br /><br /> `funcname` - 対象の関数の名前<br /><br /> `Markid` - プロファイル マークの識別子として使用する正の整数 (long)。|
|**Coverage**|カバレッジ インストルメンテーションを実行します。 これは、**Verbose**、**OutputPath**、**Exclude** および **Logfile** のオプションでのみ使用できます。|
|**Verbose**|**Verbose** オプションは、インストルメンテーション プロセスに関する詳細情報を表示するために使用します。|
|**NoWarn** `[:[Message Number[;Message Number]]]`|すべてまたは特定の警告を抑制します。<br /><br /> `Message Number` - 警告番号。 `Message Number` を省略した場合、すべての警告が抑制されます。<br /><br /> 詳細については、「[VSInstr の警告](../profiling/vsinstr-warnings.md)」を参照してください。|
|**Control:** `{` **Thread** \| **Process** \| **Global** `}`|次の VSInstr データ収集制御オプションのプロファイリング レベルを指定します。<br /><br /> **Start**<br /><br /> **StartOnly**<br /><br /> **Suspend**<br /><br /> **StopOnly**<br /><br /> **SuspendOnly**<br /><br /> **ResumeOnly**<br /><br /> **Thread** - スレッド レベルのデータ収集制御関数を指定します。 プロファイリングは、現在のスレッドに対してのみ開始または停止されます。 他のスレッドのプロファイリング状態は影響を受けません。 既定値は thread です。<br /><br /> **Process** - プロセス レベルのプロファイリング データ収集制御関数を指定します。 プロファイリングは、現在のプロセスのすべてのスレッドに対して開始または停止されます。 他のプロセスのプロファイリング状態は影響を受けません。<br /><br /> **Global** - グローバル レベル (プロセス間) のデータ収集制御関数を指定します。<br /><br /> プロファイリング レベルを指定しない場合は、エラーが発生します。|
|**Start:** `{` **Inside** \| **Outside** `},funcname`|データ収集を対象の関数とその関数から呼び出される子関数に制限します。<br /><br /> **Inside** - 対象の関数に入った直後に StartProfile 関数を挿入します。 対象の関数が戻るたびに、その直前に StopProfile 関数を挿入します。<br /><br /> **Outside** - 対象の関数を呼び出すたびに、その直前に StartProfile 関数を挿入します。 対象の関数を呼び出すたびに、その直後に StopProfile 関数を挿入します。<br /><br /> `funcname` - 対象の関数の名前。|
|**Suspend:**  `{` **Inside** \| **Outside** `},funcname`|対象の関数とその関数から呼び出される子関数に関するデータ収集を除外します。<br /><br /> **Inside** - 対象の関数に入った直後に SuspendProfile 関数を挿入します。 対象の関数が戻るたびに、その直前に ResumeProfile 関数を挿入します。<br /><br /> **Outside** - 対象の関数に入る直前に SuspendProfile 関数を挿入します。 対象の関数が終了した直後に ResumeProfile 関数を挿入します。<br /><br /> `funcname` - 対象の関数の名前。<br /><br /> 対象の関数に StartProfile 関数が含まれている場合は、その前に SuspendProfile 関数が挿入されます。 対象の関数に StopProfile 関数が含まれている場合は、その後に ResumeProfile 関数が挿入されます。|
|**StartOnly:** `{` **Before** \| **After** \| **Top** \| **Bottom** `},funcname`|プロファイリング実行中にデータ収集を開始します。 このオプションは、StartProfile API 関数を指定の位置に挿入します。<br /><br /> **Before** - 対象の関数に入る直前。<br /><br /> **After** - 対象の関数が終了した直後。<br /><br /> **Top** - 対象の関数に入った直後。<br /><br /> **Bottom** - 対象の関数の各復帰の直前。<br /><br /> `funcname` - 対象の関数の名前。|
|**StopOnly:** {**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|プロファイリング実行中にデータ収集を停止します。 このオプションは、StopProfile 関数を指定の位置に挿入します。<br /><br /> **Before** - 対象の関数に入る直前。<br /><br /> **After** - 対象の関数が終了した直後。<br /><br /> **Top** - 対象の関数に入った直後。<br /><br /> **Bottom** - 対象の関数の各復帰の直前。<br /><br /> `funcname` - 対象の関数の名前。|
|**SuspendOnly:** {**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|プロファイリング実行中にデータ収集を停止します。 このオプションは、SuspendProfile API を指定の位置に挿入します。<br /><br /> **Before** - 対象の関数に入る直前。<br /><br /> **After** - 対象の関数が終了した直後。<br /><br /> **Top** - 対象の関数に入った直後。<br /><br /> **Bottom** - 対象の関数の各復帰の直前。<br /><br /> `funcname` - 対象の関数の名前。<br /><br /> 対象の関数に StartProfile 関数が含まれている場合は、その前に SuspendProfile 関数が挿入されます。|
|**ResumeOnly:** {**Before**\|**After**\|**Top**\|**Bottom**}`,funcname`|プロファイリング実行中にデータ収集を開始または再開します。<br /><br /> 通常、このオプションは、**SuspendOnly** オプションによってプロファイリングが停止された後にプロファイリングを再開するために使用します。 このオプションは、ResumeProfile API を指定の位置に挿入します。<br /><br /> **Before** - 対象の関数に入る直前。<br /><br /> **After** - 対象の関数が終了した直後。<br /><br /> **Top** - 対象の関数に入った直後。<br /><br /> **Bottom** - 対象の関数の各復帰の直前。<br /><br /> `funcname` - 対象の関数の名前。<br /><br /> 対象の関数に StopProfile 関数が含まれている場合は、その後に ResumeProfile 関数が挿入されます。|

## <a name="see-also"></a>関連項目
- [VSPerfMon](../profiling/vsperfmon.md)
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [VSPerfReport](../profiling/vsperfreport.md)
- [VSInstr の警告](../profiling/vsinstr-warnings.md)
- [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)
