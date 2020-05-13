---
title: Visual C# のコード スニペット | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- snippets [C#], default snippets
- snippets [C#], Code Snippet Inserter
- Code Snippet Inserter [J#]
- Code Snippet Inserter [C#]
- Visual C#, default snippets
ms.assetid: dbea3dd6-e650-4190-b874-c9f097d7de6e
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fb84854bd871277f680a753b28c17e3429283928
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646721"
---
# <a name="visual-c-code-snippets"></a>Visual C# のコード スニペット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード スニペットは、あらかじめ用意されているコードのスニペットで、コードにすぐに挿入できます。 たとえば、`for` コード スニペットは空の `for` ループを作成します。 一部のコード スニペットは surround-with コード スニペットであり、コード行を選んでから、選んだコード行を組み込むコード スニペットを選ぶことができます。 たとえば、コード行を選んでから `for` コード スニペットをアクティブにすると、選んだコード行がループ ブロックの中に含まれる `for` ループが作成されます。 コード スニペットを使うと、速く、容易に、信頼性の高いプログラム コードを作成できます。

 カーソル位置にコード スニペットを挿入したり、現在選択されているコード ブロックを囲むように surround-with コード スニペットを挿入したりすることができます。 コード スニペット挿入機能は、**IntelliSense** メニューの **[コード スニペットの挿入]** または **[ブロックの挿入]** コマンドで、または Ctrl キーを押しながら T キー、X キーの順に押すか、Ctrl キーを押しながら K キー、S キーの順に押すことで、起動できます。

 コード スニペット挿入機能では、すべての利用可能なコード スニペットのコード スニペット名が表示されます。 また、コード スニペット挿入機能には、コード スニペットの名前または名前の一部を入力できる入力ダイアログ ボックスもあります。 最も近いコード スニペット名が強調表示されます。 Tab キーを押すと、コード スニペット挿入機能が閉じて、現在選択されているコード スニペットが挿入されます。 Esc キーを押すか、コード エディターをマウスでクリックすると、コード スニペットを挿入することなくコード スニペット挿入機能が閉じます。

## <a name="default-code-snippets"></a>既定のコード スニペット
 既定では、Visual Studio には次のコード スニペットが含まれます。

|名前 (またはショートカット)|説明|スニペットを挿入できる場所|
|--------------------------|-----------------|---------------------------------------|
|#if|[#if](https://msdn.microsoft.com/library/48cabbff-ca82-491f-a56a-eeccd528c7c2) ディレクティブと [#endif](https://msdn.microsoft.com/library/6a5fca55-5aee-441f-86f6-1c99fbe9ec05) ディレクティブを作成します。|任意の場所。|
|#region|[#region](https://msdn.microsoft.com/library/672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4) ディレクティブと [#endregion](https://msdn.microsoft.com/library/16099660-91b2-49e5-9646-77f9ef069526) ディレクティブを作成します。|任意の場所。|
|~|外側のクラスのデストラクターを作成します。|クラスの内部。|
|属性|<xref:System.Attribute> から派生するクラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|checked|[checked](https://msdn.microsoft.com/library/718a1194-988d-48a3-b089-d6ee8bd1608d) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|class|クラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|ctor|外側のクラスのコンストラクターを作成します。|クラスの内部。|
|cw|<xref:System.Console.WriteLine%2A> への呼び出しを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|do|[do](https://msdn.microsoft.com/library/50725f79-9ba6-4898-aa78-6e331568a1bb)`while` ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|else|[else](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|enum|[enum](https://msdn.microsoft.com/library/bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|equals|<xref:System.Object> クラスに定義された <xref:System.Object.Equals%2A> メソッドをオーバーライドするメソッド宣言を作成します。|クラスまたは構造体の内部。|
|exception|exception (既定では <xref:System.Exception>) から派生するクラスの宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|for|[for](https://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|foreach|[foreach](https://msdn.microsoft.com/library/5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|forr|各イテレーションの後でループ変数をデクリメントする [for](https://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|if|[if](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|indexer|インデクサーの宣言を作成します。|クラスまたは構造体の内部。|
|interface|[interface](https://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|invoke|イベントを安全に呼び出すブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|iterator|反復子を作成します。|クラスまたは構造体の内部。|
|iterindex|入れ子になったクラスを使って "名前付き" の反復子とインデクサーのペアを作成します。|クラスまたは構造体の内部。|
|lock|[lock](https://msdn.microsoft.com/library/656da1a4-707e-4ef6-9c6e-6d13b646af42) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|mbox|<xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> への呼び出しを作成します。 場合によっては、System.Windows.Forms.dll への参照を追加する必要があります。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|namespace|[namespace](https://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f) 宣言を作成します。|名前空間 (グローバル名前空間を含む) の内部。|
|prop|[自動実装プロパティ](https://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7)の宣言を作成します。|クラスまたは構造体の内部。|
|propfull|get および set アクセサーを持つプロパティの宣言を作成します。|クラスまたは構造体の内部。|
|propg|プライベートな "set" アクセサーを持つ読み取り専用の[自動実装プロパティ](https://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7)を作成します。|クラスまたは構造体の内部。|
|sim|[static](https://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf) [int](https://msdn.microsoft.com/library/212447b4-5d2a-41aa-88ab-84fe710bdb52) の Main メソッドの宣言を作成します。|クラスまたは構造体の内部。|
|struct|[struct](https://msdn.microsoft.com/library/ff3dd9b7-dc93-4720-8855-ef5558f65c7c) 宣言を作成します。|名前空間 (グローバル名前空間を含む)、クラス、または構造体の内部。|
|svm|[static](https://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf) [void](https://msdn.microsoft.com/library/0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4) の Main メソッドの宣言を作成します。|クラスまたは構造体の内部。|
|switch|[switch](https://msdn.microsoft.com/library/44bae8b8-8841-4d85-826b-8a94277daecb) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|try|[try-catch](https://msdn.microsoft.com/library/cb5503c7-bfa1-4610-8fc2-ddcd2e84c438) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|tryf|[try-finally](https://msdn.microsoft.com/library/c27623fb-7261-4464-862c-7a369d3c8f0a) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|unchecked|[unchecked](https://msdn.microsoft.com/library/0c021f7c-923f-4b3d-a58f-55336f5ac27e) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|unsafe|[unsafe](https://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0) ブロックを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|
|使用|[using](https://msdn.microsoft.com/library/b42b8e61-5e7e-439c-bb71-370094b44ae8) ディレクティブを作成します。|名前空間 (グローバル名前空間を含む) の内部。|
|while|[while](https://msdn.microsoft.com/library/72a0765c-6852-4aca-b327-4a11cb7f5c59) ループを作成します。|メソッド、インデクサー、プロパティ アクセサー、またはイベント アクセサーの内部。|

## <a name="see-also"></a>関連項目
 [コードスニペット関数](../ide/code-snippet-functions.md)[コードスニペット](../ide/code-snippets.md)は、次のように [How ます。置換を使用して新しいスニペットを作成し ](https://msdn.microsoft.com/8d56d43c-097a-475b-aa85-cae1554b6338)[テンプレートパラメーター](../ide/template-parameters.md) [How に置き換えます。次に [How ](../ide/how-to-use-surround-with-code-snippets.md) には、ブロックを挿入するコードスニペットを使用します。C# リファクタリング スニペットを復元する](../ide/how-to-restore-csharp-refactoring-snippets.md)
