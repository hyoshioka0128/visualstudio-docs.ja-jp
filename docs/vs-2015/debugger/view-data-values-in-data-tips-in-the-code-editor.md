---
title: コードエディターのデータヒントにデータ値を表示する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- debugging [Visual Studio], DataTips
- DataTips tool
ms.assetid: ffa7bd18-439b-4685-a9b3-c7884b5de41f
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fd2c7bf67b5c2e7f25b4193462883b53cda8db87
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700107"
---
# <a name="view-data-values-in-data-tips--in-the-code-editor"></a>コード エディターでのデータ ヒントのデータ値の表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DataTips は、デバッグ中にプログラムの変数に関する情報を確認するときに便利です。 データヒントは、中断モードのときにのみ機能します。また、実行の現在のスコープ内にある変数に対してだけ使用できます。  
  
 では [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 、datatip をソースファイル内の特定の場所に固定することも、すべてのウィンドウの上にフローティングすることもでき [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
### <a name="to-display-a-datatip-in-break-mode-only"></a>データヒントを表示するには (中断モードのみ)  
  
1. ソース ウィンドウで、現在のスコープにある任意の変数にマウス ポインターを移動します。  
  
    DataTip が表示されます。  
  
   > [!NOTE]
   > データヒントは、プログラムの実行が中断され、カーソルがホバーしていないコンテキストで常に評価されます。 現在のコンテキスト内の変数と同じ名前の別の関数内の変数にポインターを合わせると、その別の関数内の変数の値が、現在のコンテキストの変数の値として表示されます。  
  
2. マウス ポインターを離すとデータヒントが表示されなくなります。 開いたままになるようにヒントをピン留めするには、[ **ソースにピン留め** する] アイコンをクリックします。  
  
   - 変数を右クリックし、[ **ソースにピン留めする**] をクリックします。  
  
     固定したデータヒントは、デバッグ セッションを終了すると閉じます。  
  
### <a name="to-unpin-a-datatip-and-make-it-float"></a>データヒントの固定を解除してフローティングするには  
  
- ピン留めされた DataTip で、[ **ソースからのピン留めを外す** ] アイコンをクリックします。  
  
     ピン アイコンの表示が固定が解除された状態に変わり、 開いているすべてのウィンドウの上でデータヒントをフローティングできるようになります。 フローティング状態のデータヒントは、デバッグ セッションを終了すると閉じます。  
  
### <a name="to-repin-a-floating-datatip"></a>フローティング状態のデータヒントを再度固定するには  
  
- データヒントで、ピン アイコンをクリックします。  
  
     ピン アイコンの表示が固定された状態に変わります。 データヒントがソース ウィンドウ外にある場合は、ピン アイコンが無効になり、データヒントを固定することはできません。  
  
### <a name="to-close-a-datatip"></a>データヒントを閉じるには  
  
- DataTip にマウスポインターを置き、[ **閉じる** ] アイコンをクリックします。  
  
### <a name="to-close-all-datatips"></a>すべてのデータヒントを閉じるには  
  
- [ **デバッグ** ] メニューの [ **すべての DataTips をクリア**] をクリックします。  
  
### <a name="to-close-all-datatips-for-a-specific-file"></a>特定のファイルのすべてのデータヒントを閉じるには  
  
- [**デバッグ**] メニューの [*ファイル***にピン留めされたすべての DataTips をクリア**] をクリックします。  
  
## <a name="expanding-and-editing-information"></a>情報の展開と編集  
 データヒントを使用すると、配列、構造体、またはオブジェクトを展開して、メンバーを表示できます。 DataTip の変数値を編集することもできます。  
  
#### <a name="to-expand-a-variable-to-see-its-elements"></a>変数を展開して要素を表示するには  
  
- DataTip で、 **+** 変数名の前に来る記号の上にマウスポインターを置きます。  
  
     変数が展開され、ツリー形式で要素が表示されます。  
  
     変数を展開すると、キーボードの方向キーを使用して、上下に移動できます。 また、マウスも使用できます。  
  
#### <a name="to-edit-the-value-of-a-variable-using-a-datatip"></a>データヒントを使用して変数値を編集するには  
  
1. データヒントで、値をクリックします。 読み取り専用の値では無効です。  
  
2. 新しい値を入力し、Enter キーを押します。  
  
## <a name="making-a-datatip-transparent"></a>DataTip を透過的にする  
 データヒントの背後にあるコードを確認する場合は、一時的にデータヒントを透過的に設定できます。 固定されているか、またはフローティング状態になっているデータヒントには適用されません。  
  
#### <a name="to-make-a-datatip-transparent"></a>DataTip を透過的にするには  
  
- データヒントで、Ctrl キーを押します。  
  
     Ctrl キーを押している間、データヒントは透過的になります。  
  
## <a name="visualizing-complex-data-types"></a>複合データ型の表示  
 データヒントで変数名の横に虫眼鏡アイコンが表示される場合は、そのデータ型の変数に対して1つ以上の [カスタムビジュアライザーを作成](../debugger/create-custom-visualizers-of-data.md) できます。 ビジュアライザーを使用すると、よりわかりやすい形式 (通常はグラフィック形式) で情報が表示されます。  
  
#### <a name="to-view-the-contents-of-a-variable-using-a-visualizer"></a>ビジュアライザーを使用して変数の内容を表示するには  
  
- 虫眼鏡アイコンをクリックし、データ型の既定のビジュアライザーを選択します。  
  
     - または -  
  
     ビジュアライザーの横にあるポップアップ矢印をクリックし、データ型の適切なビジュアライザーを一覧から選択します。  
  
     ビジュアライザーに情報が表示されます。  
  
## <a name="adding-information-to-a-watch-window"></a>ウォッチ ウィンドウへの情報の追加  
 変数のウォッチを続行する場合は、[ **ウォッチ** ] ウィンドウに [DataTip] から変数を追加できます。  
  
#### <a name="to-add-a-variable-to-the-watch-window"></a>ウォッチ ウィンドウに変数を追加するには  
  
- [DataTip] を右クリックし、[ **ウォッチ式の追加**] をクリックします。  
  
     変数が [ **ウォッチ** ] ウィンドウに追加されます。 複数の [ **ウォッチ** ] ウィンドウをサポートするエディションを使用している場合は、ウォッチ1に変数が追加され **ます。**  
  
## <a name="importing-and-exporting-datatips"></a>データヒントのインポートとエクスポート  
 データヒントは XML ファイルにエクスポートして、他のユーザーと共有したり、テキスト エディターで編集したりすることができます。  
  
#### <a name="to-export-datatips"></a>データヒントをエクスポートするには  
  
1. [デバッグ] メニューの [ **DataTips ヒントのエクスポート**] をクリックします。  
  
     [ **Datatip のエクスポート** ] ダイアログボックスが表示されます。  
  
2. 標準のファイル技術を使用して、XML ファイルを保存する場所に移動し、[ **ファイル名** ] ボックスにファイルの名前を入力して、[ **OK**] をクリックします。  
  
#### <a name="to-import-datatips"></a>データヒントをインポートするには  
  
1. [デバッグ] メニューの [ **DataTips のインポート**] をクリックします。  
  
     [ **Datatip のインポート** ] ダイアログボックスが表示されます。  
  
2. ダイアログボックスを使用して、開く XML ファイルを検索し、[ **OK**] をクリックします。  
  
## <a name="see-also"></a>参照  
 [デバッガーでのデータの表示](../debugger/viewing-data-in-the-debugger.md)   
 [方法: [クイックウォッチ] ダイアログボックスを使用する](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)   
 [カスタムビジュアライザーの作成](../debugger/create-custom-visualizers-of-data.md)   
 [方法 : [デバッガー] ウィンドウの数値書式を変更する](https://msdn.microsoft.com/library/cd593847-a625-411d-a430-b798346ef18f)
