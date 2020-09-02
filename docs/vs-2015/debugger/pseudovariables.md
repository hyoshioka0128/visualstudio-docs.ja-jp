---
title: 擬似変数 | Microsoft Docs
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
- Watch window, pseudovariables
- debugging [Visual Studio], pseudovariables
- pseudovariables
ms.assetid: fae84f68-2138-4144-9bd4-c9e271b6182a
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e9ce72d69cb64b0421771324803a785546fa884f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65693765"
---
# <a name="pseudovariables"></a>擬似変数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

擬似変数は、変数ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスに特定の情報を表示するときに使用される用語です。 通常の変数を入力するときと同様に、擬似変数を入力できます。 ただし、擬似変数は変数ではなく、プログラム内の変数名に対応しません。  
  
## <a name="example"></a>例  
 たとえば、ネイティブ コード アプリケーションを記述していて、アプリケーションに割り当てられたハンドル数を確認する場合を考えてみます。 **[ウォッチ]** ウィンドウで、 **[名前]** 列に次の擬似変数を入力し、Enter キーを押すと、擬似変数が評価されます。  
  
```  
$handles  
```  
  
 ネイティブ コードの場合、次の表に示す擬似変数を使用できます。  
  
|擬似変数|関数|  
|--------------------|--------------|  
|`$err`|SetLastError 関数で設定された最後のエラー値を表示します。 表示される値は、本来 GetLastError が返す値を示します。<br /><br /> `$err,hr` を使用すると、この値のデコードされた形式が表示されます。 たとえば、最後のエラーが 3 の場合、`$err,hr` によって `ERROR_PATH_NOT_FOUND : The system cannot find the path specified.` と表示されます。|  
|`$handles`|アプリケーションに割り当てられているハンドル数を表示します。|  
|`$vframe`|現在のスタック フレームのアドレスを表示します。|  
|`$tid`|現在のスレッドのスレッド ID を表示します。|  
|`$env`|文字列ビューアーの環境ブロックを表示します。|  
|`$cmdline`|プログラムを実行したコマンド ライン文字列を表示します。|  
|`$pid`|プロセス ID を表示します。|  
|`$` *registername*<br /><br /> or<br /><br /> `@` *registername*|*registername* レジスタの内容を表示します。<br /><br /> 通常は、レジスタ名を入力するだけでレジスタの内容を表示できます。 この構文を使用する必要があるのは、レジスタ名で変数名をオーバーロードしている場合だけです。 レジスタ名が現在のスコープ内での変数名と同じであると、デバッガーは、その名前を変数名と解釈します。 このようなときには、`$`*registername* や `@`*registername* が便利です。|  
|`$clk`|クロック周期の時間を表示します。|  
|`$user`|アプリケーションを実行しているアカウントのアカウント情報と共に、構造体を表示します。 セキュリティ上の理由から、パスワード情報は表示されません。|  
|`$exceptionstack`|現在の Windows ランタイムの例外のスタック トレースを表示します。 `$ exceptionstack` Windows 8.1 以降で実行されているストアアプリでのみ機能します。 `$ exceptionstack` は、C++ および SHE の例外ではサポートされません。|  
|`$ReturnValue`|.NET Framework メソッドの戻り値を表示します。 「[メソッド呼び出しの戻り値を確認](https://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f)する」を参照してください。|  
  
 C# と Visual Basic では、次の表に示す擬似変数を使用できます。  
  
|擬似変数|関数|  
|--------------------|--------------|  
|`$exception`|最後の例外に関する情報が表示されます。 例外が発生しなかった場合、`$exception` を評価してエラー メッセージが表示されます。<br /><br /> Visual C# のみに、Exception Assistant が無効なときに例外が発生すると、`$exception` が自動的に **[ローカル]** ウィンドウに追加されます。|  
|`$user`|アプリケーションを実行しているアカウントのアカウント情報と共に、構造体を表示します。 セキュリティ上の理由から、パスワード情報は表示されません。|  
  
 Visual Basic では、次の表に示す擬似変数を使用できます。  
  
|擬似変数|関数|  
|--------------------|--------------|  
|`$delete` または `$$delete`|**[イミディエイト]** ウィンドウで作成された暗黙的な変数を削除します。 構文は、`$delete,` *variable* または `$delete,` *variable* です`.`|  
|`$objectids` または `$listobjectids`|すべてのアクティブ オブジェクト ID を、指定された式の子として表示します。 構文は、`$objectid,` *expression* または `$listobjectids,` *expression* です`.`|  
|`$` *N* `#`|*N* と等しいオブジェクト ID を持つオブジェクトを表示します。|  
|`$dynamic`|`IDynamicMetaObjectProvider` を実装するオブジェクト用の特別な **[動的ビュー]** ノードを表示します。 インターフェイス。 構文は `$dynamic,` *object* です。 この機能は、.NET Framework Version 4 を使用するコードにのみ適用されます。 [動的ビュー](https://msdn.microsoft.com/library/4c851b17-2c12-46a0-9828-eb6ea6f5c563)を参照してください。|  
  
## <a name="see-also"></a>参照  
 [ウォッチウィンドウとクイックウォッチウィンドウ](../debugger/watch-and-quickwatch-windows.md)   
 [[変数] ウィンドウ](https://msdn.microsoft.com/library/ce0a67f6-2502-4b7a-ba45-cc32f8aeba3e)
