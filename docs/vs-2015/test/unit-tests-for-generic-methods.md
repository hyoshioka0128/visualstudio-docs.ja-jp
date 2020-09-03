---
title: ジェネリック メソッドの単体テスト | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- generics, and unit tests
- unit tests, and generics
ms.assetid: ffc89814-a7df-44fc-aef5-dd3dfeb28a9b
caps.latest.revision: 49
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2619e975dbfd22d96db2cc382a7cebbf04a05223
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657278"
---
# <a name="unit-tests-for-generic-methods"></a>ジェネリック メソッドの単体テスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ジェネリック メソッドには、他のメソッドと同様に、単体テストを生成できます。詳細については、「[方法: 単体テストを作成して実行する](https://msdn.microsoft.com/5e0f43cf-5e51-48e2-9c98-0eb9324bdc48)」を参照してください。 次のセクションでは、ジェネリック メソッドの単体テストの作成に関する情報と例を示します。

## <a name="type-arguments-and-type-constraints"></a>型引数と型制約
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で、`MyList<T>` など、ジェネリック クラスの単体テストが生成されると、ジェネリック ヘルパー メソッドとテスト メソッドの 2 つのメソッドが生成されます。 `MyList<T>` に 1 つ以上の型制約がある場合、型引数はすべての型制約を満たす必要があります。 テスト対象のジェネリック コードが許容されたすべての入力に対して予想どおりに動作することを確認するには、テスト メソッドで、テストするすべての制約を指定して、ジェネリック ヘルパー メソッドを呼び出します。

## <a name="examples"></a>例
 ジェネリックの単体テストの例を次に示します。

- [生成されたテストコードを編集](#EditingGeneratedTestCode)しています。 この例には、「生成後のテスト コード」と「編集後のテスト コード」という 2 つのセクションがあります。 ここでは、ジェネリック メソッドから生成される未加工のテスト コードを編集して有用なテスト メソッドにする方法を示します。

- [型制約を使用](#TypeConstraintNotSatisfied)します。 この例では、型制約を使用するジェネリック メソッドの単体テストを示します。 この例では、型制約が満たされていません。

### <a name="example-1-editing-generated-test-code"></a><a name="EditingGeneratedTestCode"></a> 例 1: 生成されたテストコードの編集
 このセクションのテスト コードでは、`SizeOfLinkedList()` という名前のテスト対象コードのメソッドをテストします。 このメソッドは、リンク リスト内のノード数を示す整数を返します。

 「生成後のテスト コード」にある最初のコード例では、Visual Studio Enterprise で生成された編集前のテスト コードを示しています。 「編集後のテスト コード」にある 2 番目のコード例では、2 つのデータ型 `int` と `char` に対して SizeOfLinkedList メソッドの機能をテストする方法を示しています。

 このコードでは、2 つのメソッドを示します。

- `SizeOfLinkedListTestHelper<T>()` テスト ヘルパー メソッド。 既定では、テスト ヘルパー メソッドは名前に "TestHelper" を使用しています。

- `SizeOfLinkedListTest()` テスト メソッド。 各テスト メソッドは、TestMethod 属性でマークされています。

#### <a name="generated-test-code"></a>生成後のテスト コード
 次のテスト コードは、`SizeOfLinkedList()` メソッドから生成されました。 これは生成された編集前のテストであるため、SizeOfLinkedList メソッドを正しくテストするように変更する必要があります。

```
public void SizeOfLinkedListTestHelper<T>()
{
    T val = default(T); // TODO: Initialize to an appropriate value
    MyLinkedList<T> target = new MyLinkedList<T>(val); // TODO: Initialize to an appropriate value
    int expected = 0; // TODO: Initialize to an appropriate value
    int actual;
    actual = target.SizeOfLinkedList();
    Assert.AreEqual(expected, actual);
    Assert.Inconclusive("Verify the correctness of this test method.");
}

[TestMethod()]
public void SizeOfLinkedListTest()
{
   SizeOfLinkedListTestHelper<GenericParameterHelper>();
}
```

 上記のコードのジェネリック型パラメーターは `GenericParameterHelper` です。 このパラメーターを編集して特定のデータ型を指定できますが、次の例で示すように、このステートメントを編集せずにテストを実行できます。

#### <a name="edited-test-code"></a>編集後のテスト コード
 次のコードでは、テスト対象コードの `SizeOfLinkedList()` メソッドのテストが成功するように、テスト メソッドとテスト ヘルパー メソッドを編集しました。

##### <a name="test-helper-method"></a>テスト ヘルパー メソッド
 テスト ヘルパー メソッドは、step 1 ～ 5 というラベルの付いたコード行に対応する、次の手順を実行します。

1. ジェネリック リンク リストを作成します。

2. リンク リストに 4 つのノードを追加します。 これらのノードの内容のデータ型は不明です。

3. リンク リストの予想サイズを `expected` 変数に割り当てます。

4. リンク リストの実際のサイズを計算し、`actual` 変数に割り当てます。

5. Assert ステートメントで、`actual` と `expected` を比較します。 実際のサイズが予想サイズと異なる場合、テストは失敗します。

##### <a name="test-method"></a>テスト メソッド
 テスト メソッドは、SizeOfLinkedListTest という名前のテストの実行時に呼び出されるコードにコンパイルされます。 テスト メソッドは、step 6 と step 7 というラベルの付いたコード行に対応する、次の手順を実行します。

1. テスト ヘルパー メソッドの呼び出し時に `<int>` を指定し、`integer` 変数に対してテストを実行できることを確認します。

2. テスト ヘルパー メソッドの呼び出し時に `<char>` を指定し、`char` 変数に対してテストを実行できることを確認します。

```

public void SizeOfLinkedListTestHelper<T>()
{
    T val = default(T);
    MyLinkedList<T> target = new MyLinkedList<T>(val); // step 1
    for (int i = 0; i < 4; i++) // step 2
    {
        MyLinkedList<T> newNode = new MyLinkedList<T>(val);
        target.Append(newNode);
    }
    int expected = 5; // step 3
    int actual;
    actual = target.SizeOfLinkedList(); // step 4
    Assert.AreEqual(expected, actual); // step 5
}

[TestMethod()]
public void SizeOfLinkedListTest()
{
    SizeOfLinkedListTestHelper<int>();  // step 6
    SizeOfLinkedListTestHelper<char>(); // step 7
}
```

> [!NOTE]
> SizeOfLinkedListTest テストを実行するたびに、TestHelper メソッドは 2 回呼び出されます。 テストを成功させるには、アサート ステートメントが毎回 true と評価される必要があります。 テストが失敗した場合、`<int>` を指定した呼び出しと `<char>` を指定した呼び出しのどちらが原因でテストが失敗したかはっきりしないことがあります。 これをはっきりさせるには、コール スタックを調べるか、テスト メソッドにブレークポイントを設定してテスト実行時にデバッグします。 詳細については、「 [方法: ASP.NET ソリューションでのテストの実行中にデバッグ](https://msdn.microsoft.com/library/de4d7aa1-4a1e-467e-a19b-4a85ec245b8b)する」を参照してください。

### <a name="example-2-using-a-type-constraint"></a><a name="TypeConstraintNotSatisfied"></a> 例 2: 型制約の使用
 この例では、満たされていない型制約を使用するジェネリック メソッドの単体テストを示します。 最初のセクションでは、テスト対象コード プロジェクトのコードを示します。 型制約が強調表示されています。

 2 番目のセクションでは、テスト プロジェクトのコードを示します。

#### <a name="code-under-test-project"></a>テスト対象コード プロジェクト

```
using System;
using System.Linq;
using System.Collections.Generic;
using System.Text;

namespace ClassLibrary2
{
    public class Employee
    {
        public Employee(string s, int i)
        {
        }
    }

    public class GenericList<T> where T : Employee
    {
        private class Node
        {
            private T data;
            public T Data
            {
                get { return data; }
                set { data = value; }
            }
        }
    }
}
```

#### <a name="test-project"></a>テスト プロジェクト
 新しく生成された単体テストと同様に、有効な結果を返すように、不確定ではない Assert ステートメントをこの単体テストに追加する必要があります。 これらのステートメントは、TestMethod 属性でマークされているメソッドではなく、このテストでは `DataTestHelper<T>()` という名前の "TestHelper" メソッドに追加します。

 この例では、ジェネリック型パラメーター `T` には制約 `where T : Employee` が含まれています。 この制約は、テスト メソッドでは満たされません。 そのため、`DataTest()` メソッドには、`T` に配置された型制約を指定する要件を通知する Assert ステートメントが含まれています。 この Assert ステートメントのメッセージは、`("No appropriate type parameter is found to satisfies the type constraint(s) of T. " + "Please call DataTestHelper<T>() with appropriate type parameters.");` となります。

 つまり、`DataTest()` テスト メソッドから `DataTestHelper<T>()` メソッドを呼び出す場合は、`Employee` 型のパラメーターまたは `Employee` から派生したクラスを渡す必要があります。

 `using ClassLibrary2;`

 `using Microsoft.VisualStudio.TestTools.UnitTesting;`

 `namespace TestProject1`

```
{
    [TestClass()]
    public class GenericList_NodeTest
    {

        public void DataTestHelper<T>()
            where T : Employee
        {
            GenericList_Shadow<T>.Node target = new GenericList_Shadow<T>.Node(); // TODO: Initialize to an appropriate value
            T expected = default(T); // TODO: Initialize to an appropriate value
            T actual;
            target.Data = expected;
            actual = target.Data;
            Assert.AreEqual(expected, actual);
            Assert.Inconclusive("Verify the correctness of this test method.");
        }

        [TestMethod()]
        public void DataTest()
        {
            Assert.Inconclusive("No appropriate type parameter is found to satisfies the type constraint(s) of T. " +
            "Please call DataTestHelper<T>() with appropriate type parameters.");
        }
    }
}
```

## <a name="see-also"></a>参照
 コードの[単体テスト](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)[単体テスト](../test/unit-test-your-code.md)の構造
