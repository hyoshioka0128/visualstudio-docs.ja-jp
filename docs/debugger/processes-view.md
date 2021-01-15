---
title: プロセス ビュー | Microsoft Docs
description: プロセス ビューには、ご利用のシステム上でアクティブになっているすべてのプロセスのツリーが表示されます。 その内容と使用について説明し、詳細情報へのリンクを参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.processesview
helpviewer_keywords:
- Processes view
ms.assetid: e144e70e-eef2-45a7-a562-a177f177d9a1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a52da28d01eac4f04081497888fbbfccaf4495e2
ms.sourcegitcommit: c67dece5ded82a5867148e1f94396954c1ec4398
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "97975135"
---
# <a name="processes-view"></a>プロセス ビュー
[プロセス] ビューには、お使いのシステム上でアクティブになっている全プロセスがツリー形式で表示されます。 プロセス ID とモジュール名が表示されます。 通常は実行中のプログラムに一致する特定のシステム プロセスを調べる場合、[プロセス] ビューを使用します。 プロセスはモジュール名で識別されます。あるいは、指名された "システム プロセス" となります。

 Microsoft Windows では、複数のプロセスがサポートされています。 各プロセスには、1 つまたは複数のスレッドが含まれることがあります。そして各スレッドには、上位ウィンドウが 1 つまたは複数関連付けられることがあります。 上位ウィンドウにはそれぞれ、一連のウィンドウが与えられることがあります。 \+ 記号は、1 つのレベルが折りたたまれていることを示します。 折りたたまれたビューは、プロセスあたり 1 行から構成されます。 \+ 記号をクリックすると、レベルが展開されます。

 通常は実行中のプログラムに一致する特定のシステム プロセスを調べる場合、[プロセス] ビューを使用します。 プロセスはモジュール名で識別されます。あるいは、指名された "システム プロセス" となります。 プロセスを見つけるには、ツリーを折りたたみ、リストを検索します。

## <a name="procedures"></a>プロシージャ

#### <a name="to-open-the-processes-view"></a>[プロセス] ビューを開くには

1. **[Spy]** メニューから **[プロセス]** を選択します。

   ![Spy&#43;&#43; プロセス ビュー](../debugger/media/spy--_processes.png "Spy++_Processes") Spy++ プロセス ビュー

   上の画像からは、プロセスとスレッド ノードが展開された [プロセス] ビューを確認できます。

### <a name="in-this-section"></a>このセクションの内容
 [プロセス ビューでのプロセスの検索](../debugger/how-to-search-for-a-process-in-processes-view.md) プロセス ビューで特定のプロセスを検索する方法について説明します。

 [プロセス プロパティの表示](../debugger/how-to-display-process-properties.md) メッセージに関する詳細を表示する方法について説明します。

### <a name="related-sections"></a>関連項目
 [Spy++ ビュー](../debugger/spy-increment-views.md) ウィンドウ、メッセージ、プロセス、およびスレッドの Spy++ ツリー ビューについて説明します。

 [Spy++ の使用](../debugger/using-spy-increment.md) Spy++ ツールを紹介し、その使用方法について説明します。

 [[プロセス検索] ダイアログ ボックス](../debugger/process-search-dialog-box.md) プロセス ビューで特定のプロセスのノードを検索するために使用されます。

 [[プロセス プロパティ] ダイアログ ボックス](../debugger/process-properties-dialog-box.md) プロセス ビューで選択したプロセスのプロパティを表示します。

 [Spy++ リファレンス](../debugger/spy-increment-reference.md) Spy++ の各メニューとダイアログ ボックスについて説明するセクションが含まれています。