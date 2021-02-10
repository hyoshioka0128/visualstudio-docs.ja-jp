---
title: SharePoint でサポートされている MSBuild のプロパティ |Microsoft Docs
description: およびでサポートされており、SharePoint に固有の MSBuild プロパティの名前と説明の一覧を読み取ります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 20458cc7047e913e13f4594380d4b4946b44ec17
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938513"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint でサポートされている MsBuild プロパティ
  [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]VisualStudio ファイル、プロジェクトファイル、またはプロジェクトユーザーファイルで定義されているすべてのプロパティは、sharepoint プロジェクトで使用でき [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 Sharepoint では、 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] プロジェクトによって提供される共通プロパティに加えて、sharepoint プロジェクトに固有の追加のプロパティが定義されています。

 共通プロパティの一覧につい [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] ては、「 [MSBuild プロジェクトの共通プロパティ](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))」を参照してください。 プログラミング言語でサポートされているプロパティの完全な一覧については、 *.targets* ファイル、プロジェクトファイル (*.csproj* または *.vbproj*)、またはプロジェクトユーザーファイル (*.csproj* または *.vbproj*) を参照してください。

## <a name="msbuild-properties-specific-to-sharepoint"></a>SharePoint に固有の MsBuild プロパティ
 次の表に、 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] の SharePoint プロジェクトに特に適用されるプロパティを示し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 その他のプロパティは存在しますが、内部で使用するためのものです。

|プロパティ名|説明|
|-------------------|-----------------|
|SharePointSiteUrl|SharePoint サイトへのを表す文字列 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 。|
|SandboxedSolution|ソリューションがサンドボックスソリューションであるかどうかを示すブール値。|
|ActiveDeploymentConfiguration|アクティブな配置構成。|
|IncludeAssemblyInPackage|アセンブリがパッケージファイルに含まれるかどうかを示すブール値です。|
|PreDeploymentCommand|配置前コマンドのステップで実行するコマンドを表す文字列値。|
|PostDeploymentCommand|配置後コマンドのステップで実行するコマンドを表す文字列値。|
|CustomBeforeSharePointTargets|ターゲットファイルのパスを表す文字列 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 。 ターゲットファイルが存在し、定義されている場合は、SharePoint ターゲットデータの前にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲットファイルを変更せずにパッケージ関連のプロパティを事前することで、パッケージプロセスをカスタマイズできます。ただし、ターゲットファイルは、すべての SharePoint プロジェクトに適用されます。|
|CustomAfterSharePointTargets|ターゲットファイルのパスを表す文字列 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 。 ターゲットファイルが存在し、定義されている場合は、すべての SharePoint ターゲットデータの後にインポートされます。 このプロパティを使用すると、配布された SharePoint ターゲットファイルを変更することなくパッケージ関連のプロパティとターゲットをオーバーライドすることにより、パッケージプロセスをカスタマイズできます。ただし、ターゲットファイルは、すべての SharePoint プロジェクトに適用されます。|
|LayoutPath|パッケージ化される各ファイルが *.wsp* ファイルに追加される前に一時的に配置されるルートディレクトリを表す文字列。 このパスは、BeforeLayout および AfterLayout ターゲットをオーバーライドしてパッケージ化するファイルを追加、削除、または変更するタイミングを把握するのに役立ちます。これは、 *.wsp* ファイルの内容を変更するために使用できるためです。|
|BasePackagePath|パッケージが配置されているフォルダーを表す文字列。 この値は、プロジェクトの出力ディレクトリ (Bin\debug など) を使用します。|
|PackageExtension|パッケージに追加するファイル名拡張子を表す文字列です。 既定値は wsp です。|
|AssemblyDeploymentTarget|プロジェクトアセンブリが SharePoint サーバー上に配置される場所を表す文字列。 この値は、GlobalAssemblyCache (既定値) または WebApplication です。 このプロパティは、プロパティウィンドウで設定することもできます。|
|PackageWithValidation|パッケージ化の前に検証を実行するかどうかを指定するブール値です。 このプロパティを使用すると、パッケージのビルド中に検証エラーを無視できます。|
|ValidatePackageDependsOn|ValidatePackage ターゲットの前に実行する追加のターゲットを定義する文字列。|
|TokenReplacementFileExensions|パッケージ化中にトークンが置き換えられるファイルを定義する文字列。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>[プロパティ] ページで MsBuild のプロパティを使用する
 柔軟性を高めるために、[SharePoint のプロパティ] ページの [ **展開前のコマンドライン** ] ボックスと [ **配置後** のコマンド] ボックスでハードコーディングされた文字列を使用する代わりに、sharepoint プロパティを引数として使用できます。 たとえば、SharePoint サイトに特定の文字列を指定する代わりに、 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 代わりにを使用でき `$(SharePointSiteUrl)` ます。

> [!NOTE]
> [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]変数構文 `$(` *propertyname* `)` または環境変数構文 `%` *propertyname* を使用して、 `%` プロパティを指定できます。

## <a name="see-also"></a>関連項目

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)