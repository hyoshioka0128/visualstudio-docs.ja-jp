---
title: MSBuild の条件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, conditions
- conditions [MSBuild]
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbed62c13fc963af382ede113b138451303d9382
ms.sourcegitcommit: 273b657e115c1756adb84e0e56b6f2c709bcee76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80759715"
---
# <a name="msbuild-conditions"></a>MSBuild の条件

MSBuild では、`Condition` 属性が許可されている場所ならどこでも適用できる、特定の条件のセットがサポートされています。 次の表は、その条件を説明したものです。

|条件|説明|
|---------------|-----------------|
|'`stringA`' == '`stringB`'|`stringA` が `stringB` に等しい場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="'$(CONFIG)'=='DEBUG'"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|
|'`stringA`' != '`stringB`'|`stringA` が `stringB` と等しくない場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="'$(CONFIG)'!='DEBUG'"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|
|\<、>、\<=、>=|オペランドの数値を評価します。 関係の評価が true の場合、`true` を返します。 オペランドは、10 進数または 16 進数として評価される必要があります。 16 進数は、"0 x" で始まる必要があります。 **注:** XML では、文字 `<` および `>` をエスケープする必要があります。 シンボル `<` は、`&lt;` として表されます。 シンボル `>` は、`&gt;` として表されます。|
|Exists('`stringA`')|`stringA` という名前のファイルまたはフォルダーが存在する場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="!Exists('$(builtdir)')"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|
|HasTrailingSlash('`stringA`')|指定した文字列の末尾にバックスラッシュ (\\) 文字かスラッシュ (/) 文字のいずれかが含まれる場合、`true` と評価されます。<br /><br /> 次に例を示します。<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> 単純な英数字文字列またはブール値には、単一引用符は必要ありません。 ただし、空の値には単一引用符が必要です。|
|!|オペランドが `false` と評価される場合、`true` と評価されます。|
|And|両方のオペランドが `true` と評価される場合、`true` と評価します。|
|Or|少なくともオペランドの 1 つが `true` と評価される場合、`true` と評価します。|
|()|内部に含まれる式が `true` と評価される場合に `true` と評価されるグループ化機構。|
|$if$ ( %expression% )、$else$、$endif$|指定した `%expression%` が、渡されるカスタム テンプレート パラメーターの文字列の値と一致するかどうかをチェックします。 `$if$` 条件が `true` と評価される場合、そのステートメントが実行されます。それ以外の場合、`$else$` 条件がチェックされます。 `$else$` 条件が `true` の場合、そのステートメントが実行されます。それ以外の場合、`$endif$` 条件は式の評価を終了します。<br /><br /> 使用の例については、「[Visual Studio Project/Item Template Parameter Logic](https://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic)」(Visual Studio プロジェクト/項目テンプレート パラメーター ロジック) を参照してください。|

次の例に示すように、文字列メソッドを条件で使用できます。ここでは、文字列の関連部分のみを比較するために [TrimEnd()](/dotnet/api/system.string.trimend) 関数を使用し、.NET Framework と .NET Core のターゲット フレームワークを区別しています。

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFrameworks>net45;net48;netstandard2.1;netcoreapp2.1;netcoreapp3.1</TargetFrameworks>
    </PropertyGroup>

    <PropertyGroup Condition="'$(TargetFramework.TrimEnd('0123456789.'))' == 'net'">
        <!-- Properties for .NET Framework -->
    </PropertyGroup>

</Project>
```

## <a name="see-also"></a>関連項目

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [条件構造](../msbuild/msbuild-conditional-constructs.md)
- [チュートリアル: MSBuild プロジェクト ファイルのゼロからの作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)
