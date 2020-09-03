---
title: パラメーターの順序変更リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.reorder
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Reorder Parameters
- Reorder Parameters refactoring [C#]
ms.assetid: 4dabf21a-a9f0-41e9-b11b-55760cf2bd90
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e39564fb108b63859620e2c4a650608cdf1e7e82
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673140"
---
# <a name="reorder-parameters-refactoring-c"></a>パラメーター順序の再変更リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Reorder Parameters` は、メソッド、インデクサー、およびデリゲートのパラメーターの順序を簡単に変更できるようにする、Visual C# のリファクタリング操作です。 `Reorder Parameters` 宣言を変更し、メンバーが呼び出される任意の場所で、新しい順序を反映するようにパラメーターを再配置します。

 操作を実行するに `Reorder Parameters` は、メソッド、インデクサー、またはデリゲートの上または次にカーソルを置きます。 カーソルが位置にあるときに、 `Reorder Parameters` キーボードショートカットを押すか、ショートカットメニューのコマンドをクリックして、操作を呼び出します。

> [!NOTE]
> 拡張メソッドの最初のパラメーターの順序を変更することはできません。

### <a name="to-reorder-parameters"></a>パラメーターの順序を変更するには

1. という名前のクラスライブラリを作成し、を `ReorderParameters` `Class1` 次のコード例に置き換えます。

    ```csharp
    class ProtoClassA
    {
        // Invoke on 'MethodB'.
        public void MethodB(int i, bool b) { }
    }

    class ProtoClassC
    {
        void D()
        {
            ProtoClassA MyClassA = new ProtoClassA();

            // Invoke on 'MethodB'.
            MyClassA.MethodB(0, false);
        }
    }
    ```

2. `MethodB`メソッド宣言またはメソッド呼び出しの上にカーソルを置きます。

3. [ **リファクター** ] メニューの [ **パラメーターの並べ替え**] をクリックします。

     [ **パラメーターの順序** の変更] ダイアログボックスが表示されます。

4. [**パラメーターの順序**の変更] ダイアログボックスで、[パラメーター] ボックスの一覧からを選択 `int i` し、下矢印ボタンをクリックし**Parameters**ます。

     または、[ `int i` `bool b` **パラメーター** ] ボックスの一覧の [after] をドラッグすることもできます。

5. [ **パラメーターの順序** の変更] ダイアログボックスで、[ **OK]** をクリックします。

     [**パラメーターの並べ替え**] ダイアログボックスで [参照の**変更のプレビュー** ] オプションが選択されている場合は、[**変更のプレビュー-パラメーターの並べ替え**] ダイアログボックスが表示されます。 シグネチャとメソッドの呼び出しの両方で、のパラメーターリストの変更のプレビューを提供し `MethodB` ます。

    1. [ **変更のプレビュー-パラメーターの並べ替え** ] ダイアログボックスが表示されたら、[ **適用**] をクリックします。

         この例では、メソッド宣言とのすべてのメソッド呼び出しサイト `MethodB` が更新されます。

## <a name="remarks"></a>注釈
 パラメーターの順序を変更するには、メソッドの宣言またはメソッドの呼び出しを使用します。 メソッドまたはデリゲート宣言の上または上にカーソルを置き、本文には配置しません。

## <a name="see-also"></a>参照
 [リファクタリング (C#)](../csharp-ide/refactoring-csharp.md)