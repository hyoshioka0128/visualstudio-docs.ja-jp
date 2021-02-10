---
title: パラメーターの生成リファクタリング
description: '[クイック アクションとリファクタリング] メニューを使用して、メソッドのパラメーターを自動的に生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 33e2be19e3a5a83d89e722aa0c1a1154c8196939
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968035"
---
# <a name="generate-parameter"></a>パラメーターを生成する

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** メソッドのパラメーターを自動的に生成します。

**条件:** 現在のコンテキストに存在しないメソッドの変数を参照し、エラーを受け取ります。コード修正としてパラメーターを生成できます。 

**理由:** コンテキストを失わずに、メソッドのシグネチャをすばやく変更できます。

## <a name="how-to"></a>操作方法

1. 変数名内にカーソルを置き、**Ctrl**+ **.** キーを押して、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
1. **[Generate parameter]\(パラメーターを生成する\)** を選択します。

   ![パラメーターを生成する](media/generate-parameter.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
