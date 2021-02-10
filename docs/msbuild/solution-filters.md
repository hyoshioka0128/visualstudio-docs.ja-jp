---
title: MSBuild でのソリューション フィルター
description: ソリューション フィルターについて説明し、MSBuild を使用してソリューション フィルター ファイルを作成する方法を示します。
ms.date: 07/28/2020
ms.topic: reference
helpviewer_keywords:
- MSBuild, solution filters
- solution filters [MSBuild]
author: ghogen
ms.author: ghogen
manager: jmartens
monikerRange: '>= vs-2019'
ms.openlocfilehash: 4a5c764ad9ea4190df5e533926671dbd88c53b8b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937837"
---
# <a name="solution-filters-in-msbuild"></a>MSBuild でのソリューション フィルター

ソリューション フィルター ファイルは、ソリューション内のすべてのプロジェクトからビルドまたは読み込みを行うプロジェクトを指定する、拡張子 *.slnf* の JSON ファイルです。 MSBuild 16.7 以降では、ソリューション フィルター ファイルで MSBuild を起動し、フィルター処理を有効にしてソリューションをビルドできます。 

> [!NOTE]
> ソリューション フィルター ファイルを使用すると、読み込みまたはビルドされるプロジェクトのセットが減り、形式が簡略化されます。 ソリューション ファイルは引き続き必要です。

## <a name="build-a-solution-filter-from-the-command-line"></a>コマンド ラインからソリューション フィルターを作成する

コマンド ラインからソリューション フィルター ファイルを作成する場合は、ソリューション ファイルを作成する場合とまったく同じ構文を使用します。 次のように、ソリューションではなくソリューション フィルター ファイルを指定し、フィルター処理を有効にしてビルドします。

```console
msbuild [options] solutionFilterFile.slnf
```

また、通常どおりスイッチやその他のプロパティを追加することもできます。 詳細については、「[MSBuild コマンド ライン リファレンス](msbuild-command-line-reference.md)」をご覧ください。 このコマンドによって、フィルター処理されたプロジェクトと、それが依存しているすべてのプロジェクトをビルドできます。 コマンド ラインからソリューション フィルターを作成する場合、MSBuild は自動的に依存関係に従います。 プロジェクトは、フィルターで指定されているか、ビルドされるプロジェクトによって参照されている場合、ビルドされます。

## <a name="solution-filter-files"></a>ソリューション フィルター ファイル

Visual Studio を使用してソリューション フィルター ファイルを操作することができます。 Visual Studio でソリューション フィルターを開くと、アンロードされたプロジェクトと読み込まれたプロジェクトが表示されます。さらに多くのプロジェクトを読み込んでビルド用に選択することもできます。 最初のプロジェクトが依存しているすべてのプロジェクトも読み込んでビルドできますが、必須ではありません。 [フィルター処理済みソリューション](../ide/filtered-solutions.md)に関する記事をご覧ください。

ソリューション フィルターは、ソリューションと同じフォルダーに配置する必要はありません。 ソリューション ファイルへのパスはソリューション フィルター ファイルの場所を基準にしますが、各プロジェクトへのパスはソリューション ファイル自体を基準にし、ソリューション ファイル内のプロジェクト パスと一致している必要があります。 相対パスの使用例を次に示します。

```json
{
  "solution": {
    "path": "..\\..\\Documents\\GitHub\\msbuild\\MSBuild.sln",
    "projects": [
      "src\\Build.OM.UnitTests\\Microsoft.Build.Engine.OM.UnitTests.csproj"
    ]
  }
}
```

パス内のバックスラッシュは、エスケープされるため 2 つ重ねる必要があります。

## <a name="example"></a>例

Visual Studio でのフィルター処理されたソリューションの例を次に示します。

![Visual Studio でのフィルター処理されたソリューションのスクリーンショット](media/solution-with-filter.png)

このソリューションでは、ClassLibrary1 が ProjectA と ProjectB の両方で使用されているため、ClassLibrary1 はプロジェクト参照として一覧表示されています。

Visual Studio によって生成されるソリューション フィルター ファイルを次に示します。

```json
{
  "solution": {
    "path": "MyApplication.sln",
    "projects": [
      "MyApplication\\MyApplication.csproj",
      "ProjectA\\ProjectA.csproj"
    ]
  }
}
```

この例では、フィルター処理を有効にして (コマンド `MSBuild [options] MyFilter.slnf` を使用して) ビルドすると、MSBuild によって MyApplication と ProjectA がビルドされます。ソリューション フィルター ファイルでそれらが明示的に記載されているためです。 MSBuild により、ProjectA のビルドの一環として ClassLibrary1 がビルドされます。ProjectA がこれに依存しているためです。  ProjectB はビルドされません。 (この説明はクリーン ビルドであることを前提としています。 プロジェクトが以前にビルドされていた場合は、既に最新の状態であるプロジェクトをスキップするために、通常の規則が適用されます。)

## <a name="see-also"></a>関連項目

- [フィルター処理済みソリューション](../ide/filtered-solutions.md)
- [MSBuild コマンド ライン リファレンス](msbuild-command-line-reference.md)
