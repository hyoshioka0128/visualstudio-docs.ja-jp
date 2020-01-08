---
title: '方法: MSBuild で特殊文字をエスケープする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- special characters, escaping
- characters, escapes
- escape characters
- MSBuild, escaping special characters
ms.assetid: 1aa3669c-1647-4960-b770-752e2532102f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 955739372605b9e4f9fe58f73669322e2724de31
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595008"
---
# <a name="how-to-escape-special-characters-in-msbuild"></a>方法: MSBuild で特殊文字をエスケープする

[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクト ファイルでは、特定の文字が特殊な意味を持ちます。 そのような文字の例として、セミコロン (`;`) およびアスタリスク (`*`) があります。 特殊文字の完全な一覧については、「[MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)」を参照してください。

これらの特殊文字をプロジェクト ファイル内でリテラルとして使用するには、構文 `%<xx>` を使ってそれらの文字を指定する必要があります。ここで、`<xx>` は文字の ASCII 16 進値を表します。

## <a name="msbuild-special-characters"></a>MSBuild の特殊文字

特殊文字が使用される場所の 1 つの例として、アイテム一覧の `Include` 属性が挙げられます。 たとえば、次のアイテム一覧では、*MyFile.cs* と *MyClass.cs* の 2 つのアイテムを宣言しています。

```xml
<Compile Include="MyFile.cs;MyClass.cs"/>
```

名前にセミコロンを含むアイテムを宣言する場合は、構文 `%<xx>` を使用してセミコロンをエスケープし、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] によって 2 つの別々のアイテムが宣言されることを防ぐ必要があります。 たとえば、次のアイテムではセミコロンをエスケープして、`MyFile.cs;MyClass.cs` という名前の 1 つのアイテムを宣言しています。

```xml
<Compile Include="MyFile.cs%3BMyClass.cs"/>
```

また、[プロパティ関数](../msbuild/property-functions.md)を使用して文字列をエスケープすることもできます。 たとえば、これは上記の例と同じです。

```xml
<Compile Include="$([MSBuild]::Escape('MyFile.cs;MyClass.cs'))" />
```

### <a name="to-use-an-msbuild-special-character-as-a-literal-character"></a>MSBuild の特殊文字をリテラル文字として使用するには

特殊文字の代わりに `%<xx>` という表記を使用します。ここで、`<xx>` は ASCII 文字の 16 進値を表します。 たとえば、アスタリスク (`*`) をリテラル文字として使用するには、値 `%2A` を使用します。

## <a name="see-also"></a>関連項目
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [MSBuild](../msbuild/msbuild.md)
- [項目](../msbuild/msbuild-items.md)
