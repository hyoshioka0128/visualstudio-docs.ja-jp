---
title: VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- proflilng tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fff2486c4197cbbe28c3b5deb0099e264805e12b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74771693"
---
# <a name="rapid-web-site-profiling-with-vsperfaspnetcmd"></a>VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング

**VSPerfASPNETCmd** コマンド ライン ツールを使用すると、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを簡単にプロファイルできます。 [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールと比較すると、オプションが減り、環境変数を設定する必要がなく、コンピューターを再起動する必要がありません。 スタンドアロン プロファイラーでプロファイリングを行う場合は、**VSPerfASPNETCmd** の使用をお勧めします。 詳細については、[スタンドアロンのプロファイラーをインストールする](../profiling/how-to-install-the-stand-alone-profiler.md)」をご覧ください。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

 コンカレンシー データの収集やプロファイリングの一時停止と再開などの一部のシナリオでは、プロファイリングに **VSPerfCmd** の使用をお勧めします。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

## <a name="profile-an-aspnet-application"></a>ASP.NET アプリケーションのプロファイル

[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションをプロファイルするには、次の各セクションで説明するコマンドの 1 つを入力します。 Web サイトが起動し、プロファイラーがデータ収集を開始します。 アプリケーションを実行した後、ブラウザーを閉じます。 プロファイリングを停止するには、コマンド プロンプト ウィンドウで **Enter** キーを押します。

> [!NOTE]
> 既定では、**vsperfaspnetcmd** コマンドの後にコマンド プロンプトは戻りません。 **/nowait** オプションを使用すると、コマンド プロンプトを強制的に戻すことができます。 「[/NoWait オプションの使用](#use-the-nowait-option)」をご覧ください。

## <a name="to-collect-application-statistics-by-using-the-sampling-method"></a>サンプリング メソッドを使用してアプリケーションの統計情報を収集するには
 サンプリングは **VSPerfASPNETCmd** ツールの既定のプロファイル方法であるため、コマンド ラインで指定する必要はありません。 次のコマンド ラインは、指定した Web アプリケーションからアプリケーションの統計情報を収集します。

 **vsperfaspnetcmd**  *websiteUrl*

 ローカル サーバーでホストされる *websiteUrl* の例として、 *http://localhost/MySite/default.aspx* が考えられます。 外部サイトの例は、 *http://www.contoso.com* になります。 詳細については、「[Visual Studio でプロジェクトを開かずに Web サイトをプロファイリングする](how-to-collect-performance-data-for-a-web-site.md#to-profile-a-web-site-without-opening-a-project-in-visual-studio)」の URL の例を参照してください。

## <a name="to-collect-detailed-timing-data-by-using-the-instrumentation-method"></a>インストルメンテーション メソッドを使用して詳細なタイミング データを収集するには

次のコマンド ラインを使用して、動的にコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションから詳細なタイミング データを収集します。

**vsperfaspnetcmd /trace**  *websiteUrl*

Web アプリケーション内の静的にコンパイルされた .*dll* ファイルをプロファイルする場合は、[VSInstr](../profiling/vsinstr.md) コマンド ライン ツールを使用してファイルをインストルメント化する必要があります。 vsperfaspnetcmd /trace コマンドを実行すると、インストルメント化されたファイルのデータが収集されます。

## <a name="to-collect-net-memory-data"></a>.NET メモリ データを収集するには

**/Memory** オプションを使用すると、.NET メモリ内のオブジェクトの割り当てに関するデータが収集されるため、これらのオブジェクトの有効期間に関するデータを収集できます。 割り当てデータの収集は **/Memory** データ オプションの既定のモードであるため、コマンド ラインで指定する必要はありません。

 **vsperfaspnetcmd /memory** *websiteUrl*

 **Lifetime** パラメーターを使用して、割り当てデータに加え、オブジェクトの有効期間データを収集します。

 **vsperfaspnetcmd /memory:lifetime** *websiteUrl*

 また、 **/Trace** オプションを使用して .NET メモリ データと共に詳細なタイミング情報を収集することもできます。

 **vsperfaspnetcmd /memory** **[:lifetime]** **/trace**`websiteUrl`

## <a name="to-collect-tier-interaction-data"></a>階層相互作用データを収集するには

> [!WARNING]
> 階層相互作用プロファイル (TIP) データは、Visual Studio の任意のエディションを使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、Visual Studio Enterprise のみです。
>
> Windows 8 や Windows Server 2012 の TIP データを収集するには、インストルメンテーション ( **/trace**) オプションを使用する必要があります。

サンプリング データと共に階層相互作用データを収集するには、コマンド ラインに次のように入力します。

**vsperfaspnetcmd /tip** `websiteUrl`

インストルメンテーション データと共に階層相互作用データを収集するには、コマンド ラインに次のように入力します。

**vsperfaspnetcmd /trace /tip** *websiteUrl*

.NET メモリ データと共に階層相互作用データを収集するには、コマンド ラインに次のように入力します。

**vsperfaspnetcmd /memory** **[:lifetime]** **/tip**_websiteUrl_

## <a name="use-the-nowait-option"></a>/NoWait オプションの使用

既定では、**vsperfaspnetcmd** コマンドの後にコマンド プロンプトは戻りません。 次の構文オプションを使用すると、コマンド プロンプトを強制的に戻すことができます。 その後、コマンド プロンプト ウィンドウで他の操作を実行できます。 プロファイリングを終了するには、別の **vsperfaspnetcmd** コマンドで **/shutdown** オプションを使用します。

プロファイリングを開始するには、次のように入力します。

**vsperfaspnetcmd** [ */Options*] **/nowait**_websiteUrl_

プロファイリングを終了するには、次のように入力します。

**vsperfaspnetcmd /shutdown** *websiteUrl*

## <a name="additional-options"></a>追加オプション

**vsperfaspnetcmd /shutdown** コマンドを除き、このセクションの前半で説明した各コマンドに次の任意のオプションを追加できます。

|オプション|説明|
|------------|-----------------|
|**/Output:** `VspFile`|既定では、プロファイル データ (.*vsp*) ファイルは **PerformanceReport.vsp** というファイル名で現在のディレクトリに作成されます。 別の場所、ファイル名、またはその両方を指定するには、/output オプションを使用します。|
|**/PackSymbols:Off**|既定では、VsPerfASPNETCmd に .*vsp* ファイルのシンボル (関数名、パラメーター名など) が埋め込まれています。 シンボルを埋め込むと、プロファイル データ ファイルが非常に大きくなる可能性があります。 データを分析するときにシンボルを含む .*pdb* ファイルにアクセスできる場合は、/packsymbols:off オプションを使用してシンボルの埋め込みを無効にしてください。|
