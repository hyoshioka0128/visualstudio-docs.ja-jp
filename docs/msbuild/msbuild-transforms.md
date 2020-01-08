---
title: MSBuild 変換 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bcfc3c-14fa-455e-805c-63ccffa4a3bf
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c4262ed1a7b92170565f7006c9ed06ed884f928
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593773"
---
# <a name="msbuild-transforms"></a>MSBuild 変換
変換とは、1 つの項目一覧を別の項目コレクションに一対一で変換することです。 プロジェクトで項目一覧を変換できます。さらに変換により、ターゲットは入出力間の直接割り当てを指定できるようになります。 このトピックでは、変換と、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] で変換を利用してプロジェクトを効率的にビルドする方法について説明します。

## <a name="transform-modifiers"></a>変換修飾子
変換は任意ではなく、特別な構文により制限されています。変換修飾子はすべて %(\<ItemMetaDataName>) という形式にする必要があります。 あらゆる項目メタデータを変換修飾子として使用できます。 これには、作成時にすべての項目に割り当てられる既知の項目メタデータが含まれます。 既知の項目メタデータの一覧については、「[既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」をご覧ください。

次の例では、 *.resx* ファイルの一覧が *.resources* ファイルの一覧に変換されます。 %(filename) 変換修飾子は、各 *.resources* ファイルに対応する *.resx* ファイルと同じファイル名が与えられることを指定します。

```xml
@(RESXFile->'%(filename).resources')
```

たとえば、@(RESXFile) 項目リスト内の項目が *Form1.resx*、*Form2.resx*、*Form3.resx* である場合、変換後の一覧の出力は *Form1.resources*、 *Form2.resources*、*Form3.resources* になります。

> [!NOTE]
> 標準の項目一覧に区切りを指定するのと同じ方法で、変換後の項目一覧にカスタムの区切りを指定できます。 たとえば、変換後の項目一覧を既定のセミコロン (;) ではなくコンマ (,) で区切るには、次の XML を使用します: `@(RESXFile->'Toolset\%(filename)%(extension)', ',')`

## <a name="use-multiple-modifiers"></a>複数の修飾子を使用する
 変換式には、複数の修飾子を含めることができます。複数の修飾子は任意の順序で結合したり、繰り返したりできます。 次の例では、ファイルを含むディレクトリの名前が変更されますが、ファイルは元の名前とファイル名拡張子を維持します。

```xml
@(RESXFile->'Toolset\%(filename)%(extension)')
```

 たとえば、`RESXFile` 項目一覧に含まれる項目が *Project1\Form1.resx*、*Project1\Form2.resx*、*Project1\Form3.text* である場合、変換後の一覧の出力は *Toolset\Form1.resx*、*Toolset\Form2.resx*、*Toolset\Form3.text* になります。

## <a name="dependency-analysis"></a>依存関係の分析
 変換では、変換後の項目一覧と元の項目一覧の間に存在する一対一のマッピングか維持されます。 そのため、入力の変換である出力がターゲットによって作成される場合、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は、入力と出力のタイムスタンプを分析し、ターゲットをスキップ、ビルド、部分的再ビルドするかどうかを決定します。

 次の例の [[タスクをコピー]](../msbuild/copy-task.md) では、`BuiltAssemblies` 項目一覧のすべてのファイルが、`Outputs` 属性の変換によって指定される、タスクのターゲット フォルダーにマッピングされます。 `BuiltAssemblies` 項目一覧のファイルが変更されると、`Copy` タスクは変更されたファイルにだけ実行され、他のファイルはすべてスキップされます。 依存関係分析と変換の使用方法に関する詳細については、「[方法:インクリメンタル ビルド](../msbuild/how-to-build-incrementally.md)」を参照してください。

```xml
<Target Name="CopyOutputs"
    Inputs="@(BuiltAssemblies)"
    Outputs="@(BuiltAssemblies -> '$(OutputPath)%(Filename)%(Extension)')">

    <Copy
        SourceFiles="@(BuiltAssemblies)"
        DestinationFolder="$(OutputPath)"/>

</Target>
```

## <a name="example"></a>例

### <a name="description"></a>説明
 次の例では、変換を使用する [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクト ファイルが確認できます。 この例では、*c:\sub0\sub1\sub2\sub3* ディレクトリに *.xsd* ファイルが 1 つだけ存在し、作業ディレクトリが *c:\sub0* であると想定されています。

### <a name="code"></a>コード

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Schema Include="sub1\**\*.xsd"/>
    </ItemGroup>

    <Target Name="Messages">
        <Message Text="rootdir: @(Schema->'%(rootdir)')"/>
        <Message Text="fullpath: @(Schema->'%(fullpath)')"/>
        <Message Text="rootdir + directory + filename + extension: @(Schema->'%(rootdir)%(directory)%(filename)%(extension)')"/>
        <Message Text="identity: @(Schema->'%(identity)')"/>
        <Message Text="filename: @(Schema->'%(filename)')"/>
        <Message Text="directory: @(Schema->'%(directory)')"/>
        <Message Text="relativedir: @(Schema->'%(relativedir)')"/>
        <Message Text="extension: @(Schema->'%(extension)')"/>
    </Target>
</Project>
```

### <a name="comments"></a>コメント
 この例を実行すると、次の出力が生成されます。

```
rootdir: C:\
fullpath: C:\sub0\sub1\sub2\sub3\myfile.xsd
rootdir + directory + filename + extension: C:\sub0\sub1\sub2\sub3\myfile.xsd
identity: sub1\sub2\sub3\myfile.xsd
filename: myfile
directory: sub0\sub1\sub2\sub3\
relativedir: sub1\sub2\sub3\
extension: .xsd
```

## <a name="see-also"></a>関連項目
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [方法: インクリメンタル ビルド](../msbuild/how-to-build-incrementally.md)
