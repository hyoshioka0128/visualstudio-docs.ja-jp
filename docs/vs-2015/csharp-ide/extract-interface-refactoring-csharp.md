---
title: インターフェイスの抽出リファクタリング (C#) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.extractinterface
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Interface
- Extract Interface refactoring operation [C#]
ms.assetid: 7d0aa225-3b33-4331-9652-5a67cac6f3d0
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fdcf281e1ace40d1d7cdac0be302810ea173581b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667558"
---
# <a name="extract-interface-refactoring-c"></a>インターフェイスの抽出リファクタリング (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extract Interface はリファクタリング操作であり、既存のクラス、構造体、またはインターフェイスからのメンバーを含む新しいインターフェイスを簡単に作成できます。

 複数のクライアントが、クラス、構造体、またはインターフェイスのメンバーの同じサブセットを使用している場合、または複数のクラス、構造体、またはインターフェイスが共通のメンバーのサブセットを持っている場合は、インターフェイスのメンバーのサブセットを具体化すると役立つことがあります。 インターフェイスの使用方法の詳細については、「 [インターフェイス](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)」を参照してください。

 [インターフェイスの抽出] では、新しいファイルにインターフェイスが生成され、新しいファイルの先頭にカーソルが配置されます。 [ **インターフェイスの抽出** ] ダイアログボックスを使用して、どのメンバーを新しいインターフェイスに抽出するか、新しいインターフェイスの名前、および生成されるファイルの名前を指定できます。

### <a name="to-use-extract-interface"></a>Extract インターフェイスを使用するには

1. という名前のコンソールアプリケーションを作成し、を `ExtractInterface` 次のコードに置き換えます。 `Program`

    ```csharp
    // Invoke Extract Interface on ProtoA.
    // Note:  the extracted interface will be created in a new file.
    class ProtoA
    {
        public void MethodB(string s) { }
    }
    ```

2. カーソルがに配置されている状態で、 `MethodB` [**リファクター** ] メニューの [**インターフェイスの抽出**] をクリックします。

     [ **インターフェイスの抽出** ] ダイアログボックスが表示されます。

     また、キーボードショートカット CTRL + R を入力して、[ **インターフェイスの抽出** ] ダイアログボックスを表示することもできます。

     マウスを右クリックして [ **リファクター**] をポイントし、[インターフェイスの **抽出** ] をクリックして [ **インターフェイスの抽出** ] ダイアログボックスを表示することもできます。

3. [ **すべて選択] を**クリックします。

4. **[OK]** をクリックします。

     新しいファイル IProtoA.cs と、次のコードが表示されます。

    ```csharp
    using System;
    namespace TopThreeRefactorings
    {
        interface IProtoA
        {
            void MethodB(string s);
        }
    }
    ```

## <a name="remarks"></a>注釈
 この機能は、抽出するメンバーが含まれているクラス、構造体、またはインターフェイス内にカーソルが配置されている場合にのみアクセスできます。 カーソルがこの位置にある場合は、[インターフェイスの抽出] リファクタリング操作を呼び出します。

 クラスまたは構造体で extract インターフェイスを呼び出すと、新しいインターフェイス名を含むように基底クラスとインターフェイスリストが変更されます。 インターフェイスで extract インターフェイスを呼び出す場合、基底クラスとインターフェイスリストは変更されません。

## <a name="see-also"></a>参照
 [リファクタリング (C#)](../csharp-ide/refactoring-csharp.md)