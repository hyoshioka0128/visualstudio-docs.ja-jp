---
title: C# コード スニペット
ms.date: 06/05/2017
ms.topic: reference
helpviewer_keywords:
- snippets [C#]
- code snippets [C#]
- Code Snippet Inserter [C#]
- C#, code snippets
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d41907a15b7e0b1692dda3f4d678c2b843dfcd03
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594163"
---
# <a name="c-code-snippets"></a>C# コード スニペット

コード スニペットは、あらかじめ用意されているコードのスニペットで、コードにすぐに挿入できます。 たとえば、`for` コード スニペットは空の `for` ループを作成します。 一部のコード スニペットは surround-with コード スニペットであり、コード行を選んでから、選んだコード行を組み込むコード スニペットを選ぶことができます。 たとえば、コード行を選んでから `for` コード スニペットをアクティブにすると、選んだコード行がループ ブロックの中に含まれる `for` ループが作成されます。 コード スニペットを使うと、速く、容易に、信頼性の高いプログラム コードを作成できます。

カーソル位置にコード スニペットを挿入したり、現在選択されているコード ブロックを囲むように surround-with コード スニペットを挿入したりすることができます。 コード スニペット挿入機能は、 **[IntelliSense]** メニューの **[コード スニペットの挿入]** または **[ブロックの挿入]** コマンドを使って、またはキーボード ショートカットの場合はそれぞれ **Ctrl**+**K**、**X** キーの順に押すか、**Ctrl**+**K**、**S** キーの順に押すことで、呼び出すことができます。

**コード スニペット挿入機能**では、すべての利用可能なコード スニペットのコード スニペット名が表示されます。 また、コード スニペット挿入機能には、コード スニペットの名前または名前の一部を入力できる入力ダイアログ ボックスもあります。 最も近いコード スニペット名が強調表示されます。 **Tab** キーを押すと、コード スニペット挿入機能が閉じて、現在選択されているコード スニペットが挿入されます。 **Esc** キーを押すか、コード エディターをマウスでクリックすると、コード スニペットを挿入することなくコード スニペット挿入機能が閉じます。

## <a name="default-code-snippets"></a>既定のコード スニペット

既定では、Visual Studio の C# には次のコード スニペットが含まれます。

|名前 (またはショートカット)|説明|スニペットを挿入できる場所|
| - |-----------------| - |
|#if|[#if](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if) ディレクティブと [#endif](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endif) ディレクティブを作成します。|任意の場所。|
|#region|[#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) ディレクティブと [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) ディレクティブを作成します。|任意の場所。|
|~|外側のクラスの[ファイナライザー](/dotnet/csharp/programming-guide/classes-and-structs/destructors) (デストラクター) を作成します。|クラスの内部。|
|属性|<xref:System.Attribute> から派生するクラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|checked|[checked](/dotnet/csharp/language-reference/keywords/checked) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|class|クラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|ctor|外側のクラスのコンストラクターを作成します。|クラスの内部。|
|cw|<xref:System.Console.WriteLine%2A> への呼び出しを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|do|[do](/dotnet/csharp/language-reference/keywords/do) `while` ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|else|[else](/dotnet/csharp/language-reference/keywords/if-else) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|enum|[enum](/dotnet/csharp/language-reference/keywords/enum) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|equals|<xref:System.Object> クラスに定義された <xref:System.Object.Equals%2A> メソッドをオーバーライドするメソッド宣言を作成します。|クラスまたは構造体の内部。|
|exception|exception (既定では <xref:System.Exception>) から派生するクラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|for|[for](/dotnet/csharp/language-reference/keywords/for) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|foreach|[foreach](/dotnet/csharp/language-reference/keywords/foreach-in) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|forr|各イテレーションの後でループ変数をデクリメントする [for](/dotnet/csharp/language-reference/keywords/for) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|if|[if](/dotnet/csharp/language-reference/keywords/if-else) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|indexer|インデクサーの宣言を作成します。|クラスまたは構造体の内部。|
|interface|[interface](/dotnet/csharp/language-reference/keywords/interface) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|invoke|イベントを安全に呼び出すブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|iterator|反復子を作成します。|クラスまたは構造体の内部。|
|iterindex|入れ子になったクラスを使って "名前付き" の反復子とインデクサーのペアを作成します。|クラスまたは構造体の内部。|
|lock|[lock](/dotnet/csharp/language-reference/keywords/lock-statement) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|mbox|<xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> への呼び出しを作成します。 場合によっては、*System.Windows.Forms.dll* への参照を追加する必要があります。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|namespace|[namespace](/dotnet/csharp/language-reference/keywords/namespace) 宣言を作成します。|名前空間 (グローバル名前空間を含む) の内部。|
|prop|[自動実装プロパティ](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)の宣言を作成します。|クラスまたは構造体の内部。|
|propfull|`get` および `set` アクセサーを持つプロパティの宣言を作成します。|クラスまたは構造体の内部。|
|propg|プライベートな `set` アクセサーを持つ読み取り専用の[自動実装プロパティ](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)を作成します。|クラスまたは構造体の内部。|
|sim|[static](/dotnet/csharp/language-reference/keywords/static) [int](/dotnet/csharp/language-reference/keywords/int) の Main メソッドの宣言を作成します。|クラスまたは構造体の内部。|
|struct|[struct](/dotnet/csharp/language-reference/keywords/struct) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|svm|[static](/dotnet/csharp/language-reference/keywords/static) [void](/dotnet/csharp/language-reference/keywords/void) の Main メソッドの宣言を作成します。|クラスまたは構造体の内部。|
|switch|[switch](/dotnet/csharp/language-reference/keywords/switch) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|try|[try-catch](/dotnet/csharp/language-reference/keywords/try-catch) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|tryf|[try-finally](/dotnet/csharp/language-reference/keywords/try-finally) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|unchecked|[unchecked](/dotnet/csharp/language-reference/keywords/unchecked) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|unsafe|[unsafe](/dotnet/csharp/language-reference/keywords/unsafe) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|using|[using](/dotnet/csharp/language-reference/keywords/using-directive) ディレクティブを作成します。|名前空間 (グローバル名前空間を含む) の内部。|
|while|[while](/dotnet/csharp/language-reference/keywords/while) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|

## <a name="see-also"></a>関連項目

- [コード スニペットの関数](../ide/code-snippet-functions.md)
- [コード スニペット](../ide/code-snippets.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [方法: surround-with コード スニペットを使用する](../ide/how-to-use-surround-with-code-snippets.md)
