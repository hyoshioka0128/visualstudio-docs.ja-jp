---
title: インポートされていない型に対する IntelliSense 入力候補
description: '`using` ディレクティブでまだインポートしていない型に対して IntelliSense 入力候補を使用する方法です。'
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 04ea7c94d3dd24c1a511544adca9bfac3370cd71
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094267"
---
# <a name="intellisense-completion-for-unimported-types"></a>インポートされていない型に対する IntelliSense 入力候補

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** IntelliSense で、インポートされていない型に対して入力候補を提供します。

**条件:** プロジェクト内に既に依存関係はあっても、インポート ステートメントがファイルにまだ追加されていない型を、追加する必要があります。 

**理由:** インポート ステートメントをファイルに手動で追加する必要はありません。

## <a name="how-to"></a>方法

1. プロジェクト内に依存関係のある型を使い始めると、IntelliSense で提案が提供されます。
2. **Tab** キーを押します。 

   インポート ステートメントがファイルに追加されます。

   ![インポートされていない型に対する IntelliSense 入力候補](media/intellisense-completion-unimported-types.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
