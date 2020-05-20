---
title: '方法: インターフェイスを実装する (クラス デザイナー)'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interfaces [Visual Studio], implementing
- interfaces [Visual Studio]
ms.assetid: 81d2cf46-7f60-448c-83e3-1d16bb88ca36
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbe8db6c6bd7df5285880f7f860df5bb26db736a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590112"
---
# <a name="how-to-implement-an-interface-in-class-designer"></a>方法: クラス デザイナーでインターフェイスを実装する

**クラス デザイナー**のクラス ダイアグラム上で、インターフェイス メソッド用のコードを提供するクラスに接続して、インターフェイスを実装できます。 **クラス デザイナー**によってインターフェイス実装が生成され、インターフェイスとクラス間の関係が継承関係として表示されます。 インターフェイスとクラスの間に継承線を描画するか、インターフェイスをクラス ビューからドラッグすることにより、インターフェイスを実装できます。

> [!TIP]
> インターフェイスは、他の型を作成するのと同じ方法で作成できます。 インターフェイスが存在していてもクラス ダイアグラムに表示されていない場合は、最初にインターフェイスを表示します。 詳細については、[クラス デザイナーを使用して型を作成する](how-to-create-types.md)」および「[方法:既存の型を表示する](how-to-view-existing-types.md)」を参照してください。

## <a name="to-implement-an-interface-by-drawing-an-inheritance-line"></a>継承線を描画してインターフェイスを実装するには

1. クラス ダイアグラムで、インターフェイスおよびインターフェイスを実装するクラスを表示します。

2. クラスとインターフェイスから継承線を描画します。

     クラスにアタッチされたロリポップが表示され、インターフェイス名が表示されたラベルによって継承関係が示されます。 Visual Studio は、すべてのインターフェイス メンバーのスタブを生成します。

詳細については、[型間の継承の作成](how-to-create-inheritance-between-types.md)に関するページを参照してください。

## <a name="to-implement-an-interface-from-the-class-view-window"></a>[クラス ビュー] ウィンドウからインターフェイスを実装するには

1. クラス ダイアグラムで、インターフェイスを実装するクラスを表示します。

2. **クラス ビュー**を開き、インターフェイスを探します。

    > [!TIP]
    > **クラス ビュー**が開いていない場合は、**[表示]** メニューから、または **Ctrl**+**Shift**+**C** キーを押して、**クラス ビュー**を開きます。

3. インターフェイス ノードをダイアグラムのクラスの図形にドラッグします。

     クラスにアタッチされたロリポップが表示され、インターフェイス名が表示されたラベルによって継承関係が示されます。 Visual Studio は、すべてのインターフェイス メンバーのスタブを生成します。この時点で、インターフェイスが実装されます。

## <a name="see-also"></a>関連項目

- [方法: クラス デザイナーを使用して型を作成する](how-to-create-types.md)
- [方法: 既存の型を表示する](how-to-view-existing-types.md)
- [方法: 型の間の継承を作成する](how-to-create-inheritance-between-types.md)
- [クラスおよび型のリファクタリング](refactoring-classes-and-types.md)
