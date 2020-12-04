---
title: 名前空間とフォルダー名を同期する
description: '[クイック アクションとリファクタリング] メニューを使用して名前空間とフォルダー名を同期する方法を説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/12/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 10dff5d9129d1a91f01ef7541397d86f5a71468c
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96479811"
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
