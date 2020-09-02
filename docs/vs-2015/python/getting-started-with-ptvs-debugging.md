---
title: 'PTVS の概要: デバッグ | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 82803559-1d60-4c57-98fb-2dc1e0182b42
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: b636dd4f3a5c5265231898573bfdf52de2dff84e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197711"
---
# <a name="getting-started-with-ptvs-debugging"></a>PTVS の概要: デバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の対話型デバッガーを使用すると、Python コード内の問題を簡単に診断して解決できます。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4)で視聴できます。  
  
 直前の概要のトピックでは、空の Python アプリケーション プロジェクトを作成して、PythonApplication1.py に次のコードを入力しました。  
  
```python  
from math import sin, cos, radians  
import sys  
  
def make_dot_string(x):  
    return ' ' * int(10 * cos(radians(x)) + 10) + 'o'  
  
assert make_dot_string(90) == "          o"  
assert make_dot_string(180) == "o"  
  
def main():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
  
if __name__ == "__main__":  
    sys.exit(int(main() or 0))  
```  
  
 通常、Visual Studio でコードの作業をするときは、F5 キーを押してコードの実行を開始します。  このコマンドは、構築する必要があるプロジェクト内の任意の箇所を構築し、デバッガーの下でコードの実行を開始します。  Ctrl キーを押しながら F5 キーを押すことにより、デバッガーなしでコードを構築して起動できます。  デバッガーを使用すると、コードの実行は少し遅くなりますが、それと引き換えに強力なデバッグ機能を利用できます。  
  
 コードを起動する別の方法は、(通常は F11 キーにバインドされた) ステップ イン コマンドを使用することです。  これは F5 キーに似ていますが、各ステートメントで実行を一時停止します。  特定の位置でプログラムをブレークする場合は、コード エディターの左余白で左ポインター ボタンを押して、ブレークポイントを設定できます。  F5 キーを押すと、プログラムの実行はブレークポイントのある行でがブレークつまり停止します。  [デバッグ] メニューには、ステップごとの実行のためのオプションがさらにあります。たとえば、ステップ オーバー関数の呼び出し (F10)、ステップ イン関数の呼び出し (F11)、関数の末尾でのスキップ (Shift キーを押しながら F11) などです。  
  
 ブレークがあると、デバッガーでより多くの機能を実行できます。  [ローカル] ウィンドウには、ローカル変数の現在値が表示されます。  コードのステップを実行すると、ローカルの表示が自動的に更新します。  [自動変数] ウィンドウには、実行が停止した現在行の近くの変数が表示されます。  [ウォッチ] ウィンドウには、任意の Python の式を入力できます。これは、実行が停止するたびにデバッガーが自動的に更新しまのす。  また、エディター ウィンドウ内の変数をポインターでホバーして、変数の値のポップアップを表示することができます。このデータ ヒントの表示によって、オブジェクト内を検査できます。  一部のデータ型には、データのヒントの表示からアクセスできる特殊なビジュアライザーがあります (たとえば、HTML、XML、JSON などの特殊な書式設定を含む文字列など)。  
  
 [呼び出し履歴] ウィンドウには、デバッガーが停止している現在のステートメントの原因となった、保留中の関数呼び出しが表示されます。  さまざまなスタック フレーム (呼び出しスタック内の行) を選択して、コードが各関数での実行続行、変数の値の検索などを実行する場所にジャンプできます。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=bO7wpzgy74A&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=4)で視聴できます。  
  
## <a name="see-also"></a>参照  
 [Wiki ドキュメント](https://github.com/Microsoft/PTVS/wiki/Debugging)   
 [PTVS の概要と詳細に関するビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
