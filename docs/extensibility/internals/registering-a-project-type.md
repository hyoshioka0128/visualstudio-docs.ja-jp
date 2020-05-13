---
title: プロジェクトタイプの登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05ac1f393632934f193f5f4efaaf9e5459ffbb14
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705868"
---
# <a name="registering-a-project-type"></a>プロジェクト タイプの登録
新しいプロジェクトの種類を作成する場合は、プロジェクトの種類[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を認識して作業するためのレジストリ エントリを作成する必要があります。 通常、これらのレジストリ エントリは、レジストリ スクリプト (.rgs) ファイルを使用して作成します。

 次の例では、レジストリのステートメントは、既定のパスとデータを提供します (該当する場合)。 これらの表は、スクリプトのエントリと、ステートメントに関する追加情報を提供します。

> [!NOTE]
> 次のレジストリ情報は、プロジェクトの種類を登録するために記述するレジストリ スクリプトのエントリの種類と目的の例を示しています。 実際のエントリとその用途は、プロジェクトの種類の要件によって異なる場合があります。 開発中のプロジェクトの種類に近いサンプルを見つけ出すために使用できるサンプルを確認し、そのサンプルのレジストリ スクリプトを確認する必要があります。

 以下の例はHKEY_CLASSES_ROOTです。

## <a name="example"></a>例

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

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|拡張子が .figp のプロジェクト タイプ ファイルの名前と説明。|
|`Content Type`|REG_SZ|`Text/plain`|プロジェクト ファイルのコンテンツ タイプ。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|このタイプのプロジェクトに使用される既定のアイコンです。 %MODULE% ステートメントは、プロジェクトの種類 DLL の既定の場所にレジストリで完了します。|
|`@`|REG_SZ|`&Open in Visual Studio`|このプロジェクトの種類が開かれる既定のアプリケーションです。|
|`@`|REG_SZ|`devenv.exe "%1"`|この種類のプロジェクトを開いたときに実行される既定のコマンド。|

 次の例はHKEY_LOCAL_MACHINEで、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\Microsoft\VisualStudio\99.0Exp\パッケージ] の下にあります。

## <a name="example"></a>例

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
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

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@` (既定値)|REG_SZ|`FigPrj Project VSPackage`|この登録された VSPackage (プロジェクトの種類) のローカライズ可能な名前。|
|`InprocServer32`|REG_SZ|`%MODULE%`|プロジェクトの種類 DLL のパス。 IDE はこの DLL を読み込み、`DllGetClassObject`<xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory><xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>オブジェクトを構築するために VSPackage CLSID を渡します。|
|`CompanyName`|REG_SZ|`Microsoft`|プロジェクトタイプを開発した会社の名前。|
|`ProductName`|REG_SZ|`Figure Project Sample`|プロジェクトの種類の名前。|
|`ProductVersion`|REG_SZ|`9.0`|プロジェクトタイプリリースのバージョン番号です。|
|`MinEdition`|REG_SZ|`professional`|登録されている VS パッケージのエディション。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|プロジェクト VSPackage のパッケージの読み込みキー。 環境の開始後にプロジェクトが読み込まれるときに、キーが検証されます。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|プロジェクトの種類に対応するローカライズされたリソースを含むサテライト DLL のファイル名。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|サテライト DLL のパス。|
|`FigProjectsEvents`|REG_SZ|値については、ステートメントを参照してください。|このオートメーション イベントに対して返されるテキスト文字列を決定します。|
|`FigProjectItemsEvents`|REG_SZ|値については、ステートメントを参照してください。|このオートメーション イベントに対して返されるテキスト文字列を決定します。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\プロジェクト] の下にあります。

## <a name="example"></a>例

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
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
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|この種類のプロジェクトの既定の名前です。|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|パッケージに登録されたサテライト DLL から取得される名前のリソース ID。|
|`Package`|REG_SZ|`%CLSID_Package%`|パッケージの下に登録された VSPackage のクラス ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|プロジェクト テンプレート ファイルの既定のパス。 これらは、新しいプロジェクト テンプレートによって表示されるファイルです。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|プロジェクト項目テンプレート ファイルの既定のパス。 これらは、[新しい項目の追加] テンプレートによって表示されるファイルです。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|IDE が **[開く**] ダイアログ ボックスを実装できるようにします。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|IDE が、開いているプロジェクトがこのプロジェクトの種類 (プロジェクト ファクトリ) によって処理されるかどうかを判断するために使用されます。 複数のエントリの形式は、セミコロンで区切られたリストです。 例えば"vdproj;vdp"。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|IDE で[名前を付けて保存]操作の既定のファイル名拡張子として使用されます。|
|`Filter Settings`|REG_DWORD|さまざまなステートメントとコメントを次の表に示します。|これらの設定は、UI ダイアログ ボックスにファイルを表示するためのさまざまなフィルターを設定するために使用されます。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|項目追加テンプレートのリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|**[新しい項目の追加]** テンプレートのダイアログ ボックスに表示されるプロジェクト項目のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|[**新しい項目の追加**] ダイアログ ボックスに表示されるファイルのツリー ノードでの並べ替え順序を指定します。|

 次の表は、前のコード セグメントで使用できるフィルター オプションを示しています。

|フィルタ オプション|説明|
|-------------------|-----------------|
|`CommonFindFilesFilter`|フィルターが **[ファイル**内の検索] ダイアログ ボックスの一般的なフィルターの 1 つであることを示します。 共通フィルターは、フィルターが共通としてマークされていない前にフィルター・リストにリストされます。|
|`CommonOpenFilesFilter`|フィルタが [**ファイルを開く**] ダイアログ ボックスの一般的なフィルタの 1 つであることを示します。 共通フィルターは、フィルターが共通としてマークされていない前にフィルター・リストにリストされます。|
|`FindInFilesFilter`|フィルターが **[ファイル**内の検索] ダイアログ ボックスのフィルターの 1 つになり、共通のフィルターの後に表示されることを示します。|
|`NotOpenFileFilter`|[**ファイルを開く**] ダイアログ ボックスでフィルタを使用しないことを示します。|
|`NotAddExistingItemFilter`|[**既存項目**の追加] ダイアログ ボックスでフィルターを使用しないことを示します。|

 既定では、フィルタにこれらのフラグが設定されていない場合は、[**既存項目の追加**] ダイアログ ボックスと共通フィルタの一覧の後にある **[ファイルを開く**] ダイアログ ボックスでフィルタが使用されます。 フィルタは、[ファイル内の検索] ダイアログ ボックス**では**使用されません。

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\プロジェクト] の下にあります。

## <a name="example"></a>例

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|新しいプロジェクト テンプレートのリソース ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|登録されているプロジェクトの種類のプロジェクトの既定のパスです。|
|`SortPriority`|REG_DWORD|`41 (x29)`|[新規プロジェクト]ウィザードダイアログボックスに表示されるプロジェクトのソート順を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 は、この種類のプロジェクトが [新しいプロジェクト] ダイアログ ボックスにのみ表示されることを示します。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\プロジェクト] の下にあります。

## <a name="example"></a>例

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|None|[その他のファイル] プロジェクトのエントリに対して、次のエントリを示す既定値。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|[新しい項目の追加] テンプレート ファイルのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|**[新しい**項目の追加] ダイアログ ボックスに表示される項目の既定のパス。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|[**新しい項目の追加**] ダイアログ ボックスのツリー ノードに表示する並べ替え順序を設定します。|

 次の例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\メニュー] の下にあります。

## <a name="example"></a>例

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 メニューエントリは、メニュー情報を取得するために使用されるリソースを IDE に示します。 このデータがメニュー データベースにマージされると、同じキーがレジストリの MenusMerged セクションに追加されます。 VSPackage は、メニューマージ セクションの下で直接何も変更しないでください。 次の表の [データ] フィールドには、3 つのコンマ区切りフィールドがあります。 最初のフィールドは、メニュー リソース ファイルの完全パスを示します。

- 最初のフィールドを省略すると、メニュー リソースは、VSPackage GUID によって識別されるサテライト DLL から読み込まれます。

  2 番目のフィールドは、タイプ CTMENU のメニュー リソース ID を識別します。

- リソース ID が指定され、ファイル パスが最初のパラメーターによって指定された場合、メニュー リソースは完全なファイル パスから読み込まれます。

- リソース ID が指定されているが、ファイル パスが指定されていない場合、メニュー リソースはサテライト DLL から読み込まれます。

- フル ファイル パスが指定され、リソース ID が省略された場合、読み込まれるファイルは CTO ファイルであると想定されます。

  最後のフィールドは、CTMENU リソースのバージョン番号を示します。 バージョン番号を変更すると、メニューを再度マージできます。

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|%CLSID_Package%|REG_SZ|`,1000,1`|メニュー情報を取得するリソース。|

 次のすべての例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\NewProjectTemplates] の下にあります。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|図プロジェクトの新しいプロジェクト テンプレートのリソース ID 値。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|新しいプロジェクト ディレクトリの既定のパス。 このディレクトリ内の項目は、**新規プロジェクトウィザード**ダイアログボックスに表示されます。|
|`SortPriority`|REG_DWORD|`41 (x29)`|[**新しい**プロジェクト] ダイアログ ボックスのツリー ノードにプロジェクトを表示する順序を設定します。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 は、この種類のプロジェクトが **[新しいプロジェクト**] ダイアログ ボックスにのみ表示されることを示します。|

 次の例は、レジストリの [HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\9.0Exp\インストールされた製品] の下にあります。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名前|Type|Data|説明|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|登録された VS パッケージのクラス ID。|
|`UseInterface`|REG_DWORD|`1`|1 は、このプロジェクトと対話するために UI が使用されることを示します。 0 は、UI インターフェイスがないことを示します。|

 新しいプロジェクトの種類を制御する .vsz ファイルには、多くの場合、RELATIVE_PATHエントリが含まれています。 このパスは、次のセットアップ キーのプロジェクトの種類の \ProductDir エントリの下に指定されたパスを基準にしています。

 HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\7.0Exp\セットアップ

 たとえば、エンタープライズ フレームワーク プロジェクト テンプレートは、次のレジストリ エントリを追加します。

 HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\7.0Exp\セットアップ\EF\製品ディレクトリ = C:\プログラム ファイル\マイクロソフト ビジュアル スタジオ\エンタープライズ フレームワーク\

 つまり、.vsz ファイルに PROJECT_TYPE=EF エントリを含める場合、環境は、以前に指定した ProductDir ディレクトリに .vsz ファイルを検索します。

## <a name="see-also"></a>関連項目
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
