---
title: '方法: [モジュール] ウィンドウを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.modules
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
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b592515692e23dce49c125c7895bd158904b653f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696128"
---
# <a name="how-to-use-the-modules-window"></a>方法 : [モジュール] ウィンドウを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> この機能は、SQL またはスクリプトのデバッグでは使用できません。  
  
 [ **モジュール** ] ウィンドウには、プログラムで使用される DLL と EXE が一覧表示され、それぞれに関連する情報が表示されます。  
  
### <a name="to-display-the-modules-window-in-break-mode-or-in-run-mode"></a>[モジュール] ウィンドウを表示するには (中断モードまたは実行モードの場合)  
  
- [ **デバッグ** ] メニューの [ **ウィンドウ**] をポイントし、[ **モジュール**] をクリックします。  
  
     既定では、 **[モジュール]** ウィンドウには、モジュールが読み込み順に表示されます。 ただし、基準列を指定して並べ替えるように選択できます。  
  
### <a name="to-sort-by-any-column"></a>基準列を指定して並べ替えるには  
  
- 列の上部にあるボタンをクリックします。  
  
     ショートカットメニューを使用して、[ **モジュール** ] ウィンドウからシンボルを読み込んだり、シンボルパスを指定したりすることができます。  
  
## <a name="loading-symbols"></a>シンボルの読み込み  
 [ **モジュール** ] ウィンドウでは、デバッグシンボルが読み込まれているモジュールを確認できます。 この情報は、[ **シンボルの状態** 列に表示されます。 状態が "スキップ" と表示されている場合、 **PDB ファイルが見つからないか、開くことができません**。また、 **include/exclude 設定によって無効になって**いる場合は、Microsoft パブリックシンボルサーバーからシンボルをダウンロードしたり、コンピューターのシンボルディレクトリからシンボルを読み込んだりするように、デバッガーに指示できます。 詳細については、「[シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」を参照してください。  
  
#### <a name="to-load-symbols-manually"></a>シンボルを手動で読み込むには  
  
1. [ **モジュール** ] ウィンドウで、シンボルが読み込まれていないモジュールを右クリックします。  
  
2. [ **シンボルの読み込み元** ] をポイントし、[ **Microsoft シンボルサーバー** ] または [ **シンボルパス**] をクリックします。  
  
#### <a name="to-change-symbol-load-settings"></a>シンボル読み込みの設定を変更するには  
  
1. **[モジュール]** ウィンドウで、任意のモジュールを右クリックします。  
  
2. [ **シンボルの設定**] をクリックします。  
  
     シンボルの読み込み設定を変更できるようになりました。詳細については、「 [シンボルの場所と読み込み動作を指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)する」を参照してください。 変更内容は、デバッグ セッションを再起動しないと有効になりません。  
  
#### <a name="to-change-symbol-load-behavior-for-a-specific-module"></a>特定のモジュールのシンボル読み込み動作を変更するには  
  
1. **[モジュール]** ウィンドウで、モジュールを右クリックします。  
  
2. [ **シンボルの自動読み込みの設定** ] をポイントし、[ **常に手動で読み込む** ] または [ **既定値**] をクリックします。 変更内容は、デバッグ セッションを再起動しないと有効になりません。  
  
## <a name="see-also"></a>参照  
 [実行の中断](https://msdn.microsoft.com/30fc4643-f337-4651-b1ff-f2de2c098d40)   
 [デバッガーでのデータの表示](../debugger/viewing-data-in-the-debugger.md)   
 [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
