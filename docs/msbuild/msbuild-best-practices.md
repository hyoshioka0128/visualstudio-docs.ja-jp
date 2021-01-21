---
title: MSBuild ベスト プラクティス | Microsoft Docs
description: 条件属性の使用やワイルドカードの未使用などの MSBuild スクリプトを記述するためのベスト プラクティスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2742324f737a4e70221e3cbe4c78cff56fa7e7ca
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047660"
---
# <a name="msbuild-best-practices"></a>MSBuild のベスト プラクティス

MSBuild スクリプトを記述するための次のベスト プラクティスを推奨します。

- 既定のプロパティ値は、コマンド ラインで既定値をオーバーライドできるプロパティを宣言するのではなく、`Condition` 属性を使用して処理することをお勧めします。 たとえば、次を使用します。

```xml
<MyProperty Condition="'$(MyProperty)' == ''">
   MyDefaultValue
</MyProperty>
```

- 通常は、項目の選択時にワイルドカードを使用しないようにします。 代わりに、ファイルを明示的に指定します。 これは、ほとんどのプロジェクトの種類では、項目の追加や削除時などのさまざまなタイミングで MSBuild によってワイルドカードが展開され、予期しない動作が発生する可能性があるためです。 これに対する例外は、ワイルドカードを正しく処理する .NET Core SDK スタイルのプロジェクト内にあります。

## <a name="see-also"></a>関連項目

- [詳細な概念](../msbuild/msbuild-advanced-concepts.md)
