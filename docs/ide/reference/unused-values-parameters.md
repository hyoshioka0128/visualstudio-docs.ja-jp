---
title: 使用されていない値とパラメーター
ms.date: 02/15/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ce2b0f1e0c0db45c478c3917306683b314da0564
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "65531876"
---
# <a name="unused-value-assignments-variables-and-parameters"></a>未使用値の割り当て、変数、およびパラメーター

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** 使用されていないパラメーターをフェードアウトし、使用されていない式の値に警告を生成します。 コンパイラでは、使用されていない割り当てを検索するフロー分析も実行されます。 使用されていない値割り当てはフェードアウトし、冗長の割り当てを削除するための[クイック アクション](../quick-actions.md)が電球と一緒に表示されます。 不明な値を持つ変数が使用されていない場合、代わりに[ディスカード](/dotnet/csharp/discards)の使用を提案する [[クイック アクション]](../quick-actions.md) が表示されます ディスカードは、アプリケーション コード内で意図的に使用しない一時的なダミー変数です。 これにより、メモリの割り当てが削減されるので、コードを読みやすくなります)。

**条件:** まったく使用されていない割り当て、パラメーター、または式の値があります。

**理由:** 値の割り当て、変数、パラメーターが使用されなくなったかどうかを判断するのは難しい場合があります。 そのような値をフェードアウトするか警告を生成することで、削除するコードが視覚的にわかりやすくなります。

## <a name="unused-expression-values-and-parameters-diagnostic"></a>使用されていない式の値とパラメーターの診断

1. 使用されていない値割り当て、変数、またはパラメーターがあります。
2. 使用されていない値割り当てまたはパラメーターはフェードアウトしているように表示されます。使用されていない式の値によって、警告が生成されます。

  ![使用されていないパラメーター](media/unused-parameter.png)
  ![使用されていない値](media/unused-value.png)
  ![使用されていない値割り当て](media/unused-value-assignment.png)
  ![使用されていない値ディスカード](media/unused-value-discard.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../csharp-developer-productivity.md)
