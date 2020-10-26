---
title: LINQ のデバッグ | Microsoft Docs
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
- debugging, LINQ
- LINQ, viewing results in debugger
- LINQ, debugging
- LINQ, stepping
- LINQ, edit and continue
ms.assetid: dbae26cb-ac5f-4312-b474-b9f29714f4c6
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0292bf5b62bf150a598b4c750929ba6928216a50
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691269"
---
# <a name="debugging-linq"></a>LINQ のデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、統合言語クエリ (LINQ) コードのデバッグがサポートされていますが、いくつかの制約事項があります。 ステップ実行、ブレークポイントの設定、デバッガー ウィンドウでの結果の表示など、ほとんどのデバッグ機能を、LINQ ステートメントと組み合わせて使用することができます。 このトピックでは、LINQ のデバッグに伴う主要な制限事項について説明します。  
  
## <a name="viewing-linq-results"></a><a name="BKMK_ViewingLINQResults"></a> LINQ の結果の表示  
 LINQ ステートメントの結果を表示するには、DataTip、[ウォッチ] ウィンドウ、および [クイック ウォッチ] ダイアログ ボックスを使用します。 ソース ウィンドウを使用すると、ソース ウィンドウ内のクエリ上でポインターを停止し、DataTip を表示することができます。 LINQ 変数をコピーし、[ウォッチ] ウィンドウや [クイック ウォッチ] ダイアログ ボックスに貼り付けることができます。  
  
 LINQ では、クエリは作成または宣言の時点では評価されず、実行時にのみ評価されます。 したがって、評価の時点までクエリには値がありません。 クエリの作成と評価の詳細については、「[LINQ クエリの概要 (C#)](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)」または「[初めての LINQ クエリの作成](https://msdn.microsoft.com/library/4affb732-3e9b-4479-aa31-1f9bd8183cbe)」を参照してください。  
  
 クエリの結果を表示するためには、デバッガーがクエリを評価する必要があります。 そのため、LINQ クエリの結果をデバッガーで表示するときには、クエリが評価されることにより、次のような影響が生じます。  
  
- クエリの評価には時間がかかります。 結果ノードを展開するときにも時間を要します。 クエリによっては、評価の反復によってパフォーマンスが大幅に低下することがあります。  
  
- クエリの評価は、データの値やプログラムの状態が変化するという副作用をもたらすことがあります。 すべてのクエリに副作用があるわけではありません。 クエリの評価に副作用があるかどうかを確認するためには、クエリを実装するコードの内容を把握する必要があります。  
  
## <a name="stepping-and-linq"></a><a name="BKMK_SteppingAndLinq"></a>ステップ実行と LINQ  
 LINQ コードをデバッグする場合は、ステップ実行に動作上の違いがいくつかあるため、理解しておく必要があります。  
  
### <a name="linq-to-sql"></a>LINQ to SQL  
 LINQ to SQL クエリでは、述語コードがデバッガーによる処理の対象外となります。 そのため、述語コードにステップ インすることはできません。 式ツリーにコンパイルされるクエリは、デバッガーによる処理の対象とならないコードを生成します。  
  
### <a name="stepping-in-visual-basic"></a>Visual Basic でのステップ実行  
 Visual Basic プログラムをステップ実行し、デバッガーがクエリ宣言を検出すると、デバッガーはその宣言にはステップ インせず、宣言全体を 1 つのステートメントとして強調表示します。 この動作が発生するのは、クエリが呼び出されるまで評価されないためです。 詳細については、「[Visual Basic における LINQ の概要](https://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984)」を参照してください。  
  
 次のようなコードをステップ実行すると、クエリを作成するクエリ宣言が 1 つのステートメントとして強調表示されます。  
  
```  
Function MyFunction(ByVal x As Char)  
    Return True  
End Function  
  
Sub Main()  
    'Query creation  
    Dim x = From it In "faoaoeua" _  
            Where MyFunction(it) _  
            Select New With {.a = it}  
  
    ' Query execution  
    For Each cur In x  
        Console.WriteLine(cur.ToString())  
    Next  
End Sub  
```  
  
 さらにステップ実行すると、`For Each cur In x` が強調表示されます。 次の手順では、デバッガーが関数 `MyFunction` にステップ インします。 `MyFunction` のステップ実行の後、デバッガーは `Console.WriteLine(cur.ToSting())` に戻ります。 どの段階でも、デバッガーはクエリ宣言内の述語コードにはステップ インしません。ただし、述語コードの評価は行います。  
  
### <a name="replacing-a-predicate-with-a-function-to-enable-stepping-visual-basic"></a>述語コードを関数に置き換えてステップ実行を可能にする (Visual Basic)  
 デバッグのために述語コードをステップ実行する必要がある場合は、述語コードを同じコードが含まれる関数の呼び出しに置き換えることができます。 たとえば、次のようなコードがあるとします。  
  
```  
Dim items() as integer ={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}  
  
' Get the even numbers  
Dim query = From nextInt in items Where nextInt Mod 2 = 0 Select nextInt  
  
For each item in query  
      Console.WriteLine(item)  
Next  
```  
  
 述語コードを次のように `IsEven` という新しい関数に移動できます。  
  
```  
Dim items () as integer ={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}  
  
' Get the even numbers  
Dim query = From nextInt in items Where IsEven(nextInt) Select nextInt  
  
For each item in query  
      Console.WriteLine(item)  
Next  
...   
Function IsEven(item As =Integer) as Boolean  
      Return item Mod 2 = 0  
End Function  
```  
  
 修正したクエリは、`IsEven` のパスごとに関数 `items` を呼び出します。 デバッガー ウィンドウで各項目が指定された条件を満たすかどうかを確認し、`IsEven` 内のコードをステップ実行できます。 この例の述語コードはきわめて単純です。 もっと複雑な述語コードをデバッグする場合にも、この方法が十分役に立つことがあります。  
  
## <a name="edit-and-continue-not-supported-for-linq"></a><a name="BKMK_EditandContinueNotSupportedforLINQ"></a>LINQ でサポートされないエディット コンティニュ  
 エディット コンティニュは、LINQ クエリの変更をサポートしていません。 デバッグ セッション中に LINQ ステートメントを追加、削除、または変更すると、そのような変更がエディット コンティニュでサポートされていないことを示すダイアログ ボックスが表示されます。 このとき、変更を元に戻すか、デバッグ セッションを中止して編集済みのコードで新たなセッションを開始するかを選択できます。  
  
 また、エディット コンティニュでは、LINQ ステートメントで使用されている変数の型や値の変更もサポートされていません。 この場合も、変更を元に戻すか、デバッグ セッションを中止して新たなセッションを開始するかを選択できます。  
  
 C# では、LINQ クエリを含むメソッドのコードに対してエディット コンティニュを使用することはできません。  
  
 Visual Basic では、LINQ クエリを含むメソッドであっても、LINQ 以外のコードであればエディット コンティニュを使用できます。 LINQ ステートメントの前であれば、LINQ クエリの行番号が変わる場合でも、コードの追加や削除を行うことができます。 LINQ 以外のコードの Visual Basic デバッグは、LINQ が導入される前と同じように動作します。 ただし、デバッグを中止して変更を適用しない限り、LINQ クエリを変更、追加、または削除することはできません。  
  
## <a name="see-also"></a>参照  
 [SQL のデバッグ](https://msdn.microsoft.com/f27c17e6-1d90-49f2-9fc0-d02e6a27f109)   
 [副作用と式](https://msdn.microsoft.com/library/e1f8a6ea-9e19-481d-b6bd-df120ad3bf4e)   
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)   
 [LINQ クエリの概要 (C#)](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)   
 [Visual Basic における LINQ の概要](https://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984)
