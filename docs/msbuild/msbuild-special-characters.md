---
title: MSBuild の特殊文字 | Microsoft Docs
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- escape characters
- escape
- MSBuild Escape Characters
ms.assetid: 545e6a59-1093-4514-935e-78679a46fb3c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fdc9024db06fe27fab5dfdf9589300a6eb671368
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633214"
---
# <a name="msbuild-special-characters"></a>MSBuild の特殊文字

MSBuild では、特定のコンテキストで特別な使い方をするためにいくつかの文字が予約されています。 予約されている文脈でそのような文字を文字通り使用するには、エスケープする必要があります。 たとえば、アスタリスクは、項目定義の `Include` 属性と `Exclude` 属性、ならびに `CreateItem` の呼び出しで特別な意味を持ちます。 このような文脈でアスタリスクをアスタリスクとして表示するには、エスケープする必要があります。 その他の文脈では、アスタリスクを使う場所でそれを入力できます。

 特殊文字をエスケープするには、構文 %\<xx> を使用します。ここで、\<xx> は文字の ASCII 16 進値を表します。 詳細については、[MSBuild で特殊文字をエスケープする](../msbuild/how-to-escape-special-characters-in-msbuild.md)」を参照してください。

## <a name="special-characters"></a>特殊文字

 MSBuild の特殊文字の一覧を、次の表に示します。

|**文字**|**ASCII**|**予約されている使用方法**|
|-------------------|---------------|------------------------|
|%|%25|メタデータを参照する|
|$|%24|プロパティを参照する|
|@|%40|項目一覧を参照する|
|'|%27|条件とその他の式|
|;|%3B|一覧の区切り記号|
|?|%3F|`Include` 属性と `Exclude` 属性のファイル名のワイルドカード文字|
|*|%2A|`Include` 属性と `Exclude` 属性のファイル名で使用するワイルドカード文字|

## <a name="see-also"></a>関連項目

- [詳細な概念](../msbuild/msbuild-advanced-concepts.md)
- [項目](../msbuild/msbuild-items.md)
