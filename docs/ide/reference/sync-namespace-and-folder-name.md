---
title: 名前空間とフォルダー名を同期する
description: '[クイック アクションとリファクタリング] メニューを使用して名前空間とフォルダー名を同期する方法を説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/12/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: e4f10f3555f4edcec031cd4c144bf5a28e9c055d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967151"
---
# <a name="sync-namespace-and-folder-name"></a>名前空間とフォルダー名を同期する

このリファクタリングは以下に適用されます。

- C#

**概要:** 名前空間とフォルダー名を同期します。

**条件:** ファイルを新しいフォルダーにドラッグして、ソリューションの一部を再設計する必要があります。 

**理由:** 名前空間を新しいフォルダー構造と同じ状態に維持する必要があります。

## <a name="how-to"></a>方法

1. 名前空間の名前にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[名前空間を \<folder name> に変更します]** を選択します。

   ![名前空間とフォルダー名を同期する](media/sync-namespace-and-folder-name.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
