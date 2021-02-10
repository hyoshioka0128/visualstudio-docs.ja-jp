---
title: プロジェクトの種類を登録する |Microsoft Docs
description: 新しいプロジェクトの種類を Visual Studio が認識して使用できるようにするレジストリエントリの作成について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 893f59aa9e99d990623e0c8383c12bbffbc4a510
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944512"
---
# <a name="registering-a-project-type"></a>プロジェクト タイプの登録
新しいプロジェクトの種類を作成する場合は、がプロジェクトの種類を認識して使用できるようにするレジストリエントリを作成する必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 通常、これらのレジストリエントリを作成するには、レジストリスクリプト (.rgs) ファイルを使用します。

 次の例では、レジストリのステートメントによって、既定のパスとデータが適用されます。その後、各ステートメントのレジストリスクリプトのエントリを含むテーブルが指定されます。 これらのテーブルには、ステートメントに関するスクリプトエントリと追加情報が記載されています。

> [!NOTE]
> 次のレジストリ情報は、プロジェクトの種類を登録するために記述するレジストリスクリプトのエントリの種類と目的の例として使用することを目的としています。 実際のエントリとその使用は、プロジェクトの種類の特定の要件によって異なる場合があります。 開発しているプロジェクトの種類によく似たサンプルを見つけて、そのサンプルのレジストリスクリプトを確認するには、使用可能なサンプルを確認する必要があります。

 次の例は、HKEY_CLASSES_ROOT からのものです。

## <a name="example-1"></a>例 1

```
\.figp
   @="FigPrjFile"
   "Content Type"="text/plain"
\.figp\ShellNew
   "NullFile"=""
\FigPrjFile
   @="Figure Project File"
\DefaultIcon
   @="<Visual Studio SDK installation path>\\9.0VSIntegration\\SomeFolder\\FigPkgs\\FigPrj\\Debug\\FigPrj.dll,-206"
\shell\open
   @="&Open in Visual Studio"
\shell\open\command
   @="devenv.exe \"%1\""
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|拡張子が figp であるプロジェクトの種類のファイルの名前と説明。|
|`Content Type`|REG_SZ|`Text/plain`|プロジェクトファイルのコンテンツの種類。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|この種類のプロジェクトに使用される既定のアイコン。 % MODULE% ステートメントは、プロジェクトの種類の DLL の既定の場所にレジストリで完了します。|
|`@`|REG_SZ|`&Open in Visual Studio`|このプロジェクトの種類を開く既定のアプリケーション。|
|`@`|REG_SZ|`devenv.exe "%1"`|この種類のプロジェクトが開かれたときに実行される既定のコマンドです。|

 次の例は HKEY_LOCAL_MACHINE からのものであり、レジストリのキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\99.0Exp\Packages] の下にあります。

## <a name="example-2"></a>例 2

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
   "CompanyName"="Microsoft"
   "ProductName"="Figure Project Sample"
   "ProductVersion"="9.0"
   "MinEdition"="professional"
   "ID"=dword:00000001
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\SatelliteDLL
   "DllName"="FigPrjUI.dll"
   "Path"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\Debug\\"
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\Automation
   "FigProjects"=""
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\AutomationEvents
   "FigProjectsEvents"="Returns the FigProjectsEvents Object"
   "FigProjectItemsEvents"="Returns the FigProjectItemsEvents Object"
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@` (既定値)|REG_SZ|`FigPrj Project VSPackage`|この登録された VSPackage のローカライズ可能な名前 (プロジェクトの種類)。|
|`InprocServer32`|REG_SZ|`%MODULE%`|プロジェクトの種類の DLL のパス。 IDE はこの DLL を読み込み、VSPackage CLSID をに渡して `DllGetClassObject` <xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory> 、オブジェクトを構築し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。|
|`CompanyName`|REG_SZ|`Microsoft`|プロジェクトの種類を開発した会社の名前。|
|`ProductName`|REG_SZ|`Figure Project Sample`|プロジェクトの種類の名前。|
|`ProductVersion`|REG_SZ|`9.0`|プロジェクトの種類のリリースのバージョン番号。|
|`MinEdition`|REG_SZ|`professional`|登録されている VSPackage のエディション。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|プロジェクト VSPackage のパッケージ読み込みキー。 このキーは、環境が開始された後にプロジェクトが読み込まれるときに検証されます。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|プロジェクトの種類のローカライズされたリソースを含むサテライト DLL のファイル名。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|サテライト DLL のパス。|
|`FigProjectsEvents`|REG_SZ|値については、「ステートメント」を参照してください。|このオートメーションイベントに対して返されるテキスト文字列を決定します。|
|`FigProjectItemsEvents`|REG_SZ|値については、「ステートメント」を参照してください。|このオートメーションイベントに対して返されるテキスト文字列を決定します。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-3"></a>例 3

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
   @="#4"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000000
   "FindInFilesFilter"=dword:00000000
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\2
      (Folder 2 contains settings for Find in Files filters.)
   @="#5"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000001
   "FindInFilesFilter"=dword:00000001
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (Second GUID indicates the registered project type for the Add Items templates.)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|この種類のプロジェクトの既定の名前。|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|パッケージに登録されているサテライト DLL から取得する名前のリソース ID。|
|`Package`|REG_SZ|`%CLSID_Package%`|パッケージに登録されている VSPackage のクラス ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|プロジェクトテンプレートファイルの既定のパス。 これらのファイルは、新しいプロジェクトテンプレートによって表示されます。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|プロジェクト項目テンプレートファイルの既定のパス。 これらのファイルは、[新しい項目の追加] テンプレートによって表示されます。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|IDE で [ **開く** ] ダイアログボックスを実装できるようにします。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|IDE で、開いているプロジェクトがこのプロジェクトの種類 (プロジェクトファクトリ) によって処理されるかどうかを判断するために使用されます。 複数のエントリの形式は、セミコロンで区切られたリストです。 たとえば、".vdproj; vdp" のようにします。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|名前を付けて保存操作の既定のファイル名拡張子として IDE によって使用されます。|
|`Filter Settings`|REG_DWORD|詳細については、次の表のステートメントとコメントを参照してください。|これらの設定は、UI ダイアログボックスでファイルを表示するためのさまざまなフィルターを設定するために使用されます。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|項目テンプレートの追加用のリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|[ **新しい項目の追加** ] テンプレートのダイアログボックスに表示されるプロジェクト項目のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|[ **新しい項目の追加** ] ダイアログボックスに表示されるファイルのツリーノード内の並べ替え順序を決定します。|

 次の表は、前のコードセグメントで使用できるフィルターオプションを示しています。

|フィルターオプション|説明|
|-------------------|-----------------|
|`CommonFindFilesFilter`|フィルターが [ **フォルダーを** 指定して検索] ダイアログボックスの一般的なフィルターの1つであることを示します。 共通フィルターが [共通] としてマークされていない場合は、フィルター一覧に共通のフィルターが一覧表示されます。|
|`CommonOpenFilesFilter`|フィルターが [ **ファイルを開く** ] ダイアログボックスの一般的なフィルターの1つであることを示します。 共通フィルターが [共通] としてマークされていない場合は、フィルター一覧に共通のフィルターが一覧表示されます。|
|`FindInFilesFilter`|フィルターが [ **フォルダーを** 指定して検索] ダイアログボックスのフィルターの1つであり、共通のフィルターの後に一覧表示されることを示します。|
|`NotOpenFileFilter`|[ **ファイルを開く** ] ダイアログボックスでフィルターを使用しないことを示します。|
|`NotAddExistingItemFilter`|[ **既存項目** の追加] ダイアログボックスでフィルターを使用しないことを示します。|

 既定では、フィルターにこれらのフラグが設定されていない場合、[ **既存項目の追加** ] ダイアログボックスと [ファイルを **開く** ] ダイアログボックスで、共通フィルターが一覧表示された後にフィルターが使用されます。 フィルターは、[ **フォルダーを** 選択して検索] ダイアログボックスでは使用されません。

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-4"></a>例 4

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|新しいプロジェクトテンプレートのリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|登録されているプロジェクトの種類のプロジェクトの既定のパス。|
|`SortPriority`|REG_DWORD|`41 (x29)`|[新しいプロジェクトウィザード] ダイアログボックスに表示されるプロジェクトの並べ替え順序を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0は、この種類のプロジェクトが [新しいプロジェクト] ダイアログボックスにのみ表示されることを示します。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] の下にあります。

## <a name="example-5"></a>例 5

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|なし|次のエントリがその他のファイルプロジェクトエントリ用であることを示す既定値。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|新しい項目の追加テンプレートファイルのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|[ **新しい項目の追加** ] ダイアログボックスに表示される項目の既定のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|[ **新しい項目の追加** ] ダイアログボックスのツリーノードに表示される並べ替え順序を設定します。|

 次の例は、レジストリのキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Menus] の下にあります。

## <a name="example-6"></a>例 6

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 メニューエントリは、メニュー情報の取得に使用されたリソースを IDE で参照します。 このデータがメニューデータベースにマージされると、レジストリの MenusMerged セクションに同じキーが追加されます。 VSPackage は、MenusMerged セクションの下にあるものを直接変更することはできません。 次の表のデータフィールドには、3つのコンマ区切りのフィールドがあります。 最初のフィールドは、メニューリソースファイルの完全パスを示します。

- 最初のフィールドを省略した場合、メニューリソースは VSPackage GUID で識別されるサテライト DLL から読み込まれます。

  2番目のフィールドは、型 CTMENU のメニューリソース ID を識別します。

- リソース ID が指定されていて、ファイルパスが最初のパラメーターによって指定されている場合、メニューリソースは完全なファイルパスから読み込まれます。

- リソース ID が指定されていても、ファイルパスがではない場合、メニューリソースはサテライト DLL から読み込まれます。

- 完全なファイルパスが指定されていて、リソース ID が省略されている場合は、読み込まれるファイルが CTO ファイルであることが必要です。

  最後のフィールドは、CTMENU リソースのバージョン番号を示します。 バージョン番号を変更することによって、もう一度メニューをマージできます。

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|% CLSID_Package%|REG_SZ|`,1000,1`|メニュー情報を取得するリソース。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\NewProjectTemplates] の下にあります。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|図プロジェクトの新しいプロジェクトテンプレートのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|新しいプロジェクトディレクトリの既定のパス。 このディレクトリ内の項目は、[ **新しいプロジェクトウィザード** ] ダイアログボックスに表示されます。|
|`SortPriority`|REG_DWORD|`41 (x29)`|[ **新しいプロジェクト** ] ダイアログボックスのツリーノードにプロジェクトを表示する順序を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0は、この種類のプロジェクトが [ **新しいプロジェクト** ] ダイアログボックスにのみ表示されることを示します。|

 次の例は、レジストリのキー [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\InstalledProducts] の下にあります。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名前|種類|データ|説明|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|登録されている VSPackage のクラス ID。|
|`UseInterface`|REG_DWORD|`1`|1は、このプロジェクトとの対話に UI が使用されることを示します。 0は、UI インターフェイスがないことを示します。|

 新しいプロジェクトの種類を制御する .vsz ファイルには、多くの場合 RELATIVE_PATH エントリが含まれています。 このパスは、次のセットアップキーで、プロジェクトの種類の \ productdir エントリの下に指定されたパスに対する相対パスです。

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup

 たとえば、エンタープライズフレームワークプロジェクトテンプレートでは、次のレジストリエントリが追加されます。

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup\EF\ProductDir = C:\Program Studio\EnterpriseFrameworks\ Visual

 つまり、.vsz ファイルに PROJECT_TYPE = EF エントリを含めると、環境では、前に指定した ProductDir ディレクトリにある .vsz ファイルが検索されます。

## <a name="see-also"></a>関連項目
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
