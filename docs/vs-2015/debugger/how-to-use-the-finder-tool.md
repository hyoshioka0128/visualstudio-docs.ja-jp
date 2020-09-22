---
title: '方法: ファインダー ツールを使用する |　Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Window Finder Tool
ms.assetid: 5841926b-08c3-4e43-88bd-4223d04f9aef
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 00535fd336f504afcebdd24a4d009a10f7f6ff33
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841924"
---
# <a name="how-to-use-the-finder-tool"></a>方法: ファインダー ツールを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[ウィンドウ検索]** ダイアログ ボックスで [ファインダー] ツールを使用して、ウィンドウのプロパティまたはメッセージを表示できます。 ファインダー ツールでは、無効になっている子ウィンドウを検索し、無効になっている子ウィンドウが重なっている場合にどのウィンドウを強調表示するかを識別することもできます。  
  
 ![Spy&#43;&#43; [ウィンドウ検索] ダイアログボックス](../debugger/media/icon-spy-find.png "Icon_Spy++_Find")  
[ウィンドウの検索] ダイアログボックスのファインダーツール  
  
 上の図は、次の手順 3 の後の [ウィンドウ検索] ダイアログ ボックスを示しています。  
  
### <a name="to-display-window-properties-or-messages"></a>ウィンドウのプロパティまたはメッセージを表示するには  
  
1. Spy++ とターゲット ウィンドウが表示されるように、ご利用のウィンドウを配置します。  
  
2. **[Spy]** メニューから **[ウィンドウ検索]** を選択します。  
  
     [[ウィンドウ検索] ダイアログ ボックス](../debugger/find-window-dialog-box.md)が開きます。  
  
3. **[ファインダー ツール]** をターゲット ウィンドウにドラッグします。  
  
     そのツールをドラッグすると、 **[ウィンドウ検索]** ダイアログ ボックスに選択したウィンドウの詳細が表示されます。  
  
     または  
  
     確認するウィンドウのハンドル (たとえば、デバッガーからコピーしたもの) がある場合は、それを **[ハンドル]** テキスト ボックスに入力します。  
  
    > [!TIP]
    > 画面が乱雑にならないようにするには、 **[Spy を非表示]** オプションを選択します。 このオプションを選択すると、Spy++ のメイン ウィンドウが非表示になり、 **[ウィンドウ検索]** ダイアログ ボックスだけが他のアプリケーションの上に表示されます。 **[OK]** または **[キャンセル]** をクリックした場合、または **[Spy++ を非表示]** オプションをオフにした場合は、Spy++ のメイン ウィンドウが復元されます。  
  
4. **[表示]** で、 **[プロパティ]** または **[メッセージ]** を選択します。  
  
5. **[OK]** を押します。  
  
     **[プロパティ]** を選択した場合は、[[ウィンドウのプロパティ] ダイアログ ボックス](../debugger/window-properties-dialog-box.md)が開きます。 **[メッセージ]** を選択した場合は、[[メッセージ ビュー]](../debugger/messages-view.md) ウィンドウが開きます。  
  
## <a name="see-also"></a>参照  
 [Spy + + ビュー](../debugger/spy-increment-views.md)   
 [Spy + + の使用](../debugger/using-spy-increment.md)   
 [Spy++ リファレンス](../debugger/spy-increment-reference.md)
