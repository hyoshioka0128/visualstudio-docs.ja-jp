---
title: プロセス ビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.processesview
helpviewer_keywords:
- Processes view
ms.assetid: e144e70e-eef2-45a7-a562-a177f177d9a1
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d8b9c04d1cabd44418c70725ef331c9c4b5ec67e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580506"
---
# <a name="processes-view"></a>プロセス ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[プロセス] ビューには、お使いのシステム上でアクティブになっている全プロセスがツリー形式で表示されます。 プロセス ID とモジュール名が表示されます。 通常は実行中のプログラムに一致する特定のシステム プロセスを調べる場合、[プロセス] ビューを使用します。 プロセスはモジュール名で識別されます。あるいは、指名された "システム プロセス" となります。  
  
 Microsoft Windows では、複数のプロセスがサポートされています。 各プロセスには、1 つまたは複数のスレッドが含まれることがあります。そして各スレッドには、上位ウィンドウが 1 つまたは複数関連付けられることがあります。 上位ウィンドウにはそれぞれ、一連のウィンドウが与えられることがあります。 \+ 記号は、1 つのレベルが折りたたまれていることを示します。 折りたたまれたビューは、プロセスあたり 1 行から構成されます。 \+ 記号をクリックすると、レベルが展開されます。  
  
 通常は実行中のプログラムに一致する特定のシステム プロセスを調べる場合、[プロセス] ビューを使用します。 プロセスはモジュール名で識別されます。あるいは、指名された "システム プロセス" となります。 プロセスを見つけるには、ツリーを折りたたみ、リストを検索します。  
  
## <a name="procedures"></a>プロシージャ  
  
#### <a name="to-open-the-processes-view"></a>[プロセス] ビューを開くには  
  
1. **[Spy]** メニューから **[プロセス]** を選択します。  
  
   ![Spy&#43;&#43; プロセスビュー](../debugger/media/spy-processes.png "Spy + + _Processes")  
   Spy++ プロセス ビュー  
  
   上の画像からは、プロセスとスレッド ノードが展開された [プロセス] ビューを確認できます。  
  
### <a name="in-this-section"></a>このセクションの内容  
 [プロセスビューでのプロセスの検索](../debugger/how-to-search-for-a-process-in-processes-view.md)  
 [プロセス] ビューで特定のプロセスを検索する方法について説明します。  
  
 [表示 (プロセスのプロパティを)](../debugger/how-to-display-process-properties.md)  
 メッセージに関する詳細情報を表示する方法について説明します。  
  
### <a name="related-sections"></a>関連項目  
 [Spy++ ビュー](../debugger/spy-increment-views.md)  
 Windows、メッセージ、プロセス、およびスレッドの Spy + + ツリービューについて説明します。  
  
 [Spy++ の使用](../debugger/using-spy-increment.md)  
 Spy + + ツールの概要と、その使用方法について説明します。  
  
 [[プロセス検索] ダイアログ ボックス](../debugger/process-search-dialog-box.md)  
 [プロセス] ビューで特定のプロセスのノードを検索するために使用します。  
  
 [[プロセス プロパティ] ダイアログ ボックス](../debugger/process-properties-dialog-box.md)  
 [プロセス] ビューで選択したプロセスのプロパティを表示します。  
  
 [Spy++ リファレンス](../debugger/spy-increment-reference.md)  
 各 Spy + + メニューおよびダイアログボックスについて説明するセクションが含まれています。
