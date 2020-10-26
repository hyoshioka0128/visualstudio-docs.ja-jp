---
title: パラメーターの削除リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.remove
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], removing
- refactoring [C#], Remove Parameters
- Remove Parameters refactoring [C#]
ms.assetid: f4fc3265-0ef8-4398-a691-c338178697a6
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40c373c3575f007952143e29c8dfc2cfac3d080f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667491"
---
# <a name="remove-parameters-refactoring-c"></a>パラメーターの削除リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Remove Parameters` は、メソッド、インデクサー、またはデリゲートからパラメーターを簡単に削除できるリファクタリング操作です。 パラメーターを削除すると宣言が変更されます。メンバーが呼び出される任意の場所で、新しい宣言を反映するためにパラメーターが削除されます。

 パラメーターの削除操作を実行するには、最初にメソッド、インデクサー、またはデリゲートにカーソルを配置します。 カーソルが配置されている間に、削除操作を呼び出すには `Parameters` 、[ **リファクター** ] メニューをクリックするか、キーボードショートカットを押すか、ショートカットメニューからコマンドを選択します。

> [!NOTE]
> 拡張メソッドの最初のパラメーターを削除することはできません。

### <a name="to-remove-parameters"></a>パラメーターを削除するには

1. という名前のコンソールアプリケーションを作成し、を `RemoveParameters` `Program` 次のコードに置き換えます。

    ```csharp
    class A
    {
        // Invoke on 'A'.
        public A(string s, int i) { }
    }

    class B
    {
        void C()
        {
            // Invoke on 'A'.
            A a = new A("a", 2);
        }
    }
    ```

2. メソッドの `A` 宣言またはメソッドの呼び出しのいずれかで、メソッドにカーソルを置きます。

3. [ **リファクター** ] メニューの [ **パラメーターの削除** ] をクリックして、[ **パラメーターの削除** ] ダイアログボックスを表示します。

     キーボードショートカット CTRL + R、V を入力して、[ **パラメーターの削除** ] ダイアログボックスを表示することもできます。

     また、カーソルを右クリックして [ **リファクター**] をポイントし、[ **パラメーターの削除** ] をクリックすると、[ **パラメーターの削除** ] ダイアログボックスが表示されます。

4. [ **パラメーター** ] フィールドを使用してカーソルをに移動 `int i` し、[ **削除**] をクリックします。

5. **[OK]** をクリックします。

6. [ **変更のプレビュー-パラメーターの削除** ] ダイアログボックスで、[ **適用**] をクリックします。

## <a name="remarks"></a>注釈
 メソッドの宣言またはメソッドの呼び出しからパラメーターを削除できます。 メソッド宣言またはデリゲート名にカーソルを置き、削除パラメーターを呼び出します。

> [!CAUTION]
> [パラメーターの削除] を使用すると、メンバーの本体で参照されているパラメーターを削除できますが、メソッド本体でそのパラメーターへの参照は削除されません。 これにより、コードにビルドエラーが発生する可能性があります。 ただし、リファクタリング操作を実行する前に、[ **変更のプレビュー** ] ダイアログボックスを使用してコードを確認することができます。

 削除されるパラメーターがメソッドの呼び出し中に変更された場合、パラメーターを削除すると、変更も削除されます。 たとえば、メソッドの呼び出しがから変更された場合、

```csharp
MyMethod(param1++, param2);
```

 から

```csharp
MyMethod(param2);
```

 リファクタリング操作によって、 `param1` はインクリメントされません。

## <a name="see-also"></a>参照
 [リファクタリング (C#)](../csharp-ide/refactoring-csharp.md)