---
title: '方法: .NET Framework ソースをデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 49b13b8406dc96e8e7ebe5e79e26c5da02e8a53a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205440"
---
# <a name="how-to-debug-net-framework-source"></a>方法 : .NET Framework ソースをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

最新バージョンのには、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッグのための新機能が用意されて [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] います。 ソースをデバッグするには [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 、コードのデバッグシンボルにアクセスできる必要があります。 また、ソースへのステップインを有効にする必要もあり [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。  
  
 [ [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] **オプション** ] ダイアログボックスで、ステップ実行およびシンボルのダウンロードを有効にすることができます。 シンボルのダウンロードを有効にする場合は、シンボルを即時にダウンロードするのか、後でダウンロードするのかを選択できます。 シンボルを即時にダウンロードしない場合、次にアプリケーションのデバッグを開始するときにシンボルはダウンロードされます。 また、[ **モジュール** ] ウィンドウまたは [ **呼び出し履歴** ] ウィンドウから手動でダウンロードすることもできます。  
  
### <a name="to-enable-net-framework-source-debugging"></a>.NET Framework ソースのデバッグを有効にするには  
  
1. **[ツール]** メニューの **[オプション]** をクリックします。  
  
2. [ **オプション** ] ダイアログボックスで、[ **デバッグ** ] カテゴリをクリックします。  
  
3. **[全般**] ボックスで、[.NET Framework ソースのステップ実行**を有効にする**] を設定します。  
  
    1. [マイ コードのみ] が有効だった場合、[マイ コードのみ] が無効になったことを示す警告ダイアログ ボックスが表示されます。 **[OK]** をクリックします。  
  
    2. シンボル キャッシュの場所が設定されていない場合は、既定のシンボル キャッシュの場所が設定されたことを示す別の警告ダイアログ ボックスが表示されます。 **[OK]** をクリックします。  
  
4. [ **デバッグ** ] カテゴリの [ **シンボル**] をクリックします。  
  
5. シンボル キャッシュの場所を変更する場合:   
  
    1. 左側のボックスで [ **デバッグ** ] ノードを開きます。  
  
    2. [ **デバッグ** ] ノードで、[ **シンボル**] をクリックします。  
  
    3. **シンボルサーバーからこのディレクトリにキャッシュシンボル**内の場所を編集するか、[**参照**] をクリックして場所を選択します。  
  
6. シンボルをすぐにダウンロードする場合は、[ **上記の場所を使用してシンボルを読み込む**] をクリックします。  
  
     このボタンはデザイン モードでは使用できません。  
  
     シンボルを即時にダウンロードしない場合、次にプログラムのデバッグを開始するときにシンボルは自動的にダウンロードされます。  
  
7. **[OK]** をクリックして、 **[オプション]** ダイアログ ボックスを閉じます。  
  
### <a name="to-load-framework-symbols-using-the-modules-window"></a>[モジュール] ウィンドウを使用して Framework シンボルを読み込むには  
  
1. [ **モジュール** ] ウィンドウで、シンボルが読み込まれていないモジュールを右クリックします。 シンボルが読み込まれているかどうかを判断するには、[ **シンボルの状態** 列を参照します。  
  
2. [ **シンボルの読み込み元** ] をポイントし、[ **microsoft シンボルサーバー** ] をクリックして microsoft パブリックシンボルサーバーまたは **シンボルパス** からシンボルをダウンロードし、以前にシンボルを格納したディレクトリから読み込みます。  
  
### <a name="to-load-framework-symbols-using-the-call-stack-window"></a>[呼び出し履歴] ウィンドウを使用して Framework シンボルを読み込むには  
  
1. [ **呼び出し履歴** ] ウィンドウで、シンボルが読み込まれていないフレームを右クリックします。 フレームが淡色表示されます。  
  
2. [ **シンボルの読み込み元** ] をポイントし、[ **Microsoft シンボルサーバー** ] または [ **シンボルパス**] をクリックします。  
  
## <a name="see-also"></a>参照  
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
