---
title: エスケープする特殊文字 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- special characters to escape
- msbuild, special characters to escape
ms.assetid: 5b5172c3-41e4-4f38-a16f-2aeac831a5fc
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1b17ded468e262d4f636ed5494081adab7b8c5f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632252"
---
# <a name="special-characters-to-escape"></a>エスケープする特殊文字

特殊文字は、使用するコンテキストで特別な意味を持つ場合にのみ、エスケープする必要があります。 たとえば、アスタリスク (*) は、項目定義の Include 属性と Exclude 属性、または <xref:Microsoft.Build.Tasks.CreateItem> の呼び出しでのみ、特殊文字となります。 その他のすべての場合において、アスタリスクはリテラルのアスタリスクとして扱われます。 プロジェクト ファイルではアスタリスクをエスケープする必要はありませんが、そのようにしても問題はありません。

 特殊文字の代わりに %\<xx> という表記を使用します。ここで、\<xx> は ASCII 文字の 16 進値を表します。 たとえば、アスタリスク (*) をリテラル文字として使用するには、値 `%2A` を使用します。

 エスケープする特殊文字の完全な一覧は次のとおりです。

|文字|説明|
|---------------|-----------------|
|%|パーセント記号は、メタデータを参照するために使用します。|
|$|ドル記号は、プロパティを参照するために使用します。|
|@|アット マークは、項目一覧を参照するために使用します。|
|(|左かっこは、一覧で使用します。|
|)|右かっこは、一覧で使用します。|
|;|セミコロンは、リスト区切り記号です。|
|?|疑問符は、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|
|*|アスタリスクは、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|

> [!NOTE]
> シナリオによっては、`Exec` タスク内で使用する場合などに、二重引用符 (") 文字をエスケープする必要があります。

## <a name="see-also"></a>関連項目

- [方法: MSBuild で特殊文字をエスケープする](../msbuild/how-to-escape-special-characters-in-msbuild.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
