---
title: '方法: インターフェイスを実装する (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- interfaces [Visual Studio], implementing
- interfaces [Visual Studio]
ms.assetid: 81d2cf46-7f60-448c-83e3-1d16bb88ca36
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6b750830e8263d0016f52a71ad4eac8c6950eda8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651864"
---
# <a name="how-to-implement-an-interface-class-designer"></a>方法: インターフェイスを実装する (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラス デザイナーのクラス ダイアグラム上で、インターフェイス メソッド用のコードを提供するクラスに接続して、インターフェイスを実装できます。 クラス デザイナーによってインターフェイス実装が生成され、インターフェイスとクラス間の関係が継承関係として表示されます。 インターフェイスとクラスの間に継承線を描画するか、インターフェイスをクラス ビューからドラッグすることにより、インターフェイスを実装できます。

> [!TIP]
> インターフェイスは、他の型を作成するのと同じ方法で作成できます。 インターフェイスが存在していてもクラス ダイアグラムに表示されていない場合は、最初にインターフェイスを表示します。 詳細については「[方法: クラス デザイナーを使用して型を作成する](../ide/how-to-create-types-by-using-class-designer.md)」および「[方法: 既存の型を表示する (クラス デザイナー)](../ide/how-to-view-existing-types-class-designer.md)」を参照してください。

### <a name="to-implement-an-interface-by-drawing-an-inheritance-line"></a>継承線を描画してインターフェイスを実装するには

1. クラス ダイアグラムで、インターフェイスおよびインターフェイスを実装するクラスを表示します。

2. クラスとインターフェイスから継承線を描画します。

    クラスにアタッチされたロリポップが表示され、インターフェイス名が表示されたラベルによって継承関係が示されます。 Visual Studio は、すべてのインターフェイス メンバーのスタブを生成します。

   詳細については、「[方法: 型の間の継承を作成する (クラス デザイナー)](../ide/how-to-create-inheritance-between-types-class-designer.md)」を参照してください。

### <a name="to-implement-an-interface-from-the-class-view-window"></a>[クラス ビュー] ウィンドウからインターフェイスを実装するには

1. クラス ダイアグラムで、インターフェイスを実装するクラスを表示します。

2. クラス ビューを開き、インターフェイスを探します。

    > [!TIP]
    > クラス ビューが開いていない場合は、 **[表示]** メニューから開きます。 クラス ビューの詳細については、「[クラスとそのメンバーを表示する](https://msdn.microsoft.com/71e9e8f3-261a-4e0c-87bf-5ec48b8bf333)」を参照してください。

3. インターフェイス ノードをダイアグラムのクラスの図形にドラッグします。

     クラスにアタッチされたロリポップが表示され、インターフェイス名が表示されたラベルによって継承関係が示されます。 Visual Studio は、すべてのインターフェイス メンバーのスタブを生成します。この時点で、インターフェイスが実装されます。

## <a name="see-also"></a>参照
 方法:[クラスデザイナーを使用して型を作成](../ide/how-to-create-types-by-using-class-designer.md)する方法[: 既存の型を表示する (クラスデザイナー)](../ide/how-to-view-existing-types-class-designer.md) [方法: 型の間の継承を作成する (クラスデザイナー)](../ide/how-to-create-inheritance-between-types-class-designer.md) [リファクタリングクラスと型 (クラスデザイナー)](../ide/refactoring-classes-and-types-class-designer.md)
