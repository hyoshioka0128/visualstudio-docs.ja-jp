---
title: プロジェクトテンプレートと項目テンプレートの登録 |Microsoft Docs
description: Visual Studio がプロジェクトの種類に関する登録情報を使用して、[新しいプロジェクトの追加] ダイアログボックスと [新しい項目の追加] ダイアログボックスに表示する内容を確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 999b435719113883201b7619daca9a84d095294e
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875272"
---
# <a name="registering-project-and-item-templates"></a>プロジェクトと項目テンプレートの登録
プロジェクトの種類では、プロジェクトテンプレートとプロジェクト項目テンプレートが配置されているディレクトリを登録する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトの種類に関連付けられている登録情報を使用して、[ **新しいプロジェクトの追加** ] および [ **新しい項目の追加** ] ダイアログボックスに表示する内容を決定します。

 テンプレートの詳細については、「 [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="registry-entries-for-projects"></a>プロジェクトのレジストリエントリ
 次の例では HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudioバージョン> の下にレジストリエントリが表示され \\ < ます。 これらの表では、例で使用される要素について説明します。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名前|Type|説明|
|----------|----------|-----------------|
|@|REG_SZ|この種類のプロジェクトの既定の名前。|
|DisplayName|REG_SZ|パッケージに登録されているサテライト DLL から取得する名前のリソース ID。|
|パッケージ|REG_SZ|パッケージに登録されているパッケージのクラス ID。|
|Projecttemplates ディレクトリ|REG_SZ|プロジェクトテンプレートファイルの既定のパス。 プロジェクトテンプレートファイルは、 **新しいプロジェクト** テンプレートによって表示されます。|

### <a name="registering-item-templates"></a>登録 (項目テンプレートを)
 項目テンプレートを格納するディレクトリを登録する必要があります。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名前 | Type | 説明 |
|--------------------------|-----------| - |
| @ | REG_SZ | 項目テンプレートの追加用のリソース ID。 |
| Templates ディレクトリ | REG_SZ | **新しい項目の追加** ウィザードのダイアログボックスに表示されるプロジェクト項目のパス。 |
| TemplatesLocalizedSubDir | REG_SZ | ローカライズされたテンプレートを保持する Templates ディレクトリのサブディレクトリに名前を指定する文字列のリソース ID。 では、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サテライト dll がある場合に文字列リソースが読み込まれるため、各サテライト dll にはローカライズされた別のサブディレクトリ名を含めることができます。 |
| SortPriority | REG_DWORD | [ **新しい項目の追加** ] ダイアログボックスでのテンプレートの表示順序を制御するには、[sortpriority] を設定します。 より大きな SortPriority 値がテンプレートリストの前に表示されます。 |

### <a name="registering-file-filters"></a>ファイルフィルターの登録
 必要に応じ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] て、ファイル名の入力を求められたときにが使用するフィルターを登録できます。 たとえば、[ [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] **ファイルを開く** ] ダイアログボックスのフィルターは次のとおりです。

 **Visual C# のファイル (.cs、.resx、. \* \* \* 設定、 \* .xsd、 \* .wsdl); \* 。cs、 \* .resx、 \* settings、 \* .xsd、 \* .wsdl)**

 複数のフィルターの登録をサポートするために、各フィルターは HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ < *バージョン*> \ Projects \\ { \<*ProjectGUID*> } \ フィルター \\ < *サブキー*> の下に独自のサブキーとして登録されます。 サブキーの名前は任意です。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サブキーの名前を無視し、その値だけを使用します。

 次の表に示すように、フラグを設定することによってフィルターを使用するコンテキストを制御できます。 フィルターにフラグが設定されていない場合、[ **既存項目の追加** ] ダイアログボックスと [ **ファイルを開く** ] ダイアログボックスの共通フィルターの後に一覧表示されますが、[ **フォルダーを** 指定して検索] ダイアログボックスでは使用されません。

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

|名前|Type|説明|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|[ **フォルダーを** 選択して検索] ダイアログボックスで、フィルターを共通のフィルターの1つにします。 共通フィルターが [共通] としてマークされていない場合、[フィルター] ボックスの一覧に一般的なフィルターが表示されます|
|CommonOpenFilesFilter|REG_DWORD|[ **ファイルを開く** ] ダイアログボックスで、フィルターを共通のフィルターの1つにします。 共通フィルターが [共通] としてマークされていない場合、[フィルター] ボックスの一覧に一般的なフィルターが表示されます|
|FindInFilesFilter|REG_DWORD|[ **フォルダーを** 選択して検索] ダイアログボックスの共通フィルターの後にフィルターが一覧表示されます。|
|NotOpenFileFilter|REG_DWORD|[ **ファイルを開く** ] ダイアログボックスでフィルターを使用しないことを示します。|
|NotAddExistingItemFilter|REG_DWORD|[ **既存項目の追加** ] ダイアログボックスでフィルターを使用しないことを示します。|
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
