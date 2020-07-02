---
title: IntelliTrace の機能 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- IntelliTrace, debugging with events
- IntelliTrace, recording execution history
- debugging [Visual Studio ALM], recording execution history
- IntelliTrace, turn off
- IntelliTrace, navigating event and call history
- IntelliTrace, saving your session
- IntelliTrace, enabling
- IntelliTrace, start debugging
- IntelliTrace, debugging with events and call information
- IntelliTrace, disabling
- IntelliTrace, turn on
- debugging [Visual Studio ALM], IntelliTrace
ms.assetid: 5ccc059c-6097-46b4-9d4b-34236c02d549
caps.latest.revision: 73
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e386277c56f7da50e55e077620cbf649ec6a0c9e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546251"
---
# <a name="intellitrace-features"></a>IntelliTrace の機能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IntelliTrace を使用すると、イベントとアプリケーションを呼び出すメソッドとを記録することができます。この機能により、さまざまな実行ポイントでの状態 (呼び出し履歴およびローカル変数の値) を確認することができます。 通常どおりのデバッグの開始 - 既定では、IntelliTrace はオンになっています。このため、IntelliTrace が記録する情報が **[イベント]** タブの新しい **[診断ツール]** ウィンドウに表示されます。イベントについて記録された呼び出し履歴とローカルを確認するには、目的のイベントを選択し、 **[デバッグ履歴の有効化]** をクリックします。  
  
 詳細な手順については、[チュートリアル: IntelliTrace の使用](../debugger/walkthrough-using-intellitrace.md)に関するページを参照してください。  
  
 IntelliTrace は Visual Studio Enterprise Edition で使用できますが、Visual Studio Professional Edition または Community Edition では使用できません。  
  
 IntelliTrace が有効になっていることを確認するには、[**ツール]/[オプション]/[intellitrace**オプション] ページを開きます。 **[IntelliTrace を有効にする]** は既定でオンになります。  
  
> [!NOTE]
> **[IntelliTrace]** オプション ページ上のすべての設定の適用範囲は、個々のプロジェクトまたはソリューションではなく、Visual Studio 全体となります。 これらの設定に加えた変更は、Visual Studio のすべてのインスタンス、すべてのデバッグ セッション、あるいはすべてのプロジェクトまたはソリューションに適用されます。  
  
## <a name="choose-the-events-that-intellitrace-records"></a><a name="ChooseEvents"></a>IntelliTrace が記録するイベントを選択します  
 特定の IntelliTrace イベントの記録はオンまたはオフにすることができます。  
  
 デバッグ中の場合、デバッグを停止します。 [**ツール]、[オプション]、[intellitrace**]、[intellitrace イベント] の順に選択します。 IntelliTrace で記録するイベントを選択します。  
  
## <a name="collect-intellitrace-events-and-call-information"></a><a name="GoingFurther"></a>IntelliTrace イベントと呼び出し情報の収集  
 このオプションは既定では有効になっていませんが、IntelliTrace ではイベントと共にメソッドの呼び出しを記録できます。 メソッド呼び出しの収集を有効にするには、[ツール]、[オプション]、[IntelliTrace]、 **[全般**] の順に選択し、[ **intellitrace イベントと呼び出し情報**] を選択します。  
  
 これにより、呼び出し履歴が表示され、コード内で呼び出しの前後を移動できるようになります。 IntelliTrace は、メソッド名、メソッド エントリ、および終了ポイントなどのデータと、特定のパラメーター値および戻り値を記録します。  
  
> [!TIP]
> このオプションは既定では有効になっていません。かなりのオーバーヘッドが追加されるためです。 IntelliTrace はアプリケーションが行うすべてのメソッド呼び出しを先に取得する必要があるだけでなく、それを画面に表示したりディスクに保存したりする上で大量のデータ セットを処理する必要があります。  
>   
> パフォーマンスのオーバーヘッドは、IntelliTrace で記録するイベントの一覧を制限することで、さらに収集するモジュール数を最小限に抑えることで、減らすことができます。 詳細については、「[IntelliTrace が呼び出し情報をどの程度記録するかの制御](../debugger/intellitrace-features.md#ControlCallData)」を参照してください。  
  
### <a name="using-the-navigation-gutter"></a>ナビゲーション余白を使用する  
 コード ウィンドウの左側に表示されるナビゲーション余白を使用することができます。 ナビゲーション余白が表示されない場合は、[ツール]、[オプション]、[IntelliTrace]、 **[詳細設定**] の順に移動し、[**デバッグモードでナビゲーション余白を表示**する] を選択します。  
  
 ナビゲーション余白を使用すれば、デバッグ履歴モードでメソッド呼び出しとイベントの中を前後に移動することができます。 デバッグ履歴の詳細については、「[デバッグ履歴](../debugger/historical-debugging.md)」を参照してください。 以下のようなコマンドがあります。  
  
|名前|説明|  
|-|-|  
|**デバッガー コンテキストをここに設定**|これが表示される呼び出しタイム フレームにデバッグ コンテキストを設定します。<br /><br /> このアイコンは、現在の呼び出し履歴にのみ表示されます。|  
|**呼び出しサイトに戻る**|ポインターとデバッグ コンテキストを現在の関数が呼び出された場所に戻します。<br /><br /> ライブ デバッグ モードの場合は、このコマンドでデバッグ履歴をオンにします。 元の実行中断場所に戻ると、デバッグ履歴はオフになり、ライブ デバッグがオンになります。|  
|**前の呼び出しまたは IntelliTrace イベントへ移動**|ポインターとデバッグ コンテキストを前の呼び出しまたはイベントに戻します。<br /><br /> ライブ デバッグ モードの場合は、このコマンドでデバッグ履歴をオンにします。|  
|**ステップ イン**|現在選択されている関数にステップインします。<br /><br /> このコマンドは、デバッグ履歴モード中にのみ使用できます。|  
|**次の呼び出しまたは IntelliTrace イベントへ移動**|ポインターとデバッグ コンテキストを IntelliTrace データが存在する次の呼び出しまたはイベントまで進めます。<br /><br /> このコマンドは、デバッグ履歴モード中にのみ使用できます。|  
|**ライブ モードへ移動**|ライブ デバッグ モードに戻ります。|  
  
### <a name="search-for-a-line-or-method-in-intellitrace"></a>行またはメソッドを IntelliTrace で検索する  
 メソッドを検索できるのは、メソッド呼び出し情報が有効になっている場合に限られます。 特定の行またはメソッドの IntelliTrace 履歴を検索することができます。 デバッガーの実行が停止したら、関数本文内を右クリックしてコンテキスト メニューを表示し、 **[この行を IntelliTrace で検索]** または **[このメソッドを IntelliTrace で検索]** のいずれかをクリックします。  
  
### <a name="control-how-much-call-information-intellitrace-records"></a><a name="ControlCallData"></a>IntelliTrace が呼び出し情報をどの程度記録するかの制御  
 既定では、IntelliTrace はソリューションで使用されるすべてのモジュールについて情報を記録します。 関心のあるモジュールに関してのみ、呼び出し情報を記録するように IntelliTrace を設定できます。 [**ツール**]、[オプション]、[intellitrace]、[モジュール] で、含めるモジュール、または intellitrace から除外するモジュールを指定できます。 指定したモジュールから発生したイベントと、関心のあるモジュール内で発生したメソッド呼び出しだけが IntelliTrace で収集されます。  
  
 複数のモジュールを追加するには、ワイルドカード文字 * を文字列の先頭または末尾に使用します。 モジュール名には、アセンブリ名ではなくファイル名を使用してください。 ファイル パスは使用できません。  
  
 モジュールの数は最小限に抑えるようにしてください。 そうすれば、収集するデータが少なくなるので、パフォーマンスが向上します。 また、処理すべきデータが少なくなるので、UI のノイズが減少します。  
  
## <a name="saving-intellitrace-data-to-file"></a><a name="SaveSession"></a>IntelliTrace データをファイルに保存しています  
 デバッグ中にアプリケーションが中断状態になっている間に、IntelliTrace によって収集されたデータを [**デバッグ]/[intellitrace]/[Intellitrace セッションの保存**] に保存できます。 アプリケーションがまだ実行中の場合またはデバッグが停止状態の場合、メニュー項目は無効であるため、IntelliTrace で収集されたデータを保存することはできません。  
  
 ファイルに自動的に保存されるように IntelliTrace を構成するには、[**ツール]、[オプション]、[intellitrace]、[詳細設定**] の順に移動し、[ **intellitrace 記録をこのディレクトリに格納**する] を選択します。 生成するファイルの設定サイズを構成することもできます。その場合、IntelliTrace は領域が足りなくなると古いデータから順に上書きしていきます。 Visual Studio では、ファイルが自動保存されるときと Visual Studio のホスティング プロセス (vshost.exe) をオンにしたときに、IntelliTrace セッションごとに 2 つのファイルが作成されます。  
  
> [!TIP]
> ファイルが必要なくなった場合は、ディスク領域を節約するためにファイルの保存を自動的にオフにします。 既存のファイルは削除されません。 いつでも必要に応じてコンテキスト メニューからファイルに保存することができます。  
  
 IntelliTrace データをファイルに保存する場合は、IntelliTrace が収集対象としたプロセスごとに 1 つの .itrace ファイルが得られます。 次に、Visual Studio で [ファイル]、[開く]、[**ファイル**] の順に移動し、[ファイルを開く] ダイアログボックスで itrace ファイルを選択して、itrace ファイルを開きます。 詳細については、「[保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)」を参照してください。  
  
## <a name="blogs"></a>ブログ  
 [IntelliTrace in Visual Studio Enterprise 2015 (Visual Studio Enterprise2015 の IntelliTrace)](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)  
  
 [Visual Studio 2015 (テキスト エディター) で IntelliTrace を使用したライブ デバッグのチュートリアル](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor/)  
  
 [Visual Studio 2015 (Social Club) で IntelliTrace を使用したライブ デバッグのチュートリアル](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club/)  
  
 [Visual Studio Enterprise 2015 の IntelliTrace でアタッチがサポートするようになりました](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach/)  
  
 [IntelliTrace スタンドアロン コレクターを使用して Windows サービスからデータを収集する](https://devblogs.microsoft.com/devops/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector/)  
  
 [IntelliTrace コレクション プランの編集](https://devblogs.microsoft.com/devops/editing-the-intellitrace-collection-plan/)  
  
 [IntelliTrace を使用したカスタム TraceSource およびデバッグ](https://devblogs.microsoft.com/devops/custom-tracesource-and-debugging-using-intellitrace/)  
  
 [Active Directory アカウントで実行されている IntelliTrace スタンドアロン コレクターとアプリケーション プール](https://devblogs.microsoft.com/devops/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts/)  
  
## <a name="forums"></a>フォーラム  
 [Visual Studio デバッガー](https://social.msdn.microsoft.com/Forums/vsdebug)  
  
## <a name="videos"></a>ビデオ  
 [IntelliTrace のエクスペリエンス](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)  
  
 [Historical Debugging with IntelliTrace in Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/events/Ignite/2015/BRK3716)
