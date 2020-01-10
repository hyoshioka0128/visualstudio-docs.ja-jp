---
title: 擬似変数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Watch window, pseudovariables
- debugging [Visual Studio], pseudovariables
- pseudovariables
ms.assetid: fae84f68-2138-4144-9bd4-c9e271b6182a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5b0369a30e69fc69782bbc4a0f5b0c4518cac07
ms.sourcegitcommit: 10d16e18c5f5e482c4c2856e6cacaad283463b65
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776085"
---
# <a name="pseudovariables-in-the-visual-studio-debugger"></a>Visual Studio デバッガーの擬似変数
擬似変数は、変数ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスに特定の情報を表示するときに使用される用語です。 通常の変数を入力するときと同様に、擬似変数を入力できます。 ただし、擬似変数は変数ではなく、プログラム内の変数名に対応しません。

## <a name="example"></a>使用例
 たとえば、ネイティブ コード アプリケーションを記述していて、アプリケーションに割り当てられたハンドル数を確認する場合を考えてみます。 **[ウォッチ]** ウィンドウで、 **[名前]** 列に次の擬似変数を入力し、Enter キーを押すと、擬似変数が評価されます。

`$handles`

 ネイティブコードでは、次の表に示す擬似変数を使用できます。

|擬似変数|関数|
|--------------------|--------------|
|`$err`|SetLastError 関数で設定された最後のエラー値を表示します。 表示される値は、本来 GetLastError が返す値を示します。<br /><br /> `$err,hr` を使用すると、この値のデコードされた形式が表示されます。 たとえば、最後のエラーが 3 の場合、`$err,hr` によって `ERROR_PATH_NOT_FOUND : The system cannot find the path specified.` と表示されます。|
|`$handles`|アプリケーションに割り当てられているハンドル数を表示します。|
|`$vframe`|現在のスタック フレームのアドレスを表示します。|
|`$tid`|現在のスレッドのスレッド ID を表示します。|
|`$env`|文字列ビューアーの環境ブロックを表示します。|
|`$cmdline`|プログラムを実行したコマンド ライン文字列を表示します。|
|`$pid`|プロセス ID を表示します。|
|`$` *registername*<br /><br /> または<br /><br /> `@` *registername*|*registername* レジスタの内容を表示します。<br /><br /> 通常は、レジスタ名を入力するだけでレジスタの内容を表示できます。 この構文を使用する必要があるのは、レジスタ名で変数名をオーバーロードしている場合だけです。 レジスタ名が現在のスコープ内での変数名と同じであると、デバッガーは、その名前を変数名と解釈します。 このようなときには、`$`*registername* や `@`*registername* が便利です。|
|`$clk`|クロック周期の時間を表示します。|
|`$user`|アプリケーションを実行しているアカウントのアカウント情報と共に、構造体を表示します。 セキュリティ上の理由から、パスワード情報は表示されません。|
|`$exceptionstack`|現在の Windows ランタイムの例外のスタック トレースを表示します。 `$ exceptionstack` は、UWP アプリでのみ機能します。 `$ exceptionstack` は、および SEH C++例外ではサポートされていません|
|`$returnvalue`|メソッドの戻り値を表示します。|

 でC#は、次の表に示す擬似変数を使用できます。

|擬似変数|関数|
|--------------------|--------------|
|`$exception`|最後の例外に関する情報が表示されます。 例外が発生しなかった場合、`$exception` を評価してエラー メッセージが表示されます。<br /><br /> 例外処理アシスタントが無効になっていると、例外が発生したときに、`$exception` が自動的に **[ローカル]** ウィンドウに追加されます。|
|`$user`|アプリケーションを実行しているアカウントのアカウント情報と共に、構造体を表示します。 セキュリティ上の理由から、パスワード情報は表示されません。|
|`$returnvalue`|.NET メソッドの戻り値を表示します。|

 Visual Basic では、次の表に示す擬似変数を使用できます。

|擬似変数|関数|
|--------------------|--------------|
|`$exception`|最後の例外に関する情報が表示されます。 例外が発生しなかった場合、`$exception` を評価してエラー メッセージが表示されます。|
|`$delete` または `$$delete`|**[イミディエイト]** ウィンドウで作成された暗黙的な変数を削除します。 構文は、*変数*または`$delete,`*変数*`$delete,``.`|
|`$objectids` または `$listobjectids`|すべてのアクティブ オブジェクト ID を、指定された式の子として表示します。 構文*は、式または*`$listobjectids,`*式*`$objectid,``.`|
|`$` *N* `#`|*N* と等しいオブジェクト ID を持つオブジェクトを表示します。|
|`$dynamic`|`IDynamicMetaObjectProvider` を実装するオブジェクト用の特別な **[動的ビュー]** ノードを表示します。 インターフェイス。 構文は `$dynamic,`*オブジェクト*です。 この機能は .NET Framework バージョン4以降を使用するコードにのみ適用されます。|

## <a name="see-also"></a>関連項目
- [ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)
- [[変数] ウィンドウ](../debugger/debugger-windows.md)
