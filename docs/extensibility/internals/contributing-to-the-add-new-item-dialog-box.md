---
title: '[新しい項目の追加] ダイアログ ボックスに貢献する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83444d9be6ba23392b792a0187bf46dc9920c465
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709276"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスに投稿する
プロジェクトのサブタイプは、**プロジェクト**のレジストリ サブキーの下に**項目の追加**テンプレートを登録することで **、新しい項目の追加**] ダイアログ ボックスの項目の完全な新しいディレクトリを提供できます。

## <a name="register-add-new-item-templates"></a>登録 新しい項目の追加テンプレート
 このセクションは、レジストリ内**のHKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\8.0\Projects**にあります。 以下のレジストリ エントリは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、架空のプロジェクト サブタイプによって集計されたプロジェクトを想定しています。 プロジェクトのエントリは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以下のとおりです。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]
@="#2143"
"DefaultProjectExtension"="vbproj"
"PossibleProjectExtensions"="vbproj;vbp"
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]
@="#100"
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"
```

 **AddItemTemplates\TemplateDirs**サブキーには、**新しい項目の追加**ダイアログ ボックスで利用可能になった項目が配置されているディレクトリへのパスを持つレジストリ エントリが含まれています。

 環境は、**プロジェクト**のレジストリ サブキーの下に**AddItemTemplates**データのすべてを自動的に読み込みます。 このデータには、基本プロジェクト実装のデータと、特定のプロジェクトのサブタイプタイプのデータを含めることができます。 各プロジェクト のサブタイプは、 プロジェクトの種類**GUID**で識別されます。 プロジェクト サブタイプは、プロジェクトのサブタイプの GUID 値を返すために実装`VSHPROPID_ AddItemTemplatesGuid`<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>の<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>列挙をサポートすることで、特定のフレーバープロジェクト インスタンスに対して**項目の追加**テンプレートの代替セットを使用するように指定できます。 プロパティが`VSHPROPID_AddItemTemplatesGuid`指定されていない場合は、基本プロジェクト GUID が使用されます。

 プロジェクトのサブタイプ アグリゲーター オブジェクトにインターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>実装することで、[**新しい項目の追加**] ダイアログ ボックスで項目をフィルター処理できます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]たとえば、プロジェクトを集計してデータベース プロジェクトを実装するプロジェクト サブタイプは、フィルター処理を実装して[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**[新しい項目の追加**] ダイアログ ボックスから特定の項目をフィルター処理し、次に、 で`VSHPROPID_ AddItemTemplatesGuid`<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>サポートすることによってデータベース プロジェクト固有の項目を追加できます。 [新しい項目の追加] ダイアログ ボックスにアイテムを追加するフィルター処理とアイテムの追加の詳細については **、「[新しい項目**[の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
