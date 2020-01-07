---
title: Visual Basic での警告の構成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Basic], warnings
- run-time errors, warnings
- warnings, configuring
ms.assetid: 99cf4781-bd4d-47b4-91b9-217933509f82
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d09a251dc5f98080b317e1560423dcb7c8bf0805
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619313"
---
# <a name="configuring-warnings-in-visual-basic"></a>Visual Basic での警告の構成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] のコンパイラには、実行時エラーの原因になる可能性があるコードに関する警告のセットが用意されています。 その情報を使うと、よりきれいで、速く、優れたコードを、バグをほとんど含まずに記述することができます。 たとえば、代入されていないオブジェクト変数のメンバーを呼び出そうとしたり、戻り値を設定しないで関数から戻ろうとしたり、例外をキャッチするロジックでエラーのある `Try` ブロックを実行しようとしたりすると、コンパイラはエラーを生成します。

 場合によって、コンパイラはユーザーの代わりに追加ロジックを提供し、ユーザーがエラーの可能性を考えることなく現在の作業に集中できるようにします。 以前のバージョンの [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] では、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コンパイラが提供する追加ロジックを制限するために `Option Strict` が使われていました。 警告を構成すると、個々の警告のレベルでさらに詳細にこのロジックを制限することができます。

 プロジェクトをカスタマイズして、アプリケーションに関係のない警告はオフにし、他の警告はエラーにすることができます。 このページでは、個々の警告を有効または無効にする方法について説明します。

## <a name="turning-warnings-off-and-on"></a>警告のオフとオンの切り替え
 警告を構成するには 2 つの異なる方法があります。**プロジェクト デザイナー**を使う方法と、 **/warnaserror** および **/nowarn** コンパイラ オプションを使う方法です。

 **[プロジェクト デザイナー]** ページの **[コンパイル]** タブで、警告を有効または無効にできます。 **[すべての警告を表示しない]** チェック ボックスをオンにすると、すべての警告が無効になります。 **[すべての警告をエラーとして扱う]** をオンにすると、すべての警告がエラーとして処理されます。 一部の個別警告は、表示されるテーブルで必要に応じてエラーまたは警告として切り替えることができます。

 **Option Strict** が**オフ**に設定されていると、**Option Strict** 関連の警告を個別に扱うことはできません。 **Option Strict** が**オン**に設定されていると、関連する警告は状態に関係なくエラーとして扱われます。 コマンド ライン コンパイラで `/optionstrict:custom` を指定することによって **Option Strict** が**カスタム**に設定されていると、**Option Strict** の警告のオン/オフを独立して切り替えることができます。

 コンパイラの **/warnaserror** コマンド ライン オプションを使って、警告をエラーとして扱うかどうかを指定することもできます。 コンマ区切りリストをこのオプションに追加し、+ または - を使ってエラーまたは警告として扱う必要がある警告を指定できます。 次の表では、使用できるオプションを詳しく説明します。

|コマンド ライン オプション|指定内容|
|--------------------------|---------------|
|`/warnaserror+`|すべての警告をエラーとして扱います。|
|`/warnsaserror`-|警告をエラーとして扱いません。 既定値です。|
|`/warnaserror+:<warning list` `>`|コンマ区切りリストでエラー ID 番号を指定した特定の警告をエラーとして扱います。|
|`/warnaserror-:<warning list>`|コンマ区切りリストでエラー ID 番号を指定した特定の警告をエラーとして扱いません。|
|`/nowarn`|警告を報告しません。|
|`/nowarn:<warning list>`|コンマ区切りリストでエラー ID 番号を指定した警告を報告しません。|

 警告の一覧にはエラーとして扱う必要のある警告のエラー ID 番号が含まれ、それをコマンド ライン オプションで使って特定の警告のオン/オフを指定できます。 警告の一覧に無効な値が含まれる場合は、エラーが報告されます。

## <a name="examples"></a>使用例
 次の表では、コマンド ライン引数の動作の例を示します。

|引数|説明|
|--------------|-----------------|
|`vbc /warnaserror`|すべての警告をエラーとして扱うよう指定しています。|
|`vbc /warnaserror:42024`|警告 42024 をエラーとして扱うよう指定します。|
|`vbc /warnaserror:42024,42025`|警告 42024 と 42025 をエラーとして扱うよう指定します。|
|`vbc /nowarn`|すべての警告を報告しないよう指定します。|
|`vbc /nowarn:42024`|警告 42024 を報告しないよう指定します。|
|`vbc /nowarn:42024,42025`|警告 42024 と 42025 を報告しないよう指定します。|

## <a name="types-of-warnings"></a>警告の種類
 エラーとして処理できる警告の一覧を次に示します。

### <a name="implicit-conversion-warning"></a>暗黙的な変換の警告
 暗黙的な変換のインスタンスに対して生成されます。 `&` 演算子を使ったときの組み込み数値型から文字列への暗黙的な変換は含まれません。 新しいプロジェクトでの既定値はオフです。

 ID: 42016

### <a name="late-bound-method-invocation-and-overload-resolution-warning"></a>遅延バインド メソッドの呼び出しおよびオーバーロードの解決の警告
 遅延バインドのインスタンスに対して生成されます。 新しいプロジェクトでの既定値はオフです。

 ID: 42017

### <a name="operands-of-type-object-warnings"></a>Object 型のオペランドの警告
 `Option Strict On` でエラーを作成する `Object` 型のオペランドが発生したときに生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42018、42019

### <a name="declarations-require-as-clause-warnings"></a>"As" 句が必要な宣言の警告
 変数、関数、またはプロパティの宣言に `As` 句が不足していて `Option Strict On` によりエラーが作成されるときに生成されます。 型が割り当てられていない変数は `Object` 型と見なされます。 新しいプロジェクトでの既定値はオンです。

 ID: 42020 (変数宣言)、42021 (関数宣言)、42022 (プロパティ宣言)

### <a name="possible-null-reference-exception-warnings"></a>Null 参照例外の可能性の警告
 値が割り当てられる前に変数が使われると生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42104、42030

### <a name="unused-local-variable-warning"></a>使われていないローカル変数の警告
 宣言されたローカル変数が参照されていない場合に生成されます。 既定値はオンです。

 ID: 42024

### <a name="access-of-shared-member-through-instance-variable-warning"></a>インスタンス変数による共有メンバーへのアクセスの警告
 インスタンスによる共有メンバーへのアクセスに副作用がある場合、またはインスタンス変数による共有メンバーへのアクセスが式の右辺ではないか、パラメーターとして渡されている場合に、生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42025

### <a name="recursive-operator-or-property-access-warnings"></a>演算子またはプロパティの再帰的なアクセスの警告
 ルーチンが定義されている演算子またはプロパティがルーチンの本体で使われている場合に、生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42004 (演算子)、42026 (プロパティ)

### <a name="function-or-operator-without-return-value-warning"></a>戻り値のない関数または演算子の警告
 関数または演算子で戻り値が指定されていない場合に、生成されます。 これには、関数と同じ名前を持つ暗黙のローカル変数に対する `Set` の省略も含まれます。 新しいプロジェクトでの既定値はオンです。

 ID: 42105 (関数)、42016 (演算子)

### <a name="overloads-modifier-used-in-a-module-warning"></a>モジュールで使われている修飾子のオーバーロードの警告
 `Overloads` が `Module` で使われている場合に、生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42028

### <a name="duplicate-or-overlapping-catch-blocks-warnings"></a>重複またはオーバーラップする Catch ブロックの警告
 定義されている他の `Catch` ブロックとの関係のために絶対に到達しない `Catch` ブロックがある場合に、生成されます。 新しいプロジェクトでの既定値はオンです。

 ID: 42029、42031

## <a name="see-also"></a>参照
 [[例外処理アシスタント] ダイアログボックス](../debugger/exception-assistant-dialog-box.md)の[エラーの種類](https://msdn.microsoft.com/library/3048aabf-8c97-4e13-9150-853769cb5f6f)[試行...キャッチ...Finally ステートメント](https://msdn.microsoft.com/library/d6488026-ccb3-42b8-a810-0d97b9d6472b) [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) [/warnaserror (Visual Basic)](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1) [[コンパイル] ページ、プロジェクトデザイナー (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md) [コンパイラの警告 (既定ではオフ](https://msdn.microsoft.com/library/69809cfb-a38a-4035-b154-283a61938df8))
