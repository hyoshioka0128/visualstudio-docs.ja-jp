---
title: MSBuild 既知のアイテム メタデータ | Microsoft Docs
description: 作成時にすべての項目に割り当てられる MSBuild メタデータと、ビルド動作を制御するために定義できるいくつかのオプションの MSBuild メタデータについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, item metadata
- MSBuild, well-known item metadata
ms.assetid: b5e791b5-c68f-4978-ad8a-9247d03bb6c0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 047fe5ef6edc57681b8382a9f2a1069991e0f513
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93049011"
---
# <a name="msbuild-well-known-item-metadata"></a>MSBuild の既知の項目メタデータ

項目メタデータは、項目に添付される値です。 項目が作成されるときに MSBuild によって項目に割り当てられるものもありますが、任意のメタデータを必要に応じて定義することもできます。 一部のユーザー定義メタデータの値は、MSBuild、特定のタスク、または .NET SDK などの SDK にとって意味があります。

この記事の最初の表では、すべての項目の作成時に割り当てられるメタデータについて説明します。 次の表は、MSBuild に対して意味を持ついくつかの省略可能なメタデータを示しています。定義することでビルドの動作を制御できます。 それぞれの例で、 *C:\MyProject\Source\Program.cs* ファイルをプロジェクトに含めるために次のアイテム宣言が使用されました。

```xml
<ItemGroup>
    <MyItem Include="Source\Program.cs" />
</ItemGroup>
```

|項目メタデータ|説明|
|-------------------|-----------------|
|%(FullPath)|アイテムの完全パスが含まれます。 次に例を示します。<br /><br /> *C:\MyProject\Source\Program.cs*|
|%(RootDir)|アイテムのルート ディレクトリが含まれます。 次に例を示します。<br /><br /> *C:\\*|
|%(Filename)|拡張子の付かない、アイテムのファイル名が含まれます。 次に例を示します。<br /><br /> *Program*|
|%(Extension)|アイテムのファイル名の拡張子が含まれます。 次に例を示します。<br /><br /> *.cs*|
|%(RelativeDir)|`Include` 属性に指定されたパスが最後の円記号 (\\) まで含まれます。 次に例を示します。<br /><br /> *Source\\*<br /><br /> `Include` 属性が完全パスの場合、`%(RelativeDir)` はルート ディレクトリ `%(RootDir)` で始まります。  次に例を示します。 <br /><br /> *C:\MyProject\Source\\*|
|%(Directory)|ルート ディレクトリのないアイテムのディレクトリが含まれます。 次に例を示します。<br /><br /> *MyProject\\Source\\*|
|%(RecursiveDir)|`Include` 属性にワイルドカード \*\* が含まれる場合、このメタデータはワイルドカードを置き換えるパスの一部を指定します。 ワイルドカードの詳細については、「[方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」を参照してください。<br /><br /> *C:\MySolution\MyProject\Source\\* フォルダーに *Program.cs* ファイルが格納されている場合、およびプロジェクト ファイルに次のアイテムが含まれている場合:<br /><br /> `<ItemGroup>`<br /><br /> `<MyItem Include="C:\**\Program.cs" />`<br /><br /> `</ItemGroup>`<br /><br /> `%(MyItem.RecursiveDir)` の値は *MySolution\MyProject\Source\\* です。|
|%(Identity)|`Include` 属性で指定されたアイテム。 次に例を示します。<br /><br /> *Source\Program.cs*|
|%(ModifiedTime)|アイテムが最後に変更された時間からのタイムスタンプが含まれます。 次に例を示します。<br /><br /> `2004-07-01 00:21:31.5073316`|
|%(CreatedTime)|アイテムが作成された時間からのタイムスタンプが含まれます。 次に例を示します。<br /><br /> `2004-06-25 09:26:45.8237425`|
|%(AccessedTime)|アイテムが最後にアクセスされた時間からのタイムスタンプが含まれます。<br /><br /> `2004-08-14 16:52:36.3168743`|

## <a name="see-also"></a>関連項目

- [一般的な MSBuild 項目メタデータ](common-msbuild-item-metadata.md)
- [項目](../msbuild/msbuild-items.md)
- [バッチ処理](../msbuild/msbuild-batching.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
