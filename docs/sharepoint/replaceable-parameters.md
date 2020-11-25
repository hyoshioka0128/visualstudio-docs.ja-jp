---
title: 置き換え可能パラメーター |Microsoft Docs
description: 置換可能なパラメーター (トークン) を確認します。これは、デザイン時に実際の値がわからない SharePoint ソリューションアイテムのプロジェクトファイル内の値を指定します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, tokens
- tokens [SharePoint development in Visual Studio]
- replaceable parameters [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, replaceable parameters
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload: office
ms.openlocfilehash: 1cd44b3edfaeae376e5a4a9698d138bd75c03bf8
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95970261"
---
# <a name="replaceable-parameters"></a>置き換え可能パラメーター
  置換可能なパラメーター ( *トークン*) をプロジェクトファイル内で使用すると、デザイン時に実際の値がわからない SharePoint ソリューション項目の値を指定できます。 これらの関数は、標準テンプレートトークンに似てい [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 詳細については、「 [テンプレートパラメーター](../ide/template-parameters.md)」を参照してください。

## <a name="token-format"></a>トークンの形式
 トークンの先頭と末尾にはドル記号 ($) が付きます。 配置時には、プロジェクトが SharePoint ソリューションパッケージ (*.wsp* ファイル) にパッケージ化されるときに使用されるすべてのトークンが実際の値に置き換えられます。 たとえば、トークン **$SharePoint Package.Name $** は、文字列 "Test SharePoint Package" に解決される場合があります。

## <a name="token-rules"></a>トークンの規則
 トークンには、次の規則が適用されます。

- トークンは、行内の任意の場所で指定できます。

- トークンは複数の行にまたがることはできません。

- 同じ行と同じファイルに、同じトークンが複数回指定されている可能性があります。

- 同じ行に異なるトークンを指定することもできます。

  これらの規則に従わないトークンは無視され、警告やエラーは発生しません。

  文字列値によるトークンの置換は、マニフェスト変換の直後に行われます。 この置換により、ユーザーはトークンを使用してマニフェストテンプレートを編集できます。

### <a name="token-name-resolution"></a>トークン名の解決
 ほとんどの場合、トークンは、含まれている場所に関係なく、特定の値に解決されます。 ただし、トークンがパッケージまたは機能に関連付けられている場合、トークンの値は、そのトークンが含まれている場所によって異なります。 たとえば、機能がパッケージ A に含まれている場合、トークンは `$SharePoint.Package.Name$` "Package a" という値に解決されます。 同じ機能がパッケージ B にある場合、は `$SharePoint.Package.Name$` "パッケージ b" に解決されます。

## <a name="tokens-list"></a>トークンの一覧
 次の表に、使用可能なトークンを示します。

|名前|説明|
|----------|-----------------|
|$SharePoint. Project. FileName $|格納しているプロジェクトファイルの *名前 (など)。*|
|$SharePoint FileNameWithoutExtension $|ファイル名拡張子を含まない、含んでいるプロジェクトファイルの名前。 たとえば、"NewProj" のようになります。|
|$SharePoint. プロジェクト. AssemblyFullName $|格納しているプロジェクトの出力アセンブリの表示名 (厳密な名前)。|
|$SharePoint. Project. AssemblyFileName $|格納しているプロジェクトの出力アセンブリの名前。|
|$SharePoint AssemblyFileNameWithoutExtension $|ファイル名の拡張子を含まない、プロジェクトの出力アセンブリの名前。|
|$SharePoint AssemblyPublicKeyToken $|格納しているプロジェクトの出力アセンブリの公開キートークンを文字列に変換したもの。 ("x2" 16 進数形式では16文字)。|
|$SharePoint. Package.Name $|格納しているパッケージの名前。|
|$SharePoint. FileName $|格納しているパッケージの定義ファイルの名前。|
|$SharePoint. FileNameWithoutExtension $|格納しているパッケージの定義ファイルの名前 (拡張子なし)。|
|$SharePoint. Package.Id $|格納しているパッケージの SharePoint ID。 複数のパッケージで機能が使用されている場合は、この値が変更されます。|
|$SharePoint. FileName $|*Feature1.feature* など、含まれている機能の定義ファイルの名前。|
|$SharePoint. FileNameWithoutExtension $|ファイル名拡張子のないフィーチャー定義ファイルの名前。|
|$SharePoint。 DeploymentPath $|パッケージ内の機能を含むフォルダーの名前。 このトークンは、機能デザイナーの "配置パス" プロパティに相当します。 値の例は、"Project1_Feature1" です。|
|$SharePoint. Feature.Id $|格納している機能の SharePoint ID。 このトークンは、すべての機能レベルのトークンと同様に、機能を介してパッケージに含まれるファイルによってのみ使用できます。機能の外部のパッケージに直接追加されるわけではありません。|
|$SharePoint. ProjectItem.Name $|**ISharePointProjectItem.Name** から取得したプロジェクト項目の名前 (ファイル名ではありません)。|
|$SharePoint. \<GUID> ..AssemblyQualifiedName $|トークンのと一致する型のアセンブリ修飾名 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 。 の形式は [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 小文字で、Guid. ToString ("D") 形式 (つまり、xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) に対応しています。|
|$SharePoint. \<GUID> ..FullName $|トークン内の GUID と一致する型の完全名。 GUID の形式は小文字で、Guid. ToString ("D") 形式 (つまり、xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) に対応しています。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>トークン置換ファイル拡張子の一覧に拡張機能を追加する
 トークンは、パッケージに含まれる SharePoint プロジェクト項目に属する任意のファイルで理論的に使用できますが、既定では、は、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] パッケージファイル、マニフェストファイル、および次の拡張子を持つファイルのみでトークンを検索します。

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- ASPX

- パーツ

- REPORTVIEWER.DWP

  これらの拡張機能は、VisualStudio ファイル内の要素によって定義されます。このファイルは、 `<TokenReplacementFileExtensions>` \\ program files \> \MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools フォルダー<にあります。

  ただし、一覧にファイル拡張子を追加することはできます。 Sharepoint `<TokenReplacementFileExtensions>` ターゲットファイルのの前に定義されている sharepoint プロジェクトファイル内の任意の PropertyGroup に要素を追加 \<Import> します。

> [!NOTE]
> トークンの置換はプロジェクトのコンパイル後に発生するため、 *.cs*、 *.vb* 、 *.resx* など、コンパイルされたファイルの種類のファイル拡張子を追加しないでください。 トークンは、コンパイルされていないファイルでのみ置き換えられます。

 たとえば、ファイル名拡張子 (*myextension* と *yourextension*) をトークン置換ファイル名拡張子の一覧に追加するには、プロジェクト (*.csproj*) ファイルに次のコードを追加します。

```xml
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
.
.
.
    <!-- Define the following property to add your extension to the list of token replacement file extensions.  -->
<TokenReplacementFileExtensions>myextension;yourextension</TokenReplacementFileExtensions>
</PropertyGroup>
```

 拡張機能は、ターゲット (*.targets*) ファイルに直接追加できます。 ただし、拡張機能を追加すると、独自のものではなく、ローカルシステムにパッケージ化されているすべての SharePoint プロジェクトの拡張機能の一覧が変更されます。 この拡張機能は、システムの開発者の場合や、ほとんどのプロジェクトで必要とされる場合に便利です。 ただし、システム固有であるため、この方法は移植できないため、代わりにプロジェクトファイルに拡張機能を追加することをお勧めします。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
