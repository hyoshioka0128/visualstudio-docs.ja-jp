---
title: '方法: 並列ウォッチウィンドウを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelwatch
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel watch window
ms.assetid: 28004d9b-420c-48f7-b80e-ab1519802558
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 734a55cb06ee46afc6fc3518d6dffe349690d3d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697490"
---
# <a name="how-to-use-the-parallel-watch-window"></a>方法: 並列ウォッチ ウィンドウを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[並列ウォッチ] ウィンドウには、複数のスレッドで 1 つの式が保持している値を同時に表示できます。 各行は、1 つのアプリケーションで実行中のスレッドを表しますが、スレッドは複数の行に表示される場合があります。 具体的には、各行は関数シグネチャが現在のスタック フレーム上の関数に一致する関数呼び出しを表します。 列内の項目の並べ替え、順序変更、削除、およびグループ化を行うことができます。 スレッドのフラグ設定、フラグ解除、凍結 (中断)、および凍結解除 (再開) を実行できます。 **[並列ウォッチ]** ウィンドウには次の列が表示されます。  
  
- フラグ列。特に注意する必要のあるスレッドをマークできます。  
  
- フレーム列。矢印は、選択したフレームを示します。  
  
- 構成可能な列。コンピューター、プロセス、タイル、タスク、スレッドを表示できます。  
  
  > [!TIP]
  > [並列**ウォッチ**] ウィンドウにタスク情報を表示するには、[**並列タスク**] ウィンドウを開く必要があります。  
  
- **\<Add Watch>** 列。ウォッチする式を入力できます。  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-display-the-parallel-watch-window"></a>[並列ウォッチ] ウィンドウを表示するには  
  
1. コード内にブレークポイントを設定します。  
  
2. メニュー バーで、 **[デバッグ]** 、 **[デバッグ開始]** の順に選択します。 アプリケーションがブレークポイントに到達するを待機します。  
  
3. メニュー バーで、 **[デバッグ]** 、 **[ウィンドウ]** 、 **[並列ウォッチ]** の順にクリックして、ウォッチ ウィンドウを選択します。 最大で 4 つのウィンドウを開くことができます。  
  
### <a name="to-add-a-watch-expression"></a>ウォッチ式を追加するには  
  
- を選択 **\<Add Watch>** し、ウォッチ式を指定します。  
  
### <a name="to-flag-or-unflag-a-thread"></a>スレッドのフラグを設定または設定解除するには  
  
- 行の [フラグ] 列を選択するか、スレッドのショートカットメニューを開き、[ **フラグ** ] または [フラグ解除] を **選択します**。  
  
### <a name="to-display-only-flagged-threads"></a>フラグが設定されたスレッドのみ表示するには  
  
- [ **並列ウォッチ** ] ウィンドウの左上隅にある [フラグ付きののみ表示] ボタンをクリックします。  
  
### <a name="to-switch-frames"></a>フレームを切り替えるには  
  
- フレーム列をダブルクリックします  (キーボード:行を選択し、Enter キーを押します)。  
  
### <a name="to-sort-a-column"></a>列を並べ替えるには  
  
- 列見出しを選択します。  
  
### <a name="to-group-threads"></a>スレッドをグループ化するには  
  
- [並列ウォッチ] ウィンドウのショートカット メニューを開いて **[グループ化]** をクリックし、適切なサブメニュー項目を選択します。  
  
### <a name="to-freeze-or-thaw-threads"></a>スレッドを凍結/凍結解除するには  
  
- 行のショートカット メニューを開き、 **[凍結]** または **[凍結解除]** をクリックします。  
  
### <a name="to-export-the-data-in-the-parallel-watch-window"></a>[並列ウォッチ] ウィンドウ内のデータをエクスポートするには  
  
- **[Excel で開く]** ボタンを選択して、 **[Excel で開く]** または **[CSV にエクスポート]** を選択します。  
  
### <a name="to-filter-by-a-boolean-expression"></a>ブール式でフィルター処理するには  
  
- **[ブール式でフィルター]** ボックスにブール式を入力します。 デバッガーは、スレッド コンテキストの式を評価します。 値が `true` である行だけが表示されます。  
  
## <a name="see-also"></a>参照  
 [マルチスレッドアプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [方法: GPU スレッドウィンドウを使用する](../debugger/how-to-use-the-gpu-threads-window.md)   
 [チュートリアル: C++ AMP アプリケーションのデバッグ](https://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)
