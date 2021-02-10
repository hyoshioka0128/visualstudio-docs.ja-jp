---
title: デバッグ用 SDK ヘルパー |Microsoft Docs
description: C++ でデバッグエンジン、式エバリュエーター、およびシンボルプロバイダーを実装するためのグローバルヘルパー関数である関数と宣言について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b98914d4e7fc2d63fd6cc9f79789c389e19b784
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99936003"
---
# <a name="sdk-helpers-for-debugging"></a>デバッグ用の SDK ヘルパー
これらの関数と宣言は、C++ でデバッグエンジン、式エバリュエーター、およびシンボルプロバイダーを実装するためのグローバルヘルパー関数です。

> [!NOTE]
> 現時点では、これらの関数と宣言のマネージバージョンはありません。

## <a name="overview"></a>概要
 デバッグエンジン、式エバリュエーター、およびシンボルプロバイダーを Visual Studio で使用するためには、それらを登録する必要があります。 これを行うには、レジストリサブキーとエントリを設定します。それ以外の場合は、"メトリックの設定" と呼ばれます。 次のグローバル関数は、これらのメトリックを更新するプロセスを容易にするように設計されています。 これらの関数によって更新される各レジストリサブキーのレイアウトを確認するには、レジストリの場所に関するセクションを参照してください。

## <a name="general-metric-functions"></a>一般的なメトリック関数
 これらは、デバッグエンジンによって使用される一般的な関数です。 式エバリュエーターおよびシンボルプロバイダー用の特殊な関数については、後で詳しく説明します。

### <a name="getmetric-method"></a>GetMetric メソッド
 レジストリからメトリック値を取得します。

```cpp
HRESULT GetMetric(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   DWORD * pdwValue,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszMachine|からレジスタが書き込まれる可能性のあるリモートコンピューターの名前 ( `NULL` つまり、ローカルコンピューター)。|
|pszType|からメトリック型の1つ。|
|guidSection|から特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック型の下にサブセクションが指定します。|
|pszMetric|から取得するメトリック。 これは、特定の値の名前に対応します。|
|pdwValue|からメトリックからの値の格納場所です。 GetMetric には、DWORD (この例では)、BSTR、GUID、または Guid の配列を返すことができるいくつかの種類があります。|
|pszAltRoot|から使用する代替レジストリルート。 `NULL`既定値を使用するには、をに設定します。|

### <a name="setmetric-method"></a>SetMetric メソッド
 指定されたメトリック値をレジストリに設定します。

```cpp
HRESULT SetMetric(
         LPCWSTR pszType,
         REFGUID guidSection,
         LPCWSTR pszMetric,
   const DWORD   dwValue,
         bool    fUserSpecific,
         LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszType|からメトリック型の1つ。|
|guidSection|から特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック型の下にサブセクションが指定します。|
|pszMetric|から取得するメトリック。 これは、特定の値の名前に対応します。|
|dwValue|からメトリック内の値のストレージの場所。 DWORD (この例では)、BSTR、GUID、または Guid の配列を格納できる SetMetric には、いくつかの種類があります。|
|fUserSpecific|からメトリックがユーザー固有であり、ローカルコンピューターハイブではなくユーザーの hive に書き込まれる必要がある場合は TRUE。|
|pszAltRoot|から使用する代替レジストリルート。 `NULL`既定値を使用するには、をに設定します。|

### <a name="removemetric-method"></a>RemoveMetric メソッド
 指定されたメトリックをレジストリから削除します。

```cpp
HRESULT RemoveMetric(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszType|からメトリック型の1つ。|
|guidSection|から特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック型の下にサブセクションが指定します。|
|pszMetric|から削除するメトリック。 これは、特定の値の名前に対応します。|
|pszAltRoot|から使用する代替レジストリルート。 `NULL`既定値を使用するには、をに設定します。|

### <a name="enummetricsections-method"></a>EnumMetricSections メソッド
 レジストリ内のさまざまなメトリックセクションを列挙します。

```cpp
HRESULT EnumMetricSections(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   GUID *  rgguidSections,
   DWORD * pdwSize,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszMachine|からレジスタが書き込まれる可能性のあるリモートコンピューターの名前 ( `NULL` つまり、ローカルコンピューター)。|
|pszType|からメトリック型の1つ。|
|rgguidSections|[入力、出力]入力される Guid の事前に割り当てられた配列。|
|pdwSize|から配列に格納できる Guid の最大数 `rgguidSections` 。|
|pszAltRoot|から使用する代替レジストリルート。 `NULL`既定値を使用するには、をに設定します。|

## <a name="expression-evaluator-functions"></a>式エバリュエーター関数

|Function|説明|
|--------------|-----------------|
|GetEEMetric|レジストリからメトリック値を取得します。|
|SetEEMetric|指定されたメトリック値をレジストリに設定します。|
|RemoveEEMetric|指定されたメトリックをレジストリから削除します。|
|GetEEMetricFile|指定したメトリックからファイル名を取得して読み込み、ファイルの内容を文字列として返します。|

## <a name="exception-functions"></a>例外関数

|Function|説明|
|--------------|-----------------|
|GetExceptionMetric|レジストリからメトリック値を取得します。|
|SetExceptionMetric|指定されたメトリック値をレジストリに設定します。|
|RemoveExceptionMetric|指定されたメトリックをレジストリから削除します。|
|RemoveAllExceptionMetrics|すべての例外メトリックをレジストリから削除します。|

## <a name="symbol-provider-functions"></a>シンボルプロバイダー関数

|Function|説明|
|--------------|-----------------|
|GetSPMetric|レジストリからメトリック値を取得します。|
|SetSPMetric|指定されたメトリック値をレジストリに設定します。|
|Removmetrics メトリック|指定されたメトリックをレジストリから削除します。|

## <a name="enumeration-functions"></a>列挙関数

|Function|説明|
|--------------|-----------------|
|EnumMetricSections|指定したメトリックの種類のすべてのメトリックを列挙します。|
|EnumDebugEngine|登録されているデバッグエンジンを列挙します。|
|EnumEEs|登録されている式エバリュエーターを列挙します。|
|EnumExceptionMetrics|すべての例外メトリックを列挙します。|

## <a name="metric-definitions"></a>メトリック定義
 定義済みのメトリック名には、これらの定義を使用できます。 これらの名前は、さまざまなレジストリキーと値の名前に対応し、すべてワイド文字列として定義されます。たとえば、のように `extern LPCWSTR metrictypeEngine` なります。

|定義済みのメトリックの種類|説明: の基本キー...|
|-----------------------------|---------------------------------------|
|metrictypeEngine|すべてのデバッグエンジンのメトリック。|
|metrictypePortSupplier|すべてのポートサプライヤーメトリック。|
|metrictypeException|すべての例外メトリック。|
|metricttypeEEExtension|すべての式エバリュエーター拡張機能。|

|デバッグエンジンのプロパティ|説明|
|-----------------------------|-----------------|
|metricAddressBP|アドレスのブレークポイントのサポートを示すには、0以外に設定します。|
|metricAlwaysLoadLocal|常にデバッグエンジンをローカルに読み込むには、0以外に設定します。|
|metricLoadInDebuggeeSession|使用しない|
|Metric読み込まれる Byデバッグ|デバッグエンジンが常に、またはデバッグ中のプログラムによって読み込まれることを示す場合は0以外のに設定します。|
|metricAttach|既存のプログラムへの添付ファイルのサポートを示すには、0以外に設定します。|
|metricCallStackBP|呼び出し履歴のブレークポイントのサポートを示すには、0以外に設定します。|
|metricConditionalBP|条件付きブレークポイントの設定のサポートを示す場合は0以外の値に設定します。|
|Metricの場合|データの変更に対するブレークポイントの設定のサポートを示すには、0以外の値を設定します。|
|metricDisassembly アセンブリ|逆アセンブリの一覧の作成のサポートを示すには、0以外に設定します。|
|metricDumpWriting|ダンプ書き込み (出力デバイスへのメモリのダンプ) のサポートを示すには、0以外に設定します。|
|metricENC|エディットコンティニュのサポートを示すには、0以外のを設定します。 **注:**  カスタムデバッグエンジンではこれを設定しないようにするか、常に0に設定する必要があります。|
|metricExceptions|例外のサポートを示すには、0以外に設定します。|
|metricFunctionBP|名前付きブレークポイント (特定の関数名が呼び出されたときに中断するブレークポイント) のサポートを示すには、0以外に設定します。|
|metricHitCountBP|"ヒットポイント" ブレークポイント (特定の回数に達した後にのみトリガーされるブレークポイント) の設定のサポートを示すには、0以外の値に設定します。|
|metricJITDebug|Just-in-time デバッグのサポートを示す場合は0以外に設定します (実行中のプロセスで例外が発生したときにデバッガーが起動されます)。|
|metricMemory|使用しない|
|metricPortSupplier|実装されている場合は、ポートサプライヤーの CLSID に設定します。|
|metricRegisters|使用しない|
|metricSetNextStatement|次のステートメントを設定するためのサポートを示す場合は0以外の値に設定します (中間ステートメントの実行をスキップします)。|
|metricSuspendThread|スレッド実行を中断するためのサポートを示すには、0以外に設定します。|
|metricWarnIfNoSymbols|記号がない場合にユーザーに通知する必要があることを示すには、0以外に設定します。|
|metricProgramProvider|プログラムプロバイダーの CLSID に設定します。|
|metricAlwaysLoadProgramProviderLocal|プログラムプロバイダーを常にローカルに読み込む必要があることを示す場合は、0以外に設定します。|
|metricEngineCanWatchProcess|プログラムプロバイダーではなくプロセスイベントをデバッグエンジンが監視することを示すには、これを0以外に設定します。|
|metricRemoteDebugging|リモートデバッグのサポートを示す場合は、0以外に設定します。|
|metricEncUseNativeBuilder|エディットコンティニュマネージャーがデバッグエンジンの encbuild.dll を使用してエディットコンティニュ用にビルドする必要があることを示す場合は、0以外に設定します。 **注:**  カスタムデバッグエンジンではこれを設定しないようにするか、常に0に設定する必要があります。|
|metricLoadUnderWOW64|64ビットプロセスをデバッグするときに、デバッグエンジンを WOW 下のデバッグ対象プロセスに読み込む必要があることを示すには、これを0以外に設定します。それ以外の場合は、Visual Studio プロセス (WOW64 で実行されている) にデバッグエンジンが読み込まれます。|
|metricLoadProgramProviderUnderWOW64|WOW で64ビットプロセスをデバッグするときに、プログラムプロバイダーをデバッグ対象プロセスに読み込む必要があることを示すには、これを0以外に設定します。それ以外の場合は、Visual Studio プロセスに読み込まれます。|
|metricStopOnExceptionCrossingManagedBoundary|マネージ/アンマネージコードの境界を越えて未処理の例外がスローされた場合にプロセスを停止することを示すには、このを0以外に設定します。|
|metricAutoSelectPriority|デバッグエンジンの自動選択の優先度を設定します (値が大きいほど優先順位が高くなります)。|
|Metricautoselec/List|自動選択で無視されるデバッグエンジンの Guid を指定するエントリを含むレジストリキー。 これらのエントリは、文字列として表現された GUID を持つ数値 (0、1、2など) です。|
|metricIncompatibleList|このデバッグエンジンと互換性のないデバッグエンジンの Guid を指定するエントリを含むレジストリキー。|
|metricDisableJITOptimization|デバッグ中に just-in-time 最適化 (マネージコードの場合) を無効にする場合は、0以外に設定します。|

|式エバリュエーターのプロパティ|説明|
|-------------------------------------|-----------------|
|metricEngine|これは、指定された式エバリュエーターをサポートするデバッグエンジンの数を保持します。|
|metricPreloadModules|プログラムに対して式エバリュエーターを起動したときにモジュールをプリロードする場合は、0以外に設定します。|
|metricThisObjectName|これを "this" オブジェクト名に設定します。|

|式エバリュエーター拡張機能のプロパティ|説明|
| - |-----------------|
|metricExtensionDll|この拡張機能をサポートする dll の名前。|
|metricExtensionRegistersSupported|サポートされているレジスタの一覧。|
|metricExtensionRegistersEntryPoint|レジスタにアクセスするためのエントリポイント。|
|サポートされている Metricextensionタイプ|サポートされている型のリスト。|
|Metricextensionentrypoint Entrypoint|型にアクセスするためのエントリポイント。|

|ポートサプライヤーのプロパティ|説明|
|------------------------------|-----------------|
|metricPortPickerCLSID|ポートピッカーの CLSID (ユーザーがポートを選択し、デバッグに使用するポートを追加するために使用できるダイアログボックス)。|
|metricDisallowUserEnteredPorts|ユーザーが入力したポートをポート供給業者に追加できない場合は0以外の値です (これにより、ポートピッカーダイアログボックスが基本的に読み取り専用になります)。|
|metricPidBase|プロセス Id を割り当てるときにポートサプライヤーによって使用される基本プロセス ID。|

|定義済み SP ストアの種類|説明|
|-------------------------------|-----------------|
|storetypeFile|シンボルは別のファイルに格納されます。|
|storetypeMetadata|シンボルは、メタデータとしてアセンブリに格納されます。|

|その他のプロパティ|説明|
|------------------------------|-----------------|
|metricShowNonUserCode|非ユーザーコードを表示するには、0以外に設定します。|
|Metricジャスト Mycodeステッピング|ユーザーコードでのみステップ実行が可能であることを示す場合は、0以外に設定します。|
|metricCLSID|特定のメトリック型のオブジェクトの CLSID。|
|metricName|特定のメトリック型のオブジェクトのわかりやすい名前。|
|metricLanguage|言語名。|

## <a name="registry-locations"></a>レジストリの場所
 メトリックは、レジストリの読み取りと書き込みを行い、特に `VisualStudio` サブキーで行います。

> [!NOTE]
> ほとんどの場合、メトリックは HKEY_LOCAL_MACHINE キーに書き込まれます。 ただし、場合によっては、HKEY_CURRENT_USER がコピー先のキーになります。 Dbgmetric は、両方のキーを処理します。 メトリックを取得すると、最初に HKEY_CURRENT_USER が検索され、次に HKEY_LOCAL_MACHINE ます。 メトリックを設定するときに、使用する最上位レベルのキーをパラメーターで指定します。

 *[レジストリキー]*\

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[バージョンルート]*\

 *[メトリックルート]*\

 *[メトリックの種類]*\

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[レジストリキー]*|`HKEY_CURRENT_USER` または `HKEY_LOCAL_MACHINE`。|
|*[バージョンルート]*|Visual Studio のバージョン (たとえば、、、 `7.0` `7.1` または `8.0` )。 ただし、このルートは、 **/rootsuffix** スイッチを使用して **devenv.exe** に変更することもできます。 VSIP の場合、この修飾子は通常は **exp** であるため、バージョンのルートは 8.0 Exp のようになります。|
|*[メトリックルート]*|これは `AD7Metrics` `AD7Metrics(Debug)` 、dbgmetric. lib のデバッグバージョンが使用されているかどうかによって、またはのいずれかになります。 **注:**  Dbgmetric が使用されているかどうかにかかわらず、レジストリに反映する必要があるデバッグバージョンとリリースバージョンが異なる場合は、この名前付け規則に従う必要があります。|
|*[メトリックの種類]*|書き込まれるメトリックの種類 `Engine` (、、 `ExpressionEvaluator` など) `SymbolProvider` 。これらはすべて、として dbgmetric. h で定義されます。 `metricTypeXXXX` ここで、 `XXXX` は特定の型名です。|
|*非対称*|メトリックを設定するために値が割り当てられるエントリの名前。 メトリックの実際の編成は、メトリックの種類によって異なります。|
|*[メトリック値]*|メトリックに割り当てられた値。 値が持つ必要がある型 (文字列、数値など) は、メトリックによって異なります。|

> [!NOTE]
> すべての Guid は、の形式で格納され `{GUID}` ます。 たとえば、「 `{123D150B-FA18-461C-B218-45B3E4589F9B}` 」のように入力します。

### <a name="debug-engines"></a>デバッグエンジン
 次に示すのは、レジストリ内のデバッグエンジンのメトリックの編成です。 `Engine` はデバッグエンジンのメトリック型名であり、上記のレジストリサブツリーの *[metric type]* に対応します。

 `Engine`\

 *[エンジン guid]*\

 `CLSID` = *[クラス guid]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 `PortSupplier`\

 `0` = *[ポート供給元 guid]*

 `1` = *[ポート供給元 guid]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[エンジン guid]*|デバッグエンジンの GUID。|
|*[クラス guid]*|このデバッグエンジンを実装するクラスの GUID。|
|*[ポート供給元 guid]*|ポートサプライヤーの GUID (存在する場合)。 多くのデバッグエンジンでは既定のポート供給業者が使用されるため、独自の供給業者は指定しません。 この場合、サブキーは `PortSupplier` 存在しません。|

### <a name="port-suppliers"></a>ポート サプライヤー
 次に示すのは、レジストリ内のポートサプライヤーメトリックの編成です。 `PortSupplier` ポートサプライヤーのメトリック型の名前を指定し、 *[metric type]* に対応します。

 `PortSupplier`\

 *[ポート供給元 guid]*\

 `CLSID` = *[クラス guid]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[ポート供給元 guid]*|ポートサプライヤーの GUID|
|*[クラス guid]*|このポートサプライヤーを実装するクラスの GUID|

### <a name="symbol-providers"></a>シンボルプロバイダー
 次に示すのは、レジストリ内のシンボルサプライヤーメトリックの編成です。 `SymbolProvider` シンボルプロバイダーのメトリック型の名前を指定し、 *[metric type]* に対応します。

 `SymbolProvider`\

 *[シンボルプロバイダー guid]*\

 `file`\

 `CLSID` = *[クラス guid]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 `metadata`\

 `CLSID` = *[クラス guid]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[シンボルプロバイダー guid]*|シンボルプロバイダーの GUID|
|*[クラス guid]*|このシンボルプロバイダーを実装するクラスの GUID|

### <a name="expression-evaluators"></a>式エバリュエーター
 次に示すのは、レジストリ内の式エバリュエーターメトリックの編成です。 `ExpressionEvaluator` 式エバリュエーターのメトリック型の名前を指定し、 *[metric type]* に対応します。

> [!NOTE]
> のメトリックの種類 `ExpressionEvaluator` は、dbgmetric. h で定義されていません。式エバリュエーターのすべてのメトリックの変更は、適切な式エバリュエーターのメトリック関数を経由することを前提としています ( `ExpressionEvaluator` サブキーのレイアウトはやや複雑であるため、詳細は dbgmetric. lib 内で非表示になっています)。

 `ExpressionEvaluator`\

 *[言語 guid]*\

 *[ベンダ guid]*\

 `CLSID` = *[クラス guid]*

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 `Engine`\

 `0` = *[デバッグエンジン guid]*

 `1` = *[デバッグエンジン guid]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[言語 guid]*|言語の GUID|
|*[ベンダ guid]*|ベンダーの GUID|
|*[クラス guid]*|この式エバリュエーターを実装するクラスの GUID|
|*[デバッグエンジン guid]*|この式エバリュエーターが動作するデバッグエンジンの GUID|

### <a name="expression-evaluator-extensions"></a>式エバリュエーター拡張機能
 次に示すのは、レジストリ内の式エバリュエーター拡張機能のメトリックの編成です。 `EEExtensions` 式エバリュエーター拡張機能のメトリック型の名前を指定し、 *[metric type]* に対応します。

 `EEExtensions`\

 *[拡張 guid]*\

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[拡張 guid]*|式エバリュエーター拡張機能の GUID|

### <a name="exceptions"></a>例外
 次に示すのは、レジストリ内の例外メトリックの編成です。 `Exception` 例外のメトリック型の名前を指定します。 *[metric type]* に対応します。

 `Exception`\

 *[デバッグエンジン guid]*\

 *[例外の種類]*\

 *例外的*\

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

 *例外的*\

 *[メトリック] = [メトリック値]*

 *[メトリック] = [メトリック値]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[デバッグエンジン guid]*|例外をサポートするデバッグエンジンの GUID。|
|*[例外の種類]*|処理できる例外のクラスを識別するサブキーの一般的なタイトル。 一般的な名前は、 **C++ 例外**、 **Win32 例外**、 **共通言語ランタイム例外**、および **ネイティブ Run-Time チェック** です。 これらの名前は、ユーザーに対して特定のクラスの例外を識別するためにも使用されます。|
|*例外的*|例外の名前。たとえば、 **_com_error** や **制御を解除** します。 これらの名前は、ユーザーに対する特定の例外を識別するためにも使用されます。|

## <a name="requirements"></a>要件
 これらのファイルは、 [!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)] SDK のインストールディレクトリにあります (既定では *[drive]*、VISUAL Studio 2010 sdk \\ )。

 ヘッダー: すべての/dbgmetrich

 ライブラリ: lib\ のようになります。ライブラリ

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
