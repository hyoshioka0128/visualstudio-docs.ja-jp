---
title: XML ドキュメントのコメントを挿入する
ms.date: 01/22/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 0e21d0617f954c0cc34975b7f8626b83966f6b5d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77706396"
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>方法: ドキュメント生成のための XML コメントを挿入する

Visual Studio では、クラスやメソッドなどのコード要素を文書化しやすいように、標準的な XML ドキュメント コメント構造を自動的に生成できます。 コンパイル時に、ドキュメントのコメントを含む XML ファイルを生成できます。

> [!TIP]
> 生成された XML ファイルの場所と名前を構成する方法については、「[XML コメントによるコードの文書化 (C# ガイド)](/dotnet/csharp/codedoc)」をご覧ください。

コンパイラによって生成された XML ファイルは、.NET アセンブリと共に配布できます。これにより、Visual Studio や他の IDE で、IntelliSense を使って型やメンバーに関する概要情報を表示できます。 さらに、[DocFX](https://dotnet.github.io/docfx/) や [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) のようなツールを使用して XML ファイルを実行し、API リファレンスの Web サイトを生成することができます。

> [!NOTE]
> XML ドキュメントのコメントを自動的に挿入する **[コメントの挿入]** コマンドは、[C#](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments) と [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation) で使うことができます。 ただし、[C++ ファイルに XML ドキュメントのコメント](/cpp/build/reference/xml-documentation-visual-cpp)を手動で挿入し、コンパイル時に XML ドキュメント ファイルを生成することもできます。

## <a name="to-insert-xml-comments-for-a-code-element"></a>コード要素の XML コメントを挿入するには

1. メソッドなど、ドキュメント化する要素の上にテキスト カーソルを置きます。

2. 次のいずれかの操作を行います。

   - C# では「`///`」と入力し、Visual Basic では「`'''`」と入力します

   - **[編集]** メニューから、 **[IntelliSense]**  >  **[コメントの挿入]** の順に選択します

   - コード要素の前面またはすぐ上に表示される右クリック メニューまたはコンテキスト メニューから、 **[スニペット]**  >  **[コメントの挿入]** の順に選択します

   すぐに、XML テンプレートがコード要素の上に生成されます。 たとえば、メソッドのコメントを生成すると、 **\<summary\>** 要素、各パラメーターの **\<param\>** 要素、および戻り値を文書化するための **\<returns\>** 要素が生成されます。

   ![XML コメント テンプレート - C#](media/doc-preview-cs.png)

   ![XML コメント テンプレート - Visual Basic](media/doc-preview-vb.png)

3. 各 XML 要素の説明を入力し、コード要素を完全に文書化します。

   ![完了したコメント](media/doc-result-cs.png)

要素の上にカーソルを置くとクイック ヒントに表示される、XML コメントのスタイルを使用できます。 これらのスタイルには、斜体、太字、箇条書き、クリック可能なリンクなどがあります。

   ![完了したコメント](media/doc-style-cs.png) 

> [!NOTE]
> `///` (C#) または `'''` (Visual Basic) を入力した後で XML ドキュメントのコメントを切り替えるための[オプション](../../ide/reference/options-text-editor-csharp-advanced.md)があります。 メニュー バーから **[ツール]**  >  **[オプション]** の順に選択して、 **[オプション]** ダイアログ ボックスを開きます。 次に、 **[テキスト エディター]**  >  **[C#]** または **[Basic]**  >  **[詳細]** の順に移動します。 **[エディターのヘルプ]** セクションで、 **[XML ドキュメントを生成する]** オプションを探します。

## <a name="see-also"></a>参照

- [XML ドキュメント コメント (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [XML コメントによるコードの文書化 (C# ガイド)](/dotnet/csharp/codedoc)
- [方法: XML ドキュメントを作成する (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [C++ のコメント](/cpp/cpp/comments-cpp)
- [XML ドキュメント (C++)](/cpp/build/reference/xml-documentation-visual-cpp)
- [コード生成](../code-generation-in-visual-studio.md)
