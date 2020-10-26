---
title: 'PTVS の概要: コードの編集 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: b412c87c-2f09-4e25-9cc8-ab54f4c44412
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 2e883970b4b265b1864d53ef6e1f347160e5aeb9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62550913"
---
# <a name="getting-started-with-ptvs-editing-code"></a>PTVS の概要: コードの編集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

PTVS は、Python のために生産性の高い Visual Studio エディターのエクスペリエンスを提供します。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)で視聴できます。  
  
 空の基本的な Python アプリケーション プロジェクト テンプレートを使って開始します。  
  
 エディターで `from … import` 行の入力を開始します。  入力候補のポップアップ リストに、インポートに使用できるモジュールの完全な一覧が表示されます。  この一覧は、Python のバージョンとインストールしたライブラリに応じて異なります。  例として、数値演算ライブラリを使用します。  入力するごとに、入力候補の一覧がフィルターに掛けられて、入力された文字を含むアイテムだけが表示されるようになることが分かります。  `sin` 識別子をインポートして、ステートメントを完了します。  
  
```python  
from math import sin  
  
```  
  
 コーディングの際に、バインドされていない、しかしライブラリには存在する識別子を使用する場合、PTVS は、必要となる適切なインポート ステートメントを追加するためのポップアップ クイック フィックスを提供します。  たとえば、「`cos`」と入力した場合、**import from math** が提供されるのがわかります。  
  
 スニペットを使用してコードを生成することができます。  [編集] メニューで、[IntelliSense]、[スニペットの挿入] の順に選択します。  ここで、[Python]、[def] の順に選択します。 関数を呼び出し、 `make_dot_string` パラメーターを1つ追加し `x` ます。  ここで、テスト駆動開発のためにアサーションをファイルに追加できます。PTVS が入力候補一覧に新しい関数を既に提供できるようになっていることが分かります。  
  
```python  
assert make_dot_string(90) == '          o'  
assert make_dot_string(180) == 'o'  
  
```  
  
 ここで、新しい関数に戻り、次の本文の書き込みを開始します。  
  
```python  
return " " * int(10 * cos(radians(x)) + 10) + "o"  
  
```  
  
 PTVS がこの関数への呼び出しサイトを分析しているので、PTVS はパラメーターが整数であると想定していることが分かります。   また、`radians` をインポートするために、クイック フィックスを使用することも必要です。  
  
 最上位レベルで `main` と入力することにより、スマート タグ UI を呼び出し、タブを使用して「def main...」を選択して、別のスニペットを使用してメインのブロックを作成します。  `make_dot_string` を呼び出すための基本ループを記述します。  ピリオドを入力して示される入力候補を確認することにより、関数が文字列を返すことを PTVS が知っていることが分かります。  この型情報は、プログラム全体をフローするので、値がどこで終了しても、コードの理解と記述に役立つツールヒントと入力候補を提供できます。  
  
 print への呼び出しを追加すると、以下のような main ができあがります。  
  
```python  
def main ():  
    for i in range(10000000):  
        s = make_dot_string(i)  
        print(s)  
```  
  
 F5 キーを押すと、cmd.exe ウィンドウでコードが実行されて、前後に動くドットが表示されます。  
  
 これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=uZGZNEyyeKs&index=3&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)で視聴できます。  
  
## <a name="see-also"></a>参照  
 [Wiki ドキュメント](https://github.com/Microsoft/PTVS/wiki/Editor-Features)   
 [PTVS の概要と詳細に関するビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
