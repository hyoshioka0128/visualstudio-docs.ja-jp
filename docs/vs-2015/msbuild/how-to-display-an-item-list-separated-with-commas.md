---
title: '方法: 項目リストをコンマ区切りで表示する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, separating items with semicolons
- MSBuild, formatting item collections
ms.assetid: 3cae844c-7c6d-4144-82dc-efad10ba458f
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 93451d6d49082621df48c734de951e6a4bc7e281
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156630"
---
# <a name="how-to-display-an-item-list-separated-with-commas"></a>方法: 項目リストをコンマ区切りで表示する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] ([!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]) で項目一覧を使用するとき、項目一覧の内容を読みやすいように表示すると便利な場合があります。 あるいは、項目の一覧を特殊な区切り文字列で区切るタスクが与えられることがあります。 いずれの場合でも、項目一覧には区切り文字列を指定できます。  
  
## <a name="separating-items-in-a-list-with-commas"></a>一覧内の項目をコンマで区切る  
 既定では、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はセミコロンを利用して一覧内の項目を区切ります。 たとえば、次の値を持つ `Message` 要素があります。  
  
 `<Message Text="This is my list of TXT files: @(TXTFile)"/>`  
  
 `@(TXTFile)` 項目一覧に項目 App1.txt、App2.txt、App3.txt が含まれるとき、メッセージは次のようになります。  
  
 `This is my list of TXT files: App1.txt;App2.txt;App3.txt`  
  
 既定の動作を変更する場合、独自の区切りを指定できます。 項目一覧区切りを指定するための構文は次のようになります。  
  
 `@(ItemListName, '<separator>')`  
  
 区切りは単一の文字か文字列にすることができます。一重引用符で囲む必要があります。  
  
#### <a name="to-insert-a-comma-and-a-space-between-items"></a>項目の間にコンマとスペースを挿入するには  
  
- 次のような項目表記を使用します。  
  
     `@(TXTFile, ', ')`  
  
## <a name="example"></a>例  
 この例では、[Exec](../msbuild/exec-task.md) タスクは findstr ツールを実行し、ファイル Phrases.txt から指定のテキスト文字列を探します。 findstr コマンドでは、リテラル検索文字列が **/c:** スイッチによって示されます。そのため、項目区切り `/c:` が `@(Phrase)` 項目一覧の項目間に挿入されます。  
  
 この例では、次がこれに相当するコマンドライン コマンドです。  
  
 `findstr /i /c:hello /c:world /c:msbuild phrases.txt`  
  
```  
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
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [項目](../msbuild/msbuild-items.md)
