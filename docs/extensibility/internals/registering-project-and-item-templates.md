---
title: プロジェクトテンプレートと項目テンプレートの登録 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e35a476ab8fe8d8de3ce11dd117de4c84a3befa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724627"
---
# <a name="registering-project-and-item-templates"></a>プロジェクトと項目テンプレートの登録
プロジェクトの種類では、プロジェクトテンプレートとプロジェクト項目テンプレートが配置されているディレクトリを登録する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、プロジェクトの種類に関連付けられている登録情報を使用して、 **[新しいプロジェクトの追加]** ダイアログボックスと **[新しい項目の追加]** ダイアログボックスに表示する内容を決定します。

 テンプレートの詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="registry-entries-for-projects"></a>プロジェクトのレジストリエントリ
 次の例では、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio \\ <*バージョン*> のレジストリエントリを示します。 これらの表では、例で使用される要素について説明します。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名|[種類]|説明|
|----------|----------|-----------------|
|@|REG_SZ|この種類のプロジェクトの既定の名前。|
|DisplayName|REG_SZ|パッケージに登録されているサテライト DLL から取得する名前のリソース ID。|
|Package|REG_SZ|パッケージに登録されているパッケージのクラス ID。|
|Projecttemplates ディレクトリ|REG_SZ|プロジェクトテンプレートファイルの既定のパス。 プロジェクトテンプレートファイルは、**新しいプロジェクト**テンプレートによって表示されます。|

### <a name="registering-item-templates"></a>登録 (項目テンプレートを)
 項目テンプレートを格納するディレクトリを登録する必要があります。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名 | [種類] | 説明 |
|--------------------------|-----------| - |
| @ | REG_SZ | 項目テンプレートの追加用のリソース ID。 |
| Templates ディレクトリ | REG_SZ | **新しい項目の追加**ウィザードのダイアログボックスに表示されるプロジェクト項目のパス。 |
| TemplatesLocalizedSubDir | REG_SZ | ローカライズされたテンプレートを保持する Templates ディレクトリのサブディレクトリに名前を指定する文字列のリソース ID。 @No__t_0 は、サテライト Dll がある場合は文字列リソースを読み込むため、各サテライト DLL にはローカライズされた別のサブディレクトリ名を含めることができます。 |
| SortPriority | REG_DWORD | **新しい項目の追加** ダイアログボックスでのテンプレートの表示順序を制御するには、sortpriority を設定します。 より大きな SortPriority 値がテンプレートリストの前に表示されます。 |

### <a name="registering-file-filters"></a>ファイルフィルターの登録
 必要に応じて、ファイル名の入力を求められたときに [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用するフィルターを登録できます。 たとえば、 **[ファイルを開く]** ダイアログボックスの [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] フィルターは次のとおりです。

 **ビジュアルC#ファイル (\*、\* .resx、\*。設定、\*、\*)、です。\* .cs、\* .resx、\* の設定、0 .xsd、1)**

 複数のフィルターの登録をサポートするために、各フィルターは、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio \\ の下で独自のサブキーに登録されます。 <*バージョン*> のプロジェクト \\ {\<*projectguid*>} \ filters<*サブキー*の > を \\ します。 サブキーの名前は任意です。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、サブキーの名前を無視し、その値だけを使用します。

 次の表に示すように、フラグを設定することによってフィルターを使用するコンテキストを制御できます。 フィルターにフラグが設定されていない場合、 **[既存項目の追加]** ダイアログボックスと **[ファイルを開く]** ダイアログボックスの共通フィルターの後に一覧表示されますが、 **[フォルダーを]** 指定して検索 ダイアログボックスでは使用されません。

```
[Projects\{ProjectGUID}\Filters\MyLanguageFilter]
@="#3"
"CommonOpenFilesFilter"=dword:00000000
"CommonFindFilesFilter"=dword:00000000
"FindInFilesFilter"=dword:00000000
"NotOpenFileFilter"=dword:00000000
"NotAddExistingItemFilter"=dword:00000000
"SortPriority"=dword:00000064
```

|名|[種類]|説明|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|[**フォルダーを**選択して検索] ダイアログボックスで、フィルターを共通のフィルターの1つにします。 共通フィルターが [共通] としてマークされていない場合、[フィルター] ボックスの一覧に一般的なフィルターが表示されます|
|CommonOpenFilesFilter|REG_DWORD|**[ファイルを開く]** ダイアログボックスで、フィルターを共通のフィルターの1つにします。 共通フィルターが [共通] としてマークされていない場合、[フィルター] ボックスの一覧に一般的なフィルターが表示されます|
|FindInFilesFilter|REG_DWORD|[**フォルダーを**選択して検索] ダイアログボックスの共通フィルターの後にフィルターが一覧表示されます。|
|NotOpenFileFilter|REG_DWORD|**[ファイルを開く]** ダイアログボックスでフィルターを使用しないことを示します。|
|NotAddExistingItemFilter|REG_DWORD|**[既存項目の追加]** ダイアログボックスでフィルターを使用しないことを示します。|
|SortPriority|REG_DWORD|SortPriority を設定して、フィルターを表示する順序を制御します。 より大きな SortPriority 値が、フィルター一覧の前に表示されます。|

## <a name="directory-structure"></a>ディレクトリの構造
 Vspackage では、統合開発環境 (IDE) によって場所が登録されていれば、ローカルまたはリモートのディスク上の任意の場所にテンプレートファイルとフォルダーを配置できます。 ただし、組織を簡単にするために、製品のインストールパスの下に次のディレクトリ構造を使用することをお勧めします。

 \ テンプレート

 \ プロジェクト (プロジェクトテンプレートが含まれています)

 (\Applications

 \ コンポーネント

 \ ...

 \ProjectItems (プロジェクト項目を含む)

 \ クラス

 \ フォーム

 \Web ページ

 \ ファイル (複数ファイルのプロジェクトアイテムで使用されるファイルを含む)

 \ Wizardfiles

## <a name="see-also"></a>関連項目

- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [アプリケーションのローカライズ](../../ide/globalizing-and-localizing-applications.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
