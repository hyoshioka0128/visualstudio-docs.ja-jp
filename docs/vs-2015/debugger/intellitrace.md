---
title: IntelliTrace |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.overview
helpviewer_keywords:
- debugger, recording execution history
- debugging, recording execution history
- IntelliTrace [Visual Studio ALM]
- IntelliTrace, debugging applications
- debugger, (See also IntelliTrace [Visual Studio ALM])
- debugging, (See also IntelliTrace [Visual Studio ALM])
- IntelliTrace, collecting data from Test Manager
- IntelliTrace
- Test Manager, debugging with IntelliTrace
- IntelliTrace, debugging after a crash
ms.assetid: 486bfec2-39bd-4d78-892a-42352128ee52
caps.latest.revision: 142
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a3a3e68874bb3295f6696bbdadb3c470a7f2a4ad
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586626"
---
# <a name="intellitrace"></a>[IntelliTrace]
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンについては、「 [IntelliTrace](/visualstudio/debugger/intellitrace) 」を参照してください。  
  
IntelliTrace を使用して実行履歴を記録およびトレースすると、アプリのデバッグにかかる時間を短縮できます。 IntelliTrace には以下の機能があるので、バグを簡単に見つけることができます。  
  
- 特定のイベントを記録する  
  
   関連するコード、デバッガー イベント中に **[ローカル]** ウィンドウに表示されるデータ、および関数呼び出し情報を確認する  
  
- 再現が困難な場合、または配置で発生する場合のエラーをデバッグする  
  
  IntelliTrace は Visual Studio Enterprise Edition で使用できます (Professional Edition または Community Edition の場合は使用できません)。  
  
## <a name="what-do-you-want-to-do"></a>目的に合ったトピックをクリックしてください  
  
|||  
|-|-|  
|**IntelliTrace を使用してアプリケーションをデバッグする:**<br /><br /> -過去のイベントを表示します。<br />-過去のイベントを含む呼び出し情報を表示します。<br />-IntelliTrace セッションを保存します。<br />-IntelliTrace が収集するデータを制御します。|-   [チュートリアル: IntelliTrace の使用](../debugger/walkthrough-using-intellitrace.md)<br />     [IntelliTrace の機能](../debugger/intellitrace-features.md)<br />-   [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)<br />-   [デバッグ履歴](../debugger/historical-debugging.md)|  
|**テスト マネージャーのテスト セッション中に IntelliTrace データを収集する**|-   [手動テストでのその他の診断データの収集](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2)|  
|**展開されたアプリケーションから IntelliTrace データを収集する**|-   [IntelliTrace スタンドアロンコレクターの使用](../debugger/using-the-intellitrace-stand-alone-collector.md)|  
|**IntelliTrace ログ ファイル (.iTrace ファイル) からデバッグを開始する**|-   [保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)|  
  
## <a name="what-apps-can-i-debug-with-intellitrace"></a><a name="IntelliTraceSupport"></a>IntelliTrace を使用してデバッグできるアプリ  
  
|||  
|-|-|  
|**サポートされています**|-.NET Framework 2.0 以降のバージョンを使用する Visual Basic および Visual C# アプリケーション。<br />     ASP.NET、Microsoft Azure、Windows フォーム、WCF、WPF、Windows Workflow、SharePoint 2010、SharePoint 2013、および 64 ビットのアプリを含むほとんどのアプリケーションをデバッグできます。<br />     IntelliTrace を使用して SharePoint アプリケーションをデバッグする方法については、「[チュートリアル: Intellitrace を使用した Sharepoint アプリケーションのデバッグ](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4)」を参照してください。<br />     IntelliTrace を使用して Microsoft Azure アプリをデバッグするには、「 [intellitrace および Visual Studio を使用した発行済みのクラウドサービスのデバッグ](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)」を参照してください。|  
|**制限付きサポート**|-F # アプリの実験ベース<br />-イベントのみがサポートされている Windows ストアアプリ|  
|**サポートされていない**|-C++、その他の言語、スクリプト<br />-Windows サービス、Silverlight、Xbox、また[!INCLUDE[winmobile](../includes/winmobile-md.md)]はアプリ|  
  
> [!NOTE]
> 既に実行されているプロセスをデバッグする場合は、IntelliTrace を使用できません。 プロセスの開始時に IntelliTrace を起動する必要があります。  
  
## <a name="why-debug-with-intellitrace"></a><a name="IntelliTraceVSTraditional"></a>IntelliTrace を使用してデバッグする理由  
 従来のデバッグまたは "*ライブ*" デバッグでは、ご利用のアプリケーションの現在の状態と過去のイベントの制限されたデータのみが表示されます。 アプリケーションの現在の状態に基づいてこれらのイベントを推測するか、またはアプリケーションを再実行することによってこれらのイベントを再作成する必要があります。  
  
 IntelliTrace は、これらの時点で特定のイベントやデータを記録することによってこの従来のデバッグを拡大します。 これにより、特にバグの箇所を通り越してステップ実行した場合に、再起動せずにこれらのアプリケーションで起こったことを確認できます。 IntelliTrace は従来のデバッグ中に既定で有効になっているため、自動的に非表示の状態でデータを収集します。 これにより、従来のデバッグと IntelliTrace デバッグを簡単に切り替えて、記録された情報を見ることができます。 「 [Intellitrace の機能](../debugger/intellitrace-features.md)」および「 [intellitrace が収集するデータ](#WhatData)」を参照してください。  
  
 また、IntelliTrace は再現が困難なエラーや配置で発生するエラーのデバッグに役立ちます。 IntelliTrace データを収集し、IntelliTrace ログ ファイル (.iTrace ファイル) に保存できます。 .iTrace ファイルには、例外、パフォーマンス イベント、Web 要求、テスト データ、スレッド、モジュール、およびその他のシステム情報に関する詳細情報が含まれています。 Visual Studio Enterprise でこのファイルを開き、項目を選択し、IntelliTrace でデバッグを開始できます。 これにより、ファイル内の任意のイベントに移動して、その時点のアプリケーションに関する特定の詳細を表示できます。  
  
 次のソースからの IntelliTrace データを保存できます。  
  
- Visual Studio 2015 Enterprise または以前のバージョンの Visual Studio Ultimate の IntelliTrace セッション。  
  
- Microsoft Test Manager のテスト セッション  
  
- Microsoft Monitoring Agent を単独、または System Center 2012 と連携して使用する場合の、IIS でホストされている ASP.NET Web アプリ、または配置されて実行中の SharePoint 2010 アプリケーションと SharePoint 2013 アプリケーション。 「 [IntelliTrace スタンドアロンコレクターの使用](../debugger/using-the-intellitrace-stand-alone-collector.md)」および「 [Microsoft Monitoring Agent での監視](https://technet.microsoft.com/library/dn465153.aspx)」を参照してください。  
  
  IntelliTrace を使用したデバッグがどのように役立つかの例を次に示します。  
  
- アプリケーションのデータ ファイルが破損していますが、このイベントの発生場所を特定できません。  
  
   IntelliTrace がなければ、コード全体を確認して可能性のあるファイルのアクセスをすべて見つけ、それらのアクセスにブレークポイントを設定してから、アプリケーションを再実行して、問題の発生箇所を探さなければなりません。 IntelliTrace を使用すると、各イベントが発生したときに収集されたアプリケーションに関するファイル アクセス イベントや特定の詳細をすべて表示できます。  
  
- 例外が発生します。  
  
   IntelliTrace がない場合、例外に関するメッセージが表示されますが、例外の原因となったイベントに関する詳細な情報はわかりません。 呼び出し履歴を調べて、例外の原因となった一連の呼び出しを確認することはできますが、それらの呼び出し中に発生したイベントのシーケンスを確認することはできません。 IntelliTrace を使用すると、例外の前に発生したイベントを確認できます。  
  
- アプリケーションは、テスト コンピューターではクラッシュしますが、開発用コンピューターでは正常に実行されます。  
  
   Microsoft Test Manager から IntelliTrace データを収集して、.iTrace ファイルにデータを保存し、後日確認できるようにこのファイルを Team Foundation Server の作業項目に添付することができます。 「[手動テストでのその他の診断データの収集](https://msdn.microsoft.com/library/bb5a2cc0-84f5-4dfe-9560-ca3d313aefd2)」および「[保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)」を参照してください。  
  
- 展開されたアプリケーションでバグまたはクラッシュが発生しています。  
  
   Microsoft Azure ベースのアプリケーションの場合、アプリケーションを発行する前に IntelliTrace データの収集を構成できます。 アプリケーションの実行中、IntelliTrace はデータを .iTrace ファイルに保存します。 [IntelliTrace および Visual Studio を使用した発行済みのクラウド サービスのデバッグ](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)に関するページを参照してください。  
  
   IIS 7.0、7.5、および 8.0 でホストされる ASP.NET Web アプリ、および SharePoint 2010 アプリケーションや SharePoint 2013 アプリケーションの場合、Microsoft Monitoring Agent を単独で、または System Center 2012 と連携して使用して、IntelliTrace データを .iTrace ファイルに保存できます。  
  
   これは、配置されたアプリの問題を診断する場合に便利です。 「 [IntelliTrace スタンドアロンコレクターの使用」を](../debugger/using-the-intellitrace-stand-alone-collector.md)参照してください。  
  
## <a name="what-data-does-intellitrace-collect"></a><a name="WhatData"></a> IntelliTrace が収集するデータ  
 **イベント情報の収集**  
  
 既定では、IntelliTrace は、IntelliTrace イベント (デバッガー イベント、例外、.NET Framework イベント、およびデバッグに役立つその他のシステム イベント) のみを記録します。 常に収集されるデバッガー イベントと例外を除き、収集する IntelliTrace イベントの種類を選択できます。 「 [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)」を参照してください。  
  
- **デバッガー イベント**  
  
   IntelliTrace は、Visual Studio デバッガーに発生するイベントを常に記録します。 たとえば、アプリケーションの起動はデバッガー イベントです。 その他のデバッガー イベントは、アプリケーションの実行を中断する停止イベントです。 たとえば、ご利用のプログラムはブレークポイントをヒットしたり、トレースポイントをヒットしたり、**[ステップ]** コマンドを実行したりします。  
  
   パフォーマンスを向上するため、IntelliTrace はデバッガー イベントのすべての値を記録しません。 代わりに、次の値を記録します。  
  
  - **[ローカル]** ウィンドウの値。 これらの値を確認するために **[ローカル]** ウィンドウを開いたままにします。  
  
  - **[自動変数]** ウィンドウが開いているときにのみ **[自動変数]** ウィンドウの値  
  
  - 値を表示するためにソース ウィンドウの変数の上にマウス ポインターを移動すると表示されるデータヒントの値。 IntelliTrace は、固定されたデータヒントの値は収集しません。  
  
- **例外**  
  
   IntelliTrace は、次のような種類の例外の種類とメッセージを記録します。  
  
  - 例外がスローおよびキャッチされた場合の処理済みの例外  
  
  - ハンドルされない例外  
  
- **.NET Framework イベント**  
  
   既定では、IntelliTrace は最も一般的な .NET Framework のイベントを記録します。 次に例を示します。  
  
  - ファイル アクセス イベントの場合、IntelliTrace はファイル名を収集します。  
  
  - チェック ボックスの確認イベントの場合、IntelliTrace はチェック ボックスの状態とテキストを収集します。  
  
- **SharePoint 2010 アプリケーション イベントと SharePoint 2013 アプリケーション イベント**  
  
   Visual Studio の外部で実行されている SharePoint 2010 アプリケーションと SharePoint 2013 アプリケーションのユーザー プロファイル イベントと Unified Logging System (ULS) イベントのサブセットを記録できます。 これらのイベントを .iTrace ファイルに保存できます。 Visual Studio Enterprise 2015、以前のバージョンの Visual Studio Ultimate、または**トレース**モードで実行されている[Microsoft Monitoring Agent](https://go.microsoft.com/fwlink/?LinkID=309771)が必要です。  
  
   .iTrace ファイルを開いたら、SharePoint 相関 ID を入力して対応する Web 要求を見つけ、記録されたイベントを表示し、特定のイベントからのデバッグを開始します。 ファイルにハンドルされない例外が含まれている場合は、相関 ID を選択して例外のデバッグを開始できます。  
  
   参照:  
  
  - [IntelliTrace スタンドアロン コレクターを使用する](../debugger/using-the-intellitrace-stand-alone-collector.md)  
  
  - [保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)  
  
  - [チュートリアル: IntelliTrace を使用した SharePoint アプリケーションのデバッグ](https://msdn.microsoft.com/library/4bd80d2f-f680-4bf4-81c3-f14e8185f6a4)  
  
  **関数呼び出し情報の収集**  
  
  関数の呼び出し情報を収集するように IntelliTrace を構成することができます。 この情報は、呼び出し履歴を表示したり、コードの呼び出しで前後に移動できます。 各関数呼び出しについて、IntelliTrace は次のデータを記録します。  
  
- 関数名  
  
- 関数のエントリ ポイントでパラメーターとして渡され、関数の終了ポイントで返されるプリミティブ データ型の値  
  
- 読み取りまたは変更されたときの自動プロパティの値  
  
- null かどうかの場合以外の値を除く、1 番目のレベルの子オブジェクトへのポインター  
  
> [!NOTE]
> IntelliTrace は、配列の最初の 256 個のオブジェクトと文字列の最初の 256 文字のみを収集します。  
  
 「 [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)」を参照してください。  
  
 **収集 (モジュール情報を)**  
  
 IntelliTrace で収集される呼び出し情報の量を制御するには、目的のモジュールのみを指定します。 これにより、収集時のアプリケーションのパフォーマンスを向上させることができます。 「 [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)」を参照してください。  
  
## <a name="will-intellitrace-slow-down-my-application"></a><a name="AffectPerformance"></a>IntelliTrace はアプリケーションの速度を低下させるか  
 既定では、選択された IntelliTrace イベントについてのみ情報が収集されます。 これが原因でアプリケーションの速度が低下するかどうかは、コードの構造と構成によって決まります。 たとえば、IntelliTrace がイベントを頻繁に記録する場合、アプリケーションの速度が低下する可能性があります。 また、アプリケーションのリファクタリングを検討する必要に迫られる場合があります。  
  
 呼び出し情報を収集すると、アプリケーションの速度が大幅に低下する可能性があります。 さらに、ディスクに保存される IntelliTrace ログ ファイル (.iTrace ファイル) のサイズが増加する可能性があります。 これらの影響を最小限に抑えるには、必要なモジュールのみから呼び出し情報を収集するようにします。  ご利用の .iTrace ファイルの最大サイズを変更するには、**[ツール]**、**[オプション]**、**[IntelliTrace]**、**[詳細設定]** の順に選択します。 「 [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [IntelliTrace の機能](../debugger/intellitrace-features.md)  
  
 [IntelliTrace の構成](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)  
  
 [診断トレース データへの再現が困難なバグの組み込み](https://msdn.microsoft.com/library/944ae9af-5a55-4c58-b520-0108c03b3564)  
  
 [配置後の問題の診断](../debugger/diagnose-problems-after-deployment.md)  
  
 [保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)  
  
### <a name="blogs"></a>ブログ  
 [Visual Studio ALM + Team Foundation Server](https://devblogs.microsoft.com/devops/welcome-to-the-visual-studio-alm-team-foundation-server-blog/)  
  
### <a name="forums"></a>フォーラム  
 [Visual Studio の診断](https://social.msdn.microsoft.com/Forums/vsdebug)
