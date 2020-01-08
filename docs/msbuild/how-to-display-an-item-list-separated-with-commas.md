---
title: '方法: 項目リストをコンマ区切りで表示する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, separating items with semicolons
- MSBuild, formatting item collections
ms.assetid: 3cae844c-7c6d-4144-82dc-efad10ba458f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 677278d08e3223f759afc64692481311bfba3356
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596334"
---
# <a name="how-to-display-an-item-list-separated-with-commas"></a>方法: 項目リストをコンマ区切りで表示する
[!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] ([!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]) で項目一覧を使用するとき、項目一覧の内容を読みやすいように表示すると便利な場合があります。 あるいは、項目の一覧を特殊な区切り文字列で区切るタスクが与えられることがあります。 いずれの場合でも、項目一覧には区切り文字列を指定できます。

## <a name="separate-items-in-a-list-with-commas"></a>一覧内の項目をコンマで区切る
既定では、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] はセミコロンを利用して一覧内の項目を区切ります。 たとえば、次の値を持つ `Message` 要素があります。

`<Message Text="This is my list of TXT files: @(TXTFile)"/>`

`@(TXTFile)` 項目一覧に項目 *App1.txt*、*App2.txt*、*App3.txt* が含まれるとき、メッセージは次のようになります。

`This is my list of TXT files: App1.txt;App2.txt;App3.txt`

既定の動作を変更する場合、独自の区切りを指定できます。 項目一覧区切りを指定するための構文は次のようになります。

`@(ItemListName, '<separator>')`

区切りは単一の文字か文字列にすることができます。一重引用符で囲む必要があります。

#### <a name="to-insert-a-comma-and-a-space-between-items"></a>項目の間にコンマとスペースを挿入するには

- 次のような項目表記を使用します。

    `@(TXTFile, ', ')`

## <a name="example"></a>例
この例では、[Exec](../msbuild/exec-task.md) タスクは findstr ツールを実行し、ファイル *Phrases.txt* から指定のテキスト文字列を探します。 findstr コマンドでは、リテラル検索文字列が **-c:** スイッチによって示されます。そのため、項目区切り `-c:` が `@(Phrase)` 項目一覧の項目間に挿入されます。

この例では、次がこれに相当するコマンドライン コマンドです。

`findstr /i /c:hello /c:world /c:msbuild phrases.txt`

```xml
<Project DefaultTargets = "Find"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <ItemGroup>
        <Phrase Include="hello"/>
        <Phrase Include="world"/>
        <Phrase Include="msbuild"/>
    </ItemGroup>

    <Target Name = "Find">
        <!-- Find some strings in a file -->
        <Exec Command="findstr /i /c:@(Phrase, ' /c:') phrases.txt"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [項目](../msbuild/msbuild-items.md)
