---
title: プロジェクトテンプレートと項目テンプレートの登録 |マイクロソフトドキュメント
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
ms.openlocfilehash: b64504c39b1fc3c4a82530b265cfd0e96832b4f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705821"
---
# <a name="registering-project-and-item-templates"></a>プロジェクトと項目テンプレートの登録
プロジェクトの種類は、プロジェクトとプロジェクト項目のテンプレートが配置されているディレクトリを登録する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、プロジェクトの種類に関連付けられた登録情報を使用して、[**新しいプロジェクトの追加]** ダイアログ ボックスと [**新しい項目の追加]** ダイアログ ボックスに表示する内容を決定します。

 テンプレートの詳細については、「[プロジェクトテンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="registry-entries-for-projects"></a>プロジェクトのレジストリ エントリ
 次の例は、HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\\<*バージョン*>の下のレジストリ エントリを示しています。 付属の表では、例で使用される要素について説明します。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名前|Type|説明|
|----------|----------|-----------------|
|@|REG_SZ|この種のプロジェクトの既定の名前です。|
|DisplayName|REG_SZ|パッケージに登録されたサテライト DLL から取得される名前のリソース ID。|
|Package|REG_SZ|パッケージに登録されたパッケージのクラス ID。|
|プロジェクトテンプレートディレクトリ|REG_SZ|プロジェクト テンプレート ファイルの既定のパス。 プロジェクト テンプレート ファイルは、**新しいプロジェクト**テンプレートによって表示されます。|

### <a name="registering-item-templates"></a>項目テンプレートの登録
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
| @ | REG_SZ | 項目追加テンプレートのリソース ID。 |
| テンプレートディレクトリ | REG_SZ | **新しい項目の追加**ウィザードのダイアログ ボックスに表示されるプロジェクト項目のパス。 |
| テンプレートローカライズされたサブディレクトリ | REG_SZ | ローカライズされたテンプレートを保持する TemplatesDir のサブディレクトリに名前を付け、文字列のリソース ID。 サ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]テライト DLL がある場合は文字列リソースを読み込むため、各サテライト DLL には異なるローカライズされたサブディレクトリ名を含めることができます。 |
| SortPriority | REG_DWORD | [**新しい項目の追加**] ダイアログ ボックスでテンプレートを表示する順序を指定するには、SortPriority を設定します。 大きい並べ替え優先順位の値は、テンプレート リストの前半に表示されます。 |

### <a name="registering-file-filters"></a>ファイル フィルタの登録
 必要に応じて、ファイル名の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]入力を求めるときに使用するフィルターを登録できます。 たとえば、[ファイルを[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]**開く**] ダイアログ ボックスのフィルタは次のようになります。

 **Visual C#\*ファイル (\*.cs,\*.resx,\*\*.settings, .xsd, .wsdl);\*cs、.resx、.settings、.xsd、.wsdl)\*\*\*\***

 複数のフィルターの登録をサポートするために、各フィルターは、HKEY_LOCAL_MACHINE\ソフトウェア\VisualStudio\\<*バージョン*>\プロジェクト\\{\<*ProjectGUID*>}\Filters\\<*サブキー*>の下の独自のサブキーに登録されます。 サブキー名は任意です。[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]サブキーの名前を無視し、その値だけを使用します。

 次の表に示すようにフラグを設定することで、フィルタが使用されるコンテキストを制御できます。 フィルタにフラグが設定されていない場合は、[**既存項目の追加**] ダイアログ ボックスと **[ファイルを開く**] ダイアログ ボックスの一般的なフィルタの後に一覧表示されますが、[**ファイル内の検索**] ダイアログ ボックスでは使用されません。

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
|フィルタを検索します。|REG_DWORD|[ファイル内の検索] ダイアログ ボックスで、フィルタを一般的なフィルタ**の**1 つにします。 共通フィルターは、フィルターが共通としてマークされていない前にフィルター・リストにリストされます。|
|一般的なファイルフィルター|REG_DWORD|[**ファイルを開く**] ダイアログ ボックスで、フィルタを一般的なフィルタの 1 つにします。 共通フィルターは、フィルターが共通としてマークされていない前にフィルター・リストにリストされます。|
|フィルタを検索します。|REG_DWORD|[ファイル内の検索] ダイアログ ボックスで、共通のフィルターの後**にフィルターを**一覧表示します。|
|ファイルフィルターを開かない|REG_DWORD|[**ファイルを開く**] ダイアログ ボックスでフィルタが使用されないことを示します。|
|フィールドを追加する既存のアイテムフィルター|REG_DWORD|**[既存項目の追加]** ダイアログ ボックスでフィルターが使用されないことを示します。|
|SortPriority|REG_DWORD|フィルタの表示順序を制御するには、SortPriority を設定します。 大きい並べ替え優先順位の値は、フィルター リストの前に表示されます。|

## <a name="directory-structure"></a>ディレクトリの構造
 VSPackages は、統合開発環境 (IDE) を通じて場所が登録されている限り、ローカルディスクまたはリモートディスク上の任意の場所にテンプレートファイルとフォルダを配置できます。 ただし、組織を容易にするため、製品のインストール パスの下に次のディレクトリ構造を使用することをお勧めします。

 \テンプレート

 \プロジェクト (プロジェクト テンプレートを含む)

 \アプリケーション

 \コンポーネント

 \ ...

 \プロジェクトアイテム (プロジェクト項目を含む)

 \クラス

 \フォーム

 \Web ページ

 \HelperFiles (複数ファイルのプロジェクト項目で使用されるファイルが含まれています)

 \ウィザードファイル

## <a name="see-also"></a>関連項目

- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [アプリケーションのローカライズ](../../ide/globalizing-and-localizing-applications.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
