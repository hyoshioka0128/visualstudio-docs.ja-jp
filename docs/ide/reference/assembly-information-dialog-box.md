---
title: '[アセンブリ情報] ダイアログ ボックス'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAssemblyInfo
helpviewer_keywords:
- Assembly Information dialog box
ms.assetid: 8f1f6449-e03d-4a5b-9076-d3b1f84ada48
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae70a2bf989b73dedc5becaac6f4b49bd0108730
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595788"
---
# <a name="assembly-information-dialog-box"></a>[アセンブリ情報] ダイアログ ボックス

[アセンブリ情報] ダイアログ ボックスは、.NET Framework グローバル アセンブリ属性の値を指定するために使用します。この値は、プロジェクトで自動的に作成される AssemblyInfo ファイルに格納されます。 ソリューション エクスプローラーでの AssemblyInfo ファイルは、Visual Basic プロジェクトの場合は **[マイ プロジェクト]** ノードにあります (表示するには **[すべてのファイルを表示]** をクリックします)。 C# プロジェクトの場合は、 **[プロパティ]** にあります。 詳しくは、「[属性 (C#)](/dotnet/csharp/programming-guide/concepts/attributes/index)」をご覧ください。

このダイアログ ボックスにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** を選択します。 **[アプリケーション]** ページで、 **[アセンブリ情報]** ボタンを選択します。

## <a name="uielement-list"></a>UIElement の一覧

**タイトル**\
アセンブリ マニフェストのタイトルを指定します。 <xref:System.Reflection.AssemblyTitleAttribute> に相当します。

**説明**\
アセンブリ マニフェストの説明を指定します (省略可能)。 <xref:System.Reflection.AssemblyDescriptionAttribute> に相当します。

**会社名**\
アセンブリ マニフェストの会社名を指定します。 <xref:System.Reflection.AssemblyCompanyAttribute> に相当します。

レジストリで Company の既定値を設定または変更できます。 Windows のバージョンに応じて、**Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion** または **Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion** キーで **RegisteredOrganization** の値を探します。

**製品**\
アセンブリ マニフェストの製品名を指定します。 <xref:System.Reflection.AssemblyProductAttribute> に相当します。

**著作権**\
アセンブリ マニフェストの著作権情報を指定します。 <xref:System.Reflection.AssemblyCopyrightAttribute> に相当します。

**商標**\
アセンブリ マニフェストの商標を指定します。 <xref:System.Reflection.AssemblyTrademarkAttribute> に相当します。

**アセンブリ バージョン**\
アセンブリのバージョンを指定します。 <xref:System.Reflection.AssemblyVersionAttribute> に相当します。

**ファイル バージョン**\
Win32 ファイル バージョン リソースの特定のバージョン番号を使用するようコンパイラに指示します。 <xref:System.Reflection.AssemblyFileVersionAttribute> に相当します。

**GUID**\
アセンブリを示す一意の GUID。 プロジェクトを作成すると、Visual Studio でアセンブリの GUID が生成されます。 <xref:System.Guid> に相当します。

**ニュートラル言語**\
アセンブリがサポートするカルチャを指定します。 <xref:System.Resources.NeutralResourcesLanguageAttribute> に相当します。 既定値は **[(なし)]** です。

**アセンブリを COM 参照可能にする**\
アセンブリの型を COM に使用できるようにするかどうかを指定します。 <xref:System.Runtime.InteropServices.ComVisibleAttribute> に相当します。

> [!NOTE]
> .NET Framework クラス ライブラリで NuGet パッケージを生成するときにこれらのプロパティを設定する方法の詳細については、「[パッケージのプロジェクト プロパティを構成する](/nuget/quickstart/create-and-publish-a-package-using-visual-studio-net-framework#configure-project-properties-for-the-package)」を参照してください。

## <a name="see-also"></a>関連項目

- [[アプリケーション] ページ (プロジェクト デザイナー)](../../ide/reference/application-page-project-designer-visual-basic.md)
- [属性](https://msdn.microsoft.com/Library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)
