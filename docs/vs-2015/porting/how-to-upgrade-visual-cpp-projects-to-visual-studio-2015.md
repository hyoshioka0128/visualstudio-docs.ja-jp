---
title: '方法: Visual C++ プロジェクトを Visual Studio 2015 にアップグレードする | Microsoft Docs'
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- projects [C++], upgrading
ms.assetid: 9a283ebb-f6d8-49c0-a73e-323979ff56a2
caps.latest.revision: 26
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: 60ba1ad7f1ed467cb1a396f80228b8915bd62a31
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918799"
---
# <a name="how-to-upgrade-visual-c-projects-to-visual-studio-2015"></a>方法: Visual C++ プロジェクトを Visual Studio 2015 にアップグレードする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2017 の最新ドキュメントについては、「[Visual C++ 移植とアップグレードのガイド](/cpp/porting/visual-cpp-porting-and-upgrading-guide)」をご覧ください。

旧バージョンの Visual Studio で作成された Visual C++ プロジェクトを初めて開くと、そのプロジェクトを更新するよう求めるメッセージが表示されることがあります。 Visual C++ コンパイラおよびライブラリを最新バージョンにアップグレードするかどうかを確認するメッセージです。 アップグレードのオプションは、プロジェクトの作成に使用された [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のバージョンによって異なります。

 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] を使用して、 [!INCLUDE[win8](../includes/win8-md.md)] で作成された [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]プロジェクトを開き、編集し、ビルドすることができますが、新しい [!INCLUDE[win8](../includes/win8-md.md)] プロジェクトを作成するには [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]を使用する必要があります ( [!INCLUDE[win81](../includes/win81-md.md)] プロジェクトを作成するには、 [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)]を使用する必要があります。)。

 Windows 10 プロジェクトを作成するには、 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]を使用する必要があります。

 プロジェクトを更新するように求めるメッセージが表示されない場合は、プロジェクトのアップグレードのために何もする必要がない可能性があります。

- プロジェクト (.vcproj) が [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] よりも前のバージョンの [!INCLUDE[vs2010](../includes/vs2010-md.md)]で作成されていた場合は、プロジェクトを更新する必要があります。

- プロジェクト (.vcxproj) が [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]、  [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]、または [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] で作成されている場合、次の 2 つのオプションがあります。

  - 更新をスキップできます。 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] が [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] SP1、[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]、または [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] の Visual C++ ツールにアクセスできる場合、プロジェクトは変更を加えずに読み込まれます。 そのアクセスを可能にするには、プロジェクトの作成に使用したバージョンの Visual Studio を、 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]と同じマシンにインストールします。 詳細については、「 [Installing Visual Studio Versions Side-by-Side](../install/install-visual-studio-versions-side-by-side.md)」を参照してください。

  - [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が後で説明するような変更を加えられるようにすることで、プロジェクトを更新できます。 ソリューションに複数の Visual C++ プロジェクトが含まれる場合は、すべてのプロジェクトを更新する必要があります。

    > [!NOTE]
    > 最初に更新を求められたときに更新しない場合は、後で **[プロジェクト]** メニューの **[VC++ プロジェクトの更新]** を選択してプロジェクトを更新できます。 このコマンドが表示されない場合、更新は必要ではありません。

## <a name="upgrading-a-visual-c-project"></a>Visual C++ プロジェクトのアップグレード
 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] が自動的にプロジェクトを更新できるようにすると、次の変更が加えられます。

- [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)] のコンパイラおよびライブラリを使用するように、プロジェクトを変更します (PlatformToolset = VisualStudio v140)。

- [!INCLUDE[cppcli](../includes/cppcli-md.md)] プロジェクトの場合は、TargetFrameworkVersion を .NET Framework 4.5.2 に変更します。

## <a name="continuing-to-work-with-a-custom-platformtoolset"></a>カスタム PlatformToolset の使用の継続
 [!INCLUDE[vs_dev14](../includes/vs-dev14-md.md)]でカスタム PlatformToolset を引き続き使用する場合、ツールセットは、x86 コンピューターでは %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\Platforms\Win32\PlatformToolsets\ の下、x64 コンピューターでは %ProgramFiles (x86)%\MSBuild\Microsoft.Cpp\v4.0\Platforms\Win32\PlatformToolsets\ の下に格納されている必要があります。 カスタム PlatformToolset を作成する方法については、Visual C++ チーム ブログの「 [C++ ネイティブ マルチ ターゲット](https://blogs.msdn.com/b/vcblog/archive/2009/12/08/c-native-multi-targeting.aspx) 」を参照してください。

## <a name="see-also"></a>関連項目
 Visual [Studio プロジェクトの移植、移行、およびアップグレードに](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)関する[ビジュアルC++な移植とアップグレードのガイド](https://msdn.microsoft.com/library/f5fbcc3d-aa72-41a6-ad9a-a706af2166fb)
