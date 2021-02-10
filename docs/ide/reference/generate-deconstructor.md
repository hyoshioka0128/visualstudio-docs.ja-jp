---
title: デコンストラクターのクイック アクションを生成する
description: '[クイック アクションとリファクタリング] メニューを使用して、新しいデコンストラクターのメソッド スタブをすぐに生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: a4c243ab46858a4c8eb944d485900718b685bf5c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897959"
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