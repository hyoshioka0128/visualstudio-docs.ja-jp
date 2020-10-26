---
title: '方法: [呼び出し履歴] ウィンドウを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.callstack
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- aspx
helpviewer_keywords:
- threading [Visual Studio], displaying calls to or from
- functions [debugger], viewing code on call stack
- disassembly code
- breakpoints, Call Stack window
- debugging [Visual Studio], switching to another stack frame
- debugging [Visual Studio], Call Stack window
- Call Stack window, viewing source code for functions on the call stack
- stack, switching stack frames
- Call Stack window, viewing disassembly code for functions on the call stack
ms.assetid: 5154a2a1-4729-4dbb-b675-db611a72a731
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 84c0bfead1633da13b4284cad04ace674045b057
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697483"
---
# <a name="how-to-use-the-call-stack-window"></a>方法 : [呼び出し履歴] ウィンドウを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[呼び出し履歴]** ウィンドウを使用すると、現在呼び出し履歴にある関数呼び出しやプロシージャ呼び出しを表示できます。  
  
 [ **呼び出し履歴** ] ウィンドウには、各関数の名前と、それが記述されているプログラミング言語が表示されます。 関数またはプロシージャ名に、モジュール名、行番号、パラメーター名、型、値などのオプション情報が追加される場合があります。 このオプション情報の表示は、オンとオフを切り替えることができます。  
  
 黄色の矢印は、現在、実行ポインターが存在するスタック フレームを示します。 既定では、これは、[ソース]、[ **逆アセンブリ**]、[ **ローカル**]、[ **ウォッチ**]、および [ **自動変数** ] の各ウィンドウに情報が表示されるフレームです。 コンテキストをスタック上の別のフレームに変更する場合は、[ **呼び出し履歴** ] ウィンドウで実行できます。  
  
 コールスタックの一部でデバッグシンボルを使用できない場合 **、呼び出し履歴ウィンドウで** は、呼び出し履歴のその部分に関する正しい情報を表示できないことがあります。 次のような出力が表示されます。  
  
 [下のフレームは間違っているか、または見つかりません。name.dll に対して読み込まれたシンボルはありません。]  
  
 マネージコードでは、既定でになります。 [ **呼び出し履歴** ] ウィンドウでは、非ユーザーコードの情報が非表示になります。 非表示情報の代わりに次のような出力が表示されます。  
  
 **[\<External Code>]**  
  
 非ユーザー コードとは "マイ コード" 以外のすべてのコードです。ショートカット メニューを使用して非ユーザー コードの呼び出し履歴情報を表示することもできます。  
  
 ショートカット メニューを使用することにより、スレッド間の呼び出しを表示するかどうかを選択できます。  
  
> [!NOTE]
> 使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-display-the-call-stack-window-in-break-mode-or-in-run-mode"></a>[呼び出し履歴] ウィンドウを表示するには (中断モードまたは実行モードの場合)  
  
- [ **デバッグ** ] メニューの [ **ウィンドウ** ] をポイントし、[ **呼び出し履歴**] をクリックします。  
  
### <a name="to-change-the-optional-information-displayed"></a>表示されるオプション情報を変更するには  
  
- [**呼び出し履歴**] ウィンドウを右クリックし、[**表示 \<**_the information that you want_**> **] を設定またはオフにします。  
  
### <a name="to-display-non-user-code-frames-in-the-call-stack-window"></a>[呼び出し履歴] ウィンドウで非ユーザー コードのフレームを表示するには  
  
- **[呼び出し履歴]** ウィンドウを右クリックし、 **[外部コードの表示]** をクリックします。  
  
### <a name="to-switch-to-another-stack-frame"></a>別のスタック フレームに切り替えるには  
  
1. [ **呼び出し履歴** ] ウィンドウで、表示するコードとデータが含まれているフレームを右クリックします。  
  
2. **[フレームに切り替え]** をクリックします。  
  
     巻いた尾の付いた緑色の矢印が、選択したフレームの横に表示されます。 実行ポインターは、黄色の矢印でマークされた元のフレームに置かれたままです。 **[デバッグ]** メニューの **[ステップ]** または **[続行]** をクリックすると、選択したフレームではなく、元のフレームで実行が継続されます。  
  
### <a name="to-display-calls-to-or-from-another-thread"></a>別のスレッドとの間の呼び出しを表示するには  
  
- **[呼び出し履歴]** ウィンドウを右クリックし、 **[他のスレッドの呼び出しを含む]** をクリックします。  
  
### <a name="to-view-the-source-code-for-a-function-on-the-call-stack"></a>呼び出し履歴上の関数のソース コードを表示するには  
  
- **[呼び出し履歴]** ウィンドウで、ソース コードを表示する関数を右クリックし、 **[ソース コードへ移動]** をクリックします。  
  
### <a name="to-visually-trace-the-call-stack"></a>呼び出し履歴を視覚的にトレースするには  
  
1. **[呼び出し履歴]** ウィンドウでショートカット メニューを開きます。 [ **コードマップの呼び出し履歴を表示**] をクリックします。 (キーボード: **CTRL**  + **SHIFT**  +  **`** )  
  
     「 [デバッグ中の呼び出し履歴のメソッドのマップ」を](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)参照してください。  
  
### <a name="to-view-the-disassembly-code-for-a-function-on-the-call-stack"></a>呼び出し履歴上の関数の逆アセンブリ コードを表示するには  
  
- **[呼び出し履歴]** ウィンドウで、逆アセンブリ コードを表示する関数を右クリックし、 **[逆アセンブルを表示]** をクリックします。  
  
### <a name="to-run-to-a-specific-function-from-the-call-stack-window"></a>[呼び出し履歴] ウィンドウで特定の関数までを実行するには  
  
- [ **呼び出し履歴** ] ウィンドウで関数を選択し、右クリックして、[ **カーソル行の前まで実行**] を選択します。  
  
### <a name="to-set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>関数呼び出しの終了ポイントにブレークポイントを設定するには  
  
- [呼び出し履歴関数にブレークポイントを設定する](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_the_call_stack_window)に関するセクションを参照してください。  
  
### <a name="to-load-symbols-for-a-module"></a>モジュールのシンボルを読み込むには  
  
- [ **呼び出し履歴** ] ウィンドウで、再読み込みするシンボルがあるモジュールが表示されているフレームを右クリックし、[ **シンボルの読み込み**] を選択します。  
  
## <a name="loading-symbols"></a>シンボルの読み込み  
 **[呼び出し履歴]** ウィンドウで、シンボルがまだ読み込まれていないコードに対してデバッグ シンボルを読み込むことができます。 これらのシンボルには、Microsoft のパブリック シンボル サーバーからダウンロードされる .NET Framework シンボルやシステム シンボル、または、デバッグしているコンピューター上のシンボル パス内のシンボルを指定できます。  
  
 [シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事をご覧ください。  
  
#### <a name="to-load-symbols"></a>シンボルを読み込むには  
  
1. [ **呼び出し履歴** ] ウィンドウで、シンボルが読み込まれていないフレームを右クリックします。 フレームが淡色表示されます。  
  
2. [ **シンボルの読み込み元** ] をポイントし、[ **Microsoft シンボルサーバー** ] または [ **シンボルパス**] をクリックします。  
  
#### <a name="to-set-the-symbol-path"></a>シンボル パスを設定するには  
  
1. **[呼び出し履歴]** ウィンドウで、ショートカット メニューの **[シンボルの設定]** をクリックします。  
  
     **[オプション]** ダイアログ ボックスが表示され、 **[シンボル]** ページが表示されます。  
  
2. [ **シンボルの設定**] をクリックします。  
  
3. **[オプション]** ダイアログ ボックスで、フォルダー アイコンをクリックします。  
  
     **[シンボル ファイル (.pdb) の場所]** ボックスにカーソルが表示されます。  
  
4. デバッグしているコンピューター上のシンボルの場所へのディレクトリ パス名を入力します。 ローカル デバッグの場合、これはローカル コンピューターです。 リモート デバッグの場合、これはリモート コンピューターです。  
  
5. **[OK]** をクリックして、 **[オプション]** ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [[呼び出し履歴] ウィンドウの混合コードと不足情報](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)   
 [方法: デバッガーウィンドウの数値書式を変更する](https://msdn.microsoft.com/library/cd593847-a625-411d-a430-b798346ef18f)   
 [デバッガーでのデータの表示](../debugger/viewing-data-in-the-debugger.md)   
 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [ブレークポイントの使用](../debugger/using-breakpoints.md)
