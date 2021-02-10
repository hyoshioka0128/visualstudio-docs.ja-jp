---
title: エスケープする特殊文字 | Microsoft Docs
description: 使用されているコンテキストで特別な意味を持つ場合にのみエスケープする必要がある特殊文字について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5e665c214ea75de67a6c339bb516dfb812936448
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99878150"
---
# <a name="special-characters-to-escape"></a>エスケープする特殊文字

特殊文字は、使用するコンテキストで特別な意味を持つ場合にのみ、エスケープする必要があります。 たとえば、アスタリスク (*) は、項目定義の Include 属性と Exclude 属性、または <xref:Microsoft.Build.Tasks.CreateItem> の呼び出しでのみ、特殊文字となります。 その他のすべての場合において、アスタリスクはリテラルのアスタリスクとして扱われます。 プロジェクト ファイルではアスタリスクをエスケープする必要はありませんが、そのようにしても問題はありません。

 特殊文字の代わりに %\<xx> という表記を使用します。ここで、\<xx> は ASCII 文字の 16 進値を表します。 たとえば、アスタリスク (*) をリテラル文字として使用するには、値 `%2A` を使用します。

 エスケープする特殊文字の完全な一覧は次のとおりです。

|文字|ASCII エンコード|説明|
|---------|----------|-----------|
|%|%25|パーセント記号は、メタデータを参照するために使用します。|
|$|%24|ドル記号は、プロパティを参照するために使用します。|
|@|%40|アット マークは、項目一覧を参照するために使用します。|
|(|%28|左かっこは、一覧で使用します。|
|)|%29|右かっこは、一覧で使用します。|
|;|%3B|セミコロンは、リスト区切り記号です。|
|?|%3F|疑問符は、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|
|* |%2A|アスタリスクは、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|

> [!NOTE]
> シナリオによっては、`Exec` タスク内で使用する場合などに、二重引用符 (") 文字をエスケープする必要があります。

## <a name="see-also"></a>関連項目

- [方法: MSBuild で特殊文字をエスケープする](../msbuild/how-to-escape-special-characters-in-msbuild.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
