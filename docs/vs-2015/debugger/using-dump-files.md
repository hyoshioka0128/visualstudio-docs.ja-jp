---
title: ダンプファイルを使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crashdump
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- dumps, about dumps
- crash dumps
- dump files
- dumps
ms.assetid: b71be6dc-57e0-4730-99d2-b540a0863e49
caps.latest.revision: 56
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1a2d6215887512f2e0c1410688b2bc924dc1fe3a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86387058"
---
# <a name="using-dump-files"></a>ダンプ ファイルの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ヒープ情報あり/なしのダンプ ファイル、ダンプ ファイルを作成する、ダンプ ファイルを開く、ダンプ ファイルのバイナリ、PDB、ソース ファイルを検索する 
  
## <a name="contents"></a><a name="BKMK_Contents"></a> 目次  
 [ダンプ ファイルとは](#BKMK_What_is_a_dump_file_)  
  
 [ヒープの有無に関係なくファイルをダンプする](#BKMK_Dump_files__with_or_without_heaps)  
  
 [要件と制限事項](#BKMK_Requirements_and_limitations)  
  
 [ダンプファイルを作成する](#BKMK_Create_a_dump_file)  
  
 [ダンプファイルを開く](#BKMK_Open_a_dump_file)  
  
 [バイナリ、シンボル (.pdb) ファイル、ソース ファイルを検索する](#BKMK_Find_binaries__symbol___pdb__files__and_source_files)  
  
## <a name="what-is-a-dump-file"></a><a name="BKMK_What_is_a_dump_file_"></a> ダンプファイルとは  
 *ダンプファイル*は、ダンプが実行された時点でのアプリのスナップショットです。 ダンプ ファイルには、実行されたプロセスと読み込まれたモジュールが示されます。 ダンプがヒープ情報と共に保存された場合、ダンプ ファイルにはその時点におけるアプリのメモリの内容のスナップショットも含まれています。 Visual Studio でヒープ情報ありのダンプ ファイルを開くのは、デバッグ セッションのブレークポイントで実行を中断するようなものです。 実行を続行することはできませんが、ダンプの作成時におけるアプリのスタック、スレッド、変数値を調べることができます。  
  
 ダンプが主に使用されるのは、開発者がアクセスできないコンピューター上で発生する問題をデバッグする場合です。 たとえば、お客様のコンピューターで顧客のクラッシュや応答していないプログラムを再現できない場合に、顧客のコンピューターのダンプファイルを使用できます。 また、テスト用コンピューターを使用してより多くのテストを行うことができるように、クラッシュまたは応答しないプログラムデータを保存するために、テスターによってダンプが作成されます。 Visual Studio デバッガーでは、マネージドまたはネイティブ コードのダンプ ファイルを保存できます。 デバッガーは、Visual Studio または *ミニ* ダンプ形式でファイルを保存する他のプログラムによって作成されたダンプファイルを読み込むことができます。  
  
 ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="dump-files-with-or-without-heaps"></a><a name="BKMK_Dump_files__with_or_without_heaps"></a> ヒープの有無に関係なくファイルをダンプする  
 ヒープ情報あり/なしのダンプ ファイルを作成できます。  
  
- **ヒープを含むダンプファイル** には、アプリのメモリのスナップショットが含まれています。 ダンプの作成時における変数値も含まれています。 ヒープ情報と共に保存されたダンプ ファイルを読み込む場合、Visual Studio はアプリケーション バイナリが見つからなくてもシンボルを読み込むことができます。 また、Visual Studio は、読み込まれたネイティブ モジュールのバイナリをダンプ ファイルに保存するため、デバッグが大幅に簡単になります。  
  
- ヒープの**ないダンプファイル**は、ヒープ情報を含むダンプよりもはるかに小さくなります。 ただし、デバッガーはアプリのバイナリを読み込んでシンボル情報を見つける必要があります。 バイナリはダンプの作成時に使用されたバイナリと完全に一致する必要があります。 ヒープ情報なしのダンプ ファイルには、スタック変数の値のみ保存されます。  
  
  ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="requirements-and-limitations"></a><a name="BKMK_Requirements_and_limitations"></a> 要件と制限事項  
  
- 最適化されたコードのダンプ ファイルをデバッグすると、混乱が生じることがあります。 たとえば、コンパイラによる関数のインライン展開により、予期しない呼び出し履歴になっていたり、その他の最適化により、変数の有効期間が変更されていたりします。  
  
- 64 ビット コンピューターからのダンプ ファイルは、64 ビット コンピューター上で実行される Visual Studio のインスタンス上でデバッグする必要があります。  
  
- VS 2013 より前の Visual Studio のバージョンでは、一部のツール (タスク マネージャーや 64 ビット WinDbg など) によって収集された 64 ビット コンピューター上で実行する 32 ビット アプリケーションのダンプは Visual Studio で開くことができませんでした。 VS 2013 ではこの制限はありません。  
  
- Visual Studio では、ARM デバイスからのネイティブ アプリのダンプ ファイルをデバッグできます。 また、ARM デバイスからのマネージド アプリのダンプ ファイルもデバッグできますが、これはネイティブ デバッガーでのみ可能です。  
  
- Visual Studio 2013 で [カーネルモード](https://msdn.microsoft.com/library/windows/hardware/ff551880.aspx) のダンプファイルをデバッグするには、 [Windows 用デバッグツールの Windows 8.1 バージョン](https://msdn.microsoft.com/windows/hardware/gg463009)をダウンロードします。 「 [Visual Studio でのカーネルデバッグ」を](https://msdn.microsoft.com/library/windows/hardware/jj149675.aspx)参照してください。  
  
- Visual Studio では、 [フルユーザーモードダンプ](/windows-hardware/drivers/debugger/user-mode-dump-files#full)と呼ばれる以前のダンプ形式で保存されたダンプファイルをデバッグすることはできません。 フル ユーザー モード ダンプがヒープ情報ありのダンプとは異なることに注意してください。  
  
- Visual Studio で [SOS.dll (SOS デバッガー拡張)](https://msdn.microsoft.com/library/9ac1b522-77ab-4cdc-852a-20fcdc9ae498) を使用してデバッグするには、Windows Driver KIT (WDK) の一部である Windows 用デバッグツールをインストールする必要があります。 「 [Windows 8.1 Preview: キット、bits、ツールのダウンロード](https://msdn.microsoft.com/library/windows/hardware/bg127147.aspx)」を参照してください。  
  
  ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="create-a-dump-file"></a><a name="BKMK_Create_a_dump_file"></a> ダンプ ファイルを作成する  
 Visual Studio でダンプ ファイルを作成するには:   
  
- Visual Studio でのプロセスのデバッグ中、デバッガーが例外またはブレークポイントで停止するときに、ダンプ ファイルを保存できます。 [ **ダンプに名前を付けて保存**] を **選択します**。 [名前を付け **てダンプを保存** ] ダイアログボックスの [ **ファイルの種類** ] ボックスの一覧で、[ **ミニダンプ** ] または [ **ヒープ付きミニダンプ** ] (既定値) を選択できます。  
  
- [Just-in-time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)を有効にすると、デバッガーの外部で実行されているクラッシュしたプロセスにデバッガーをアタッチし、ダンプファイルを保存できます。 「[実行中のプロセスへのアタッチ」を](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)参照してください。  
  
  Windows ミニダンプ形式をサポートするプログラムでもダンプ ファイルを作成できます。 たとえば、 [Windows Sysinternals](https://technet.microsoft.com/sysinternals/default)の**Procdump**コマンドラインユーティリティでは、トリガーまたはオンデマンドに基づいてプロセスクラッシュダンプファイルを作成できます。 他のツールを使用したダンプファイルの作成の詳細については、このトピックの「 [要件と制限事項](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations) 」を参照してください。  
  
  ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="open-a-dump-file"></a><a name="BKMK_Open_a_dump_file"></a> ダンプ ファイルを開く  
  
1. Visual Studio で、[ **ファイル**]、[ **開く**]、[ **ファイル**] の順に選択します。  
  
2. **[ファイルを開く]** ダイアログ ボックスで、ダンプ ファイルを探して選択します。 通常は拡張子 .dmp が付いています。 次に **[OK]** を選択します。  
  
3. [ **ダンプファイルの概要** ] ウィンドウが表示されます。 このウィンドウでは、ダンプ ファイルのデバッグに関する概要情報を確認し、シンボル パスを設定したりデバッグを開始したりすることができます。概要情報をクリップボードにコピーすることもできます。  
  
     ![ミニダンプ概要ページ](../debugger/media/dbg-dump-summarypage.png "DBG_DUMP_SummaryPage")  
  
4. デバッグを開始するには、[ **アクション** ] セクションにアクセスし、[ **ネイティブのみでデバッグ** ] または [ **混合でデバッグ**] を選択します。  
  
## <a name="find-binaries-symbol-pdb-files-and-source-files"></a><a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> バイナリ、シンボル (.pdb) ファイル、ソースファイルを検索する  
 Visual Studio でダンプ ファイルのデバッグ機能をすべて使用するには、次のファイルにアクセスできる必要があります。  
  
- ダンプの作成に使用した .exe ファイルと、ダンプ プロセスで使用したその他のファイルおよびバイナリ (DLL など)。  
  
   ヒープ情報ありのダンプをデバッグする場合、Visual Studio は、一部のモジュールにバイナリ ファイルが欠落している状況にも対処できますが、有効な呼び出し履歴を生成できる十分なモジュールのバイナリがあることが必要です。 Visual Studio は、ネイティブ モジュールのバイナリをヒープ情報ありのダンプ ファイルに保存します。  
  
- .exe およびその他のバイナリのシンボル (.pdb) ファイル。  
  
- 目的のモジュールのソース ファイル。  
  
   実行可能ファイルと .pdb ファイルは、ダンプの作成時に使用したものと、バージョンおよびビルドが正確に一致している必要があります。  
  
   ソース ファイルを見つけることができない場合は、モジュールの逆アセンブルを使用してデバッグできます。  
  
  **実行可能ファイルの既定の検索パス**  
  
  Visual Studio では、ダンプ ファイルに含まれていない実行可能ファイルが次の場所で自動的に検索されます。  
  
1. ダンプ ファイルが格納されているディレクトリ。  
  
2. ダンプ ファイルで指定されたモジュールのパス。 これは、ダンプが収集されたコンピューター上のモジュール パスです。  
  
3. [Visual Studio**ツール**] の [**オプション**] ダイアログボックスの [**デバッグ**]、[**オプション**]、[**シンボル**] ページで指定したシンボルパス。 検索する複数の場所をこのページで追加できます。  
  
   **[バイナリが見つかりません]、[シンボルが見つかりません]、[ソースが見つかりません] のページの使用**  
  
   ダンプでモジュールをデバッグするために必要なファイルが見つからない場合は、適切なページが表示されます (**バイナリが見つからない**か、 **シンボルが見つから**ないか、 **ソースが見つかり**ません)。 これらのページでは、問題の原因に関する詳細な情報が表示され、ファイルの正しい場所を特定するために役立つアクション リンクも表示されます。 「 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」を参照してください。  
  
   ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="see-also"></a>参照  
 [Just-in-time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [IntelliTrace](../debugger/intellitrace.md)
