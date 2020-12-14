---
title: デコンストラクターのクイック アクションを生成する
description: '[クイック アクションとリファクタリング] メニューを使用して、新しいデコンストラクターのメソッド スタブをすぐに生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: ff2ac7682eff1c3da0597a95945a6a0b016d9213
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617254"
---
# <a name="generate-a-deconstructor-in-visual-studio"></a>Visual Studio でデコンストラクターを生成する

このコード生成は以下に適用されます。

- C#

**概要:** 新しいデコンストラクターのメソッド スタブをすぐに生成できます。

**条件:** 型を自動的に正しく分解します。

**理由:** デコンストラクターの型は手動で指定できますが、この機能では、正しい out パラメーターと共にスタブが生成されます。

## <a name="generate-a-deconstructor"></a>デコンストラクターを生成する

1. out パラメーターを指定し、新しい型を宣言します。 この宣言により、宣言に一致するデコンストラクト インスタンスが見つからないとき、エラーが発生します。

   ![デコンストラクター不足エラー](media/deconstruct.png)

2. 次のいずれかのステップを使用します。

   - **[キーボード]**
      - 宣言にカーソルを置き、Ctrl + . キーを選択します **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。
      - テキスト カーソルが既にクラスの空の行の上にある場合に、左余白に表示される :::image type="icon" source="media/screwdriver.png"::: アイコンを選択します。

      ![デコンストラクターの生成のコード修正](media/deconstruct-codefix.png)

3. **[Generate method 'MyInternalClass.Deconstruct']\(メソッド 'MyInternalClass.Deconstruct' の生成\)** を選択し、デコンストラクターを生成します。

   ![結果的に生成されるデコンストラクター コード](media/deconstruct-result.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)