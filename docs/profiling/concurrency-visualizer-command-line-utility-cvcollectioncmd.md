---
title: コンカレンシー ビジュアライザー コマンドライン ユーティリティ (CVCollectionCmd) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.cvcollectioncmd
ms.assetid: 476601be-1608-4014-af15-5aba6ccbed1c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2721798ee9f0c7e006acdedbecaecbd56068be3f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "72911203"
---
# <a name="concurrency-visualizer-command-line-utility-cvcollectioncmd"></a>コンカレンシー ビジュアライザー コマンドライン ユーティリティ (CVCollectionCmd)
コンカレンシー ビジュアライザーのコマンド ライン ユーティリティ (*CVCollectionCmd.exe*) を使用して、コマンド ラインからトレースを収集することで、Visual Studio 用のコンカレンシー ビジュアライザーでトレースを表示できます。 これらのツールは、Visual Studio がインストールされていないコンピューターで使用できます。

> [!NOTE]
> Visual Studio 2013 以降、コンカレンシー ビジュアライザーは任意の拡張機能となっています。 (以前は、Visual Studio に含まれていました。)ダウンロード センターから [Concurrency Visualizer Collection Tools for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=49103) をダウンロードできます。

## <a name="download-the-concurrency-visualizer-command-line-utility"></a>コンカレンシー ビジュアライザーのコマンド ライン ユーティリティのダウンロード
 コマンド ライン ユーティリティをダウンロードしてインストールするには、[Concurrency Visualizer Collection Tools for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=49103) に移動して指示に従います。 既定では、*CVCollectionCmd.exe* のインストール先は %ProgramFiles%\Microsoft Concurrency Visualizer Collection Tools\ (%ProgramFiles(x86)%\Microsoft Concurrency Visualizer Collection Tools\ on x64 computers) となっています。

## <a name="collect-a-trace-with-cvcollectioncmd"></a>CVCollectionCmd を使用したトレースの収集
 トレースを収集するには、CVCollectionCmd でアプリを起動するか、CVCollectionCmd にアタッチします。 オプションについては、以下のコマンド リファレンスを参照してください。 次に例を示します。

```cmd
<Path>CVCollectionCmd /launch c:\myapp\myapp.exe /outdir c:\myapp\data
```

## <a name="commands-and-parameters"></a>コマンドおよびパラメーター
 コマンド ライン ユーティリティにコマンドとパラメーターに関するヘルプを表示するには、コマンド プロンプトに次のコマンドを入力します。

 **CvCollectionCmd /?**

|オプション|説明|パラメーター|戻り値|
|------------|-----------------|----------------|-------------------|
|Query|コレクションを開始できるかどうかを返します。|なし|コレクションを開始できる場合は 0。<br /><br /> コレクションが既に実行中の場合は 1。<br /><br /> コレクションは実行中でないが、必要な [ETW](/dotnet/framework/wcf/samples/etw-tracing) セッションの 1 つ以上が既に有効になっている場合は 2。|
|Launch|コンカレンシー ビジュアライザーで、指定されたプロセスを実行します。|実行可能ファイルのパス。|実行が成功した場合は 0。<br /><br /> ターゲット アプリケーションを開始できなかったために実行が失敗した場合は 1。<br /><br /> CVCollectionCmd に、指定された出力ディレクトリへの書き込みアクセス許可がないために実行が失敗した場合は 13。|
|Attach|システム全体でのトレースのコレクションを開始します。プロセスが指定されている場合は、そのプロセスにアタッチします。|なし。|アタッチが成功した場合は 0。<br /><br /> 指定されたプロセスが無効であるか、指定があいまいなためにアタッチが失敗した場合は 1。<br /><br /> CVCollectionCmd に、指定された出力ディレクトリへの書き込みアクセス許可がないためにアタッチが失敗した場合は 13。|
|Detach|コレクションを停止します。|なし。|デタッチが成功した場合は 0。<br /><br /> コレクションが現在実行されていないためにデタッチが失敗した場合は 1。<br /><br /> コレクションを停止できなかったためにデタッチが失敗した場合は 2。|
|Analyze|指定されたトレースを分析します。|CVTrace ファイルの完全パス。|分析が成功した場合は 0。<br /><br /> システム全体のトレースが指定されている一方、ターゲット プロセスが指定されていないために分析を開始できない場合は 1。<br /><br /> システム全体のトレースではない一方、プロセスが指定されているために分析を開始できない場合は 2。<br /><br /> 指定されたプロセスが無効なために分析が失敗した場合は 3。<br /><br /> 指定された CVTrace ファイルが無効なために分析が失敗した場合は 4。|
|LaunchArgs|ターゲット実行可能ファイルの引数を指定します。 このオプションは、Launch コマンドにのみ適用されます。|アプリケーションへのコマンド ライン引数。|なし。|
|OutDir|トレース ファイルを保存するディレクトリを指定します。 Launch コマンドと Attach コマンドに適用されます。|ディレクトリ パスまたは相対パス。|なし。|
|Process|Attach コマンドの実行時にアタッチするプロセス、または Analyze コマンドの実行時にトレースで分析するプロセスを指定します。 Attach コマンドと Analyze コマンドに適用されます。|PID またはプロセスの名前。|なし。|
|Config|既定以外のコレクション設定が必要な場合、構成ファイルのパスを指定します。   Launch コマンド、Attach コマンド、および Analyze コマンドに適用されます。|XML 構成ファイルのディレクトリ パスまたは相対パス。|なし。|

## <a name="customize-configuration-settings"></a>構成設定のカスタマイズ
 CVCollectionCmd を使用してトレースを収集する際に、コレクション設定をカスタマイズする必要がある場合には、構成ファイルを使用してコレクション設定を指定します。

> [!NOTE]
> Visual Studio を使用してトレースを収集する場合は、構成ファイルを直接変更しないでください。  代わりに、 [[詳細設定]](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) ダイアログ ボックスを使用して設定を変更します。

 コレクション設定を変更するには、CVCollectionCmd ユーティリティを実行するコンピューター上に構成ファイルを作成します。 新しい構成ファイルを作成することも、Visual Studio がインストールされているコンピューター上の構成ファイルをコピーして、そのコピーを変更することもできます。 構成ファイルの名前は *UserConfig.xml* で、保管先は *Local AppData* フォルダーです。 ユーティリティを実行するときに、Launch、Attach、または Analyze コマンドと共に Config オプションを使用します。  Config オプションに関連付けられているパラメータに、構成ファイルのパスを指定します。

### <a name="configuration-file-tags"></a>構成ファイルのタグ
 構成ファイルは、XML ベースです。 有効なタグと値を次に示します。

| タグ | 説明 | 値 |
|-------------------------| - | - |
| Config | 構成ファイル全体を区分します。 | 以下の要素が含まれている必要があります。<br /><br /> -   MinorVersion<br />-   MajorVersion |
| MajorVersion | 構成ファイルのメジャー バージョンを指定します。 | [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] プロジェクトの場合は、1 を指定する必要があります。 1 が指定されていない場合、ユーティリティは機能しません。 |
| MinorVersion | 構成ファイルのマイナー バージョンを指定します。 | [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] プロジェクトの場合は、0 を指定する必要があります。 0 が指定されていない場合、ユーティリティは機能しません。 |
| IncludeEnvSymbolPath | 環境シンボル パス (_NT_SYMBOL_PATH) を使用するかどうかを判別する値を設定します。 | -   True<br />-   False |
| DeleteEtlsAfterAnalysis | 分析の完了時に ETL ファイルを削除するかどうかを判別する値を設定します。 | -   True<br />-   False |
| SymbolPath | シンボル サーバーのパスを指定します。 詳細については、「 [Microsoft のシンボル サーバーを使用して、デバッグ シンボル ファイルを入手するには](/windows/win32/dxtecharts/debugging-with-symbols)」を参照してください。 | ディレクトリ名または URL。 |
| Markers | マーカー プロバイダーのリストが格納されます。 | 0 個以上の MarkerProvider 要素を格納できます。 |
| MarkerProvider | 単一のマーカー プロバイダーを指定します。 | 以下の要素が含まれている必要があります。<br /><br /> -   Level<br />-   GUID<br />-   Name<br /><br /> 以下の要素を含めることができます。<br /><br /> -   Categories<br />-   IsEnabled |
| Level | MarkerProvider の重要度レベルを設定します。 | -   Low<br />-   Normal<br />-   High<br />-   Critical<br />-   Everything |
| Guid | ETW マーカー プロバイダーのグローバル一意識別子。 | GUID。 |
| Name | マーカー プロバイダーの説明を指定します。 | 文字列。 |
| Categories | マーカー プロバイダーについて収集するカテゴリを指定します。 | コンマ区切りの文字列または数値の範囲。 |
| IsEnabled | マーカー プロバイダーをコレクションに有効にするかどうかを判別する値を設定します。 | -   True<br />-   False |
| FilterConfig | コレクションからフィルター処理する ETW イベントの構成オプションのリストを指定します。 | 以下の要素を含めることができます。<br /><br /> -   CollectClrEvents<br />-   ClrCollectionOptions<br />-   CollectSampleEvents<br />-   CollectGpuEvents<br />-   CollectFileIO |
| CollectClrEvents | CLR イベントを収集するかどうかを判別する値を設定します。 | -   True<br />-   False |
| ClrCollectionOptions | ネイティブ アプリの CLR イベントを収集するかどうか、および NGEN ランダウン イベントを収集するかどうかを指定します。 | 以下の値のいずれか、または両方を含めることも、空にすることもできます。<br /><br /> -   CollectForNative<br />-   DisableNGenRundown |
| CollectSampleEvents | サンプル イベントを収集するかどうかを判別する値を設定します。 | -   True<br />-   False |
| CollectGpuEvents | DX によって生成されたイベントを収集するかどうかを判別する値を設定します。 | -   True<br />-   False |
| CollectFileIO | ファイル I/O イベントを収集するかどうかを判別する値を設定します。 | -   True<br />-   False |
| UserBufferSettings | ユーザー バッファー設定パラメーターのリストを指定します。 | 以下の要素が含まれている必要があります。<br /><br /> -   BufferFlushTimer<br />-   BufferSize<br />-   MinimumBuffers<br />-   MaximumBuffers |
| KernelBufferSettings | カーネル バッファー設定パラメーターのリストを指定します。 | 以下の要素が含まれている必要があります。<br /><br /> -   BufferFlushTimer<br />-   BufferSize<br />-   MinimumBuffers<br />-   MaximumBuffers |
| BufferFlushTimer | ETW バッファーのフラッシュ タイマーを指定します。 | 正の整数。 |
| BufferSize | イベント トレース セッション バッファーに割り当てられるメモリーの量 (KB 単位)。 | 0 ～ 1024 の数値。 |
| MinimumBuffers | イベント トレース セッションのバッファー プールに割り当てられるバッファーの最小数。 | 論理コア数の 2 倍以上の正の整数。 |
| MaximumBuffers | イベント トレース セッションのバッファー プールに割り当てられるバッファーの最大数。 | MinimumBuffers の値以上の数値。 |
| JustMyCode | [マイ コードのみ] ディレクトリのリストを指定します。 | 0 個以上の MyCodeDirectory 要素のリスト。 |
| MyCodeDirectory | コードを格納するディレクトリを指定します。 | 絶対パス。 |

### <a name="example"></a>例
 新しい構成ファイルを最初から作成する代わりに、以下の例をコピーして、そのコピーを必要に応じて変更できます。

```xml
<?xml version="1.0"?>
<LocalConfig xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" MajorVersion="1" MinorVersion="0">

  <IncludeEnvSymbolPath>true</IncludeEnvSymbolPath>

  <DeleteEtlsAfterAnalysis>true</DeleteEtlsAfterAnalysis>

  <TraceLocation>C:\traces</TraceLocation>

  <SymbolPath>http://symweb</SymbolPath>

  <Markers>
    <MarkerProvider Name="Default" Guid="8d4925ab-505a-483b-a7e0-6f824a07a6f0" Level="Low" />
    <MarkerProvider Name="TPL" Guid="2e5dba47-a3d2-4d16-8ee0-6671ffdcd7b5" Level="Normal" />
    <MarkerProvider Name="TPL Dataflow" Guid="16f53577-e41d-43d4-b47e-c17025bf4025" Level="Normal" />
    <MarkerProvider Name="TPL Synchronization" Guid="ec631d38-466b-4290-9306-834971ba0217" Level="Normal" />
    <MarkerProvider Name="PLINQ" Guid="159eeeec-4a14-4418-a8fe-faabcd987887" Level="Normal" />
    <MarkerProvider Name="Concurrency Runtime" Guid="f7b697a3-4db5-4d3b-be71-c4d284e6592f" Level="Normal" />
    <MarkerProvider Name="Scenario Markers" Guid="fb9244c9-f23a-4966-8a9c-97a51f8c355b" Level="Low" />

    <!-- The IsEnabled and Categories elements are optional -->
    <MarkerProvider Name="myMarker1" Guid="d0dbb3a3-895c-4ce6-96d9-28f69d664dc3" Level="Critical" IsEnabled="false" Categories="0,1,3-5,8" />
    <MarkerProvider Name="myMarker2" Guid="03452127-a617-4302-9e30-c0d10442e4ee" Level="Low" IsEnabled="false" Categories="0,1,3-5,8-10,11-13" />
  </Markers>

  <FilterConfig>
    <CollectClrEvents>true</CollectClrEvents>
    <ClrCollectionOptions>CollectForNative DisableNGenRundown</ClrCollectionOptions>
    <CollectSampleEvents>true</CollectSampleEvents>
    <CollectGpuEvents>true</CollectGpuEvents>
    <CollectFileIO>true</CollectFileIO>
  </FilterConfig>

  <UserBufferSettings>
    <BufferFlushTimer>0</BufferFlushTimer>
    <BufferSize>256</BufferSize>
    <MinimumBuffers>512</MinimumBuffers>
    <MaximumBuffers>1024</MaximumBuffers>
  </UserBufferSettings>

  <KernelBufferSettings>
    <BufferFlushTimer>0</BufferFlushTimer>
    <BufferSize>256</BufferSize>
    <MinimumBuffers>512</MinimumBuffers>
    <MaximumBuffers>1024</MaximumBuffers>
  </KernelBufferSettings>

  <!-- List of MyCodeDirectory directories -->
  <JustMyCode>
    <MyCodeDirectory>C:\myBinaries1</MyCodeDirectory>
    <MyCodeDirectory>C:\myBinaries2</MyCodeDirectory>
  </JustMyCode>
</LocalConfig>

```
