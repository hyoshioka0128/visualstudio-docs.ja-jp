---
title: メソッドの抽出リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Method
- Extract Method refactoring operation [C#]
ms.assetid: eeba11df-a815-4bec-9c21-8a831891b783
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6e6d5e7913a7433fd4b30da490f33dd614c3e2b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667539"
---
# <a name="extract-method-refactoring-c"></a>メソッドの抽出リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Extract メソッド** は、既存のメンバーのコードフラグメントから新しいメソッドを簡単に作成できるリファクタリング操作です。

 **Extract メソッド**を使用して、既存のメンバーのコードブロック内から選択したコードを抽出することで、新しいメソッドを作成できます。 抽出された新しいメソッドには、選択したコードが含まれ、既存のメンバー内の選択したコードが新しいメソッドの呼び出しで置き換えられます。 コードのフラグメントを独自のメソッドに変えることで、再利用と読みやすさを向上させるために、コードをすばやく正確に再構成できます。

 **Extract メソッド** には、次のような利点があります。

- では、再利用可能な不連続メソッドを強調することで、コーディングのベストプラクティスを推奨します。

- 適切な組織を通じてコードを自己文書化することをお勧めします。

     わかりやすい名前が使用されている場合、高度なメソッドは一連のコメントに似ています。

- より詳細なメソッドを作成して、オーバーライドを簡略化することをお勧めします。

- コードの重複を減らします。

### <a name="to-use-extract-method"></a>Extract メソッドを使用するには

1. `ExtractMethod` という名前のコンソール アプリケーションを作成し、`Program` を次のコード例で置き換えます。

    ```csharp
    class A
    {
        const double PI = 3.141592;

        double CalculatePaintNeeded(double paintPerUnit, double radius)
        {
            // Select any of the following:
            // 1. The entire next line of code.
            // 2. The right-hand side of the next line of code.
            // 3. Just "PI *" of the right-hand side of the next line
            //    of code (to see the prompt for selection expansion).
            // 4.  All code within the method body.
            // ...Then invoke Extract Method.

            double area = PI * radius * radius;

            return area / paintPerUnit;
        }
    }
    ```

2. 抽出するコードフラグメントを選択します。

    ```csharp
    double area = PI * radius * radius;
    ```

3. [ **リファクター** ] メニューの [ **メソッドの抽出**] をクリックします。

     [ **メソッドの抽出** ] ダイアログボックスが表示されます。

     または、キーボードショートカット CTRL + R、M を入力して、[ **メソッドの抽出** ] ダイアログボックスを表示することもできます。

     選択したコードを右クリックして [ **リファクター**] をポイントし、[ **メソッドの抽出** ] をクリックして [ **メソッドの抽出** ] ダイアログボックスを表示することもできます。

4. [ `CircleArea` **新しいメソッド名** ] ボックスに、のように、新しいメソッドの名前を指定します。

     [ **プレビューメソッドシグネチャ**] の下に、新しいメソッドシグネチャのプレビューが表示されます。

5. **[OK]** をクリックします。

## <a name="remarks"></a>注釈
 [ **メソッドの抽出** ] コマンドを使用すると、同じクラスのソースメンバーの後に新しいメソッドが挿入されます。

## <a name="partial-types"></a>部分型
 クラスが部分型の場合は、 **Extract メソッド** によって、ソースメンバーの直後に新しいメソッドが生成されます。 **Extract メソッド** は、新しいメソッドのシグネチャを決定し、新しいメソッドのコードによってインスタンスデータが参照されない場合に静的メソッドを作成します。

## <a name="generic-type-parameters"></a>ジェネリック型の型パラメーター
 制約のないジェネリック型パラメーターを持つメソッドを抽出した場合、生成されたコードは、 `ref` 値が割り当てられていない限り、そのパラメーターに修飾子を追加しません。 抽出されたメソッドが、ジェネリック型引数として参照型をサポートする場合は、メソッドシグネチャのパラメーターに修飾子を手動で追加する必要があり `ref` ます。

## <a name="anonymous-methods"></a>匿名メソッド
 匿名メソッドの外部で宣言または参照されているローカル変数への参照を含む匿名メソッドの一部を抽出しようとすると、セマンティック変更の可能性について Visual Studio から警告が表示されます。

 匿名メソッドでローカル変数の値を使用すると、匿名メソッドが実行された時点で値が取得されます。 匿名メソッドを別のメソッドに抽出すると、抽出されたメソッドの呼び出しの時点でローカル変数の値が取得されます。

 次の例は、このセマンティックの変更を示しています。 このコードが実行されると、 **11** がコンソールに出力されます。 **Extract メソッド**を使用して、コードコメントでマークされているコードの領域を独自のメソッドに抽出してから、リファクタリングしたコードを実行すると、 **10**がコンソールに出力されます。

```csharp
class Program
{
    delegate void D();
    D d;
    static void Main(string[] args)
    {
        Program p = new Program();
        int i = 10;
        /*begin extraction*/
            p.d = delegate { Console.WriteLine(i++); };
        /*end extraction*/
        i++;
        p.d();
    }
}
```

 このような状況を回避するには、クラスの匿名メソッドフィールドで使用されるローカル変数を作成します。

## <a name="see-also"></a>参照
 [リファクタリング (C#)](../csharp-ide/refactoring-csharp.md)