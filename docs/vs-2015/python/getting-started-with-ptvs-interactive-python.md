---
title: 'PTVS の概要: 対話型の Python | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: fa594314-bdd0-4da5-874a-57b03414b675
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 4fba8bf658a50a7a7e28abace1eb622ab14f5f26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62550988"
---
# <a name="getting-started-with-ptvs-interactive-python"></a>PTVS の概要: 対話型の Python
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

対話型のプロンプトや read-eval-print ループ (REPL) は、生産性の高いプログラミング言語のための重要なツールです。  これにより、コードのスニペットを実行して API を発見および理解したり、API の使用を試したり、プロジェクトやプログラムなどの実動コードを対話形式で開発したりすることが可能になります。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=yc2CROtTsC0&index=5&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)で視聴できます。  
  
 [Python Environments] ウィンドウに、すべての Python 環境の一覧が表示されます。  そのいずれかを選択して、対話型ウィンドウまたは REPL を開くことができます。  コマンド プロンプトで Python.exe を実行したことがある場合は、以前に Python REPL を見ています。  REPL がプロンプトを出すので、ユーザーはコードを入力し、Enter キーを押して、コードの結果をすぐに確認できます。  これはライブ実行コンテキストであり、すべての実行、変数の割り当てなどのすべての状態が含まれます。 後で REPL プロンプトに送信する場合は、結果を保持する変数を参照できます。  複数行のコードを記述して、それらすべてを一度に実行できます (たとえば、メソッドの宣言や複数のステートメントなど)。  
  
 新しいライブラリの使用を開始するとき、そのライブラリを試用するために REPL はたいへん便利です。  ライブラリをインポートしたり、サブ パッケージ、クラス、および関数を調べたりすることができます。  Python は、その `help()` 関数によってこのすべての情報を通知します。  また、Python Tools for Visual Studio (PTVS) は、エディターで使用されるコードのモデル化に基づいて提案やドキュメントを提供します。その際、ライブラリを実行する必要はありません。  コードを実行するとき、PTVS は Python ランタイムからの情報を使用して PTVS の提案を改善します。  
  
 対話型ウィンドウは、開発しながらコードをテストするなど、反復的なまたは革新的なコードの開発にも役立ちます。  エディター ウィンドウで関数を選択して、右ポインター ボタンを押し、[Interactive に送信] を選択できます。  このコマンドは、次回の入力として選択内容を対話形式のウィンドウにコピーし、それを実行します。  その結果がすぐに表示されます。  以前の入力を変更する必要がある場合、上向き矢印キーを押してコードを再表示してから、それを変更して、Ctrl キーを押しながら Enter キーを押してコードを実行することができます。  入力の最後に Enter キーを押すと入力内容が実行されますが、入力の途中で Enter キーを押すと改行が挿入されます。  
  
 Python のインストール環境ごとに、必要な数の対話形式のウィンドウを開くことができます。  ウィンドウの上部には、表示のクリア、実行コンテキストのリセットなどのボタンがあります。 履歴はそのまま残ります。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=yc2CROtTsC0&index=5&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)で視聴できます。  
  
## <a name="see-also"></a>参照  
 [Wiki ドキュメント](https://github.com/Microsoft/PTVS/wiki/Interactive-REPL)   
 [PTVS の概要と詳細に関するビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
