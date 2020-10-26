---
title: フィールドのカプセル化リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.encapsulatefield
dev_langs:
- CSharp
helpviewer_keywords:
- Encapsulate Field refactoring operation [C#]
- refactoring [C#], Encapsulate Field
ms.assetid: bf714a04-ab1e-49ce-99ce-dda1ebb1a17f
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b4f5ddbe7eab925b06584f00b04bed3c74e9811
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667573"
---
# <a name="encapsulate-field-refactoring-c"></a>フィールドのカプセル化リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**"フィールドのカプセル化"** リファクタリング操作を使用すると、既存のフィールドからプロパティをすばやく作成し、新しいプロパティへの参照を使用してコードをシームレスに更新することができます。

 [フィールド](https://msdn.microsoft.com/library/3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7)が[パブリック](https://msdn.microsoft.com/library/0ae45d16-a551-4b74-9845-57208de1328e)の場合、他のオブジェクトはそのフィールドに直接アクセスでき、そのフィールドを所有するオブジェクトによって検出されないように変更できます。 [プロパティ](https://msdn.microsoft.com/library/e295a8a2-b357-4ee7-a12e-385a44146fa8)を使用してそのフィールドをカプセル化することで、フィールドへの直接アクセスを禁止できます。

 新しいプロパティを作成するために、 **フィールドのカプセル化** 操作によって、カプセル化するフィールドのアクセス修飾子が [private](https://msdn.microsoft.com/library/654c0bb8-e6ac-4086-bf96-7474fa6aa1c8)に変更され、そのフィールドに対して [get](https://msdn.microsoft.com/library/a52de048-fbe0-41b0-82ec-8e4ac04d3a71) アクセサーと [set](https://msdn.microsoft.com/library/30d7e4e5-cc2e-4635-a597-14a724879619) アクセサーが生成されます。 フィールドが読み取り専用で宣言されている場合など、`get` アクセサーだけが生成されることもあります。

 リファクタリングエンジンは、[**フィールドのカプセル化**] ダイアログボックスの [**参照の更新**] セクションで指定された領域で、新しいプロパティへの参照を使用してコードを更新します。

### <a name="to-create-a-property-from-a-field"></a>フィールドからプロパティを作成するには

1. `EncapsulateFieldExample` という名前のコンソール アプリケーションを作成し、`Program` を次のコード例で置き換えます。

    ```csharp
    class Square
    {
        // Select the word 'width' and then use Encapsulate Field.
        public int width, height;
    }
    class MainClass
    {
        public static void Main()
        {
            Square mySquare = new Square();
            mySquare.width = 110;
            mySquare.height = 150;
            // Output values for width and height.
            Console.WriteLine("width = {0}", mySquare.width);
            Console.WriteLine("height = {0}", mySquare.height);
        }
    }
    ```

2. [コードエディター](../ide/writing-code-in-the-code-and-text-editor.md)で、カプセル化するフィールドの名前の宣言内にカーソルを置きます。 次の例では、カーソルを `width` という語に移動します。

    ```csharp
    public int width, height;
    ```

3. [ **リファクター** ] メニューの [ **フィールドのカプセル化**] をクリックします。

     [ **フィールドのカプセル化** ] ダイアログボックスが表示されます。

     また、キーボードショートカット CTRL + R、E を入力して、[ **フィールドのカプセル化** ] ダイアログボックスを表示することもできます。

     また、カーソルを右クリックして [ **リファクター**] をポイントし、[ **フィールドのカプセル化** ] をクリックすると、[ **フィールドのカプセル化** ] ダイアログボックスが表示されます。

4. 設定を指定します。

5. Enter キーを押すか、[ **OK** ] ボタンをクリックします。

6. [ **参照の変更のプレビュー** ] オプションを選択した場合は、[参照の変更の **プレビュー** ] ウィンドウが開きます。 **[適用]** をクリックします。

     次の `get` アクセサー コードおよび `set` アクセサー コードがソース ファイルに表示されます。

    ```csharp
    public int Width
    {
        get { return width; }
        set { width = value; }
    }
    ```

     `Main` メソッドのコードも、新しい `Width` プロパティ名で更新されます。

    ```csharp
    Square mySquare = new Square();
    mySquare.Width = 110;
    mySquare.height = 150;
    // Output values for width and height.
    Console.WriteLine("width = {0}", mySquare.Width);
    ```

## <a name="remarks"></a>注釈
 **"フィールドのカプセル化"** 操作は、カーソルがフィールド宣言と同じ行に配置されている場合にのみ可能です。

 複数のフィールドを宣言する宣言では、[ **フィールドのカプセル化** ] は、コンマをフィールド間の境界として使用し、カーソルの一番上にあるフィールドとカーソルと同じ行でリファクタリングを開始します。 宣言でフィールドの名前を選択することで、カプセル化するフィールドを指定することもできます。

 このリファクタリング操作によって生成されるコードは、[フィールドのカプセル化] コード スニペット機能でモデル化されています。 コード スニペットは変更できます。 詳細については、「[Code Snippets](../ide/code-snippets.md)」を参照してください。

## <a name="see-also"></a>参照
 [リファクタリング (C#)](../csharp-ide/refactoring-csharp.md) [Visual C# のコードスニペット](../ide/visual-csharp-code-snippets.md)