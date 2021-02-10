---
title: '方法: ビルドで環境変数を使用する | Microsoft Docs'
description: MSBuild プロジェクト ファイルの環境変数にアクセスし、環境変数を使用してプロジェクト ファイルを変更せずにビルド オプションを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- environment variables, referencing
- projects [.NET Framework], environment variables
- MSBuild, environment variables
ms.assetid: 7f9e4469-8865-4b59-aab3-3ff26bd36e77
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c7c81f36d37d071593a013067f661451b8916caa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914194"
---
# <a name="how-to-use-environment-variables-in-a-build"></a>方法: ビルドで環境変数を使用する

プロジェクトをビルドするとき、プロジェクト ファイルまたはプロジェクトを構成するファイルに含まれていない情報を使用してビルド オプションを設定する必要がある場合があります。 通常、この情報は環境変数に格納されます。

## <a name="reference-environment-variables"></a>環境変数を参照する

 すべての環境変数は、Microsoft Build Engine (MSBuild) プロジェクト ファイルでプロパティとして使用可能です。

> [!NOTE]
> プロジェクト ファイルに、環境変数と同じ名前のプロパティが明示的に定義されている場合、環境変数の値はプロジェクト ファイル内のプロパティによってオーバーライドされます。

#### <a name="to-use-an-environment-variable-in-an-msbuild-project"></a>MSBuild プロジェクトで環境変数を使用するには

- プロジェクト ファイルで宣言された変数と同様に、環境変数を参照します。 たとえば、次のコードは、BIN_PATH 環境変数を参照します。

   `<FinalOutput>$(BIN_PATH)\MyAssembly.dll</FinalOutput>`

  環境変数が設定されていない場合は、`Condition` 属性を使用して、プロパティの既定値を指定することができます。

#### <a name="to-provide-a-default-value-for-a-property"></a>プロパティの既定値を指定するには

- プロパティに値がない場合に限り、`Condition` 属性をプロパティで使用して値を設定します。 たとえば、`ToolsPath` 環境変数が設定されていない場合に限り、次のコードによって `ToolsPath` プロパティが *c:\tools* に設定されます。

     `<ToolsPath Condition="'$(TOOLSPATH)' == ''">c:\tools</ToolsPath>`

    > [!NOTE]
    > プロパティ名は大文字と小文字が区別されないため、`$(ToolsPath)` と `$(TOOLSPATH)` の両方が同じプロパティまたは環境変数を参照します。

## <a name="example"></a>例

 次のプロジェクト ファイルは、環境変数を使用して、ディレクトリの場所を指定します。

```xml
<Project DefaultTargets="FakeBuild">
    <PropertyGroup>
        <FinalOutput>$(BIN_PATH)\myassembly.dll</FinalOutput>
        <ToolsPath Condition=" '$(ToolsPath)' == '' ">
            C:\Tools
        </ToolsPath>
    </PropertyGroup>
    <Target Name="FakeBuild">
        <Message Text="Building $(FinalOutput) using the tools at $(ToolsPath)..."/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)
- [MSBuild プロパティ](../msbuild/msbuild-properties.md)
- [方法: 同じソース ファイルを異なるオプションでビルドする](../msbuild/how-to-build-the-same-source-files-with-different-options.md)
