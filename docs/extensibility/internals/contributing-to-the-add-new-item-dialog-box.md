---
title: '[新しい項目の追加] ダイアログボックスに貢献する |Microsoft Docs'
description: Visual Studio の [新しい項目の追加] ダイアログボックスを表示する方法については、「Projects レジストリサブキーの下に項目テンプレートを追加する」を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e3fdc5705cad0ec696a520350042d7f18aaec146
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99884638"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログボックスに投稿する
**Projects** サブキーの下に **項目** テンプレートを追加することにより、プロジェクトのサブタイプは、[**新しい項目の追加**] ダイアログボックスの項目の完全な新しいディレクトリを提供できます。

## <a name="register-add-new-item-templates"></a>新しい項目テンプレートの追加の登録
 このセクションは、レジストリの [ **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects** ] の下にあります。 以下のレジストリエントリは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトが仮定のプロジェクトサブタイプによって集計されていることを前提としています。 プロジェクトのエントリを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以下に示します。

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

 **AddItemTemplates\TemplateDirs** サブキーには、[**新しい項目の追加**] ダイアログボックスで使用できるようになった項目が配置されるディレクトリへのパスを含むレジストリエントリが含まれています。

 環境では、**プロジェクト** のレジストリサブキーの下に、すべての **additemtemplates** データが自動的に読み込まれます。 このデータには、基本プロジェクトの実装のデータと、特定の種類のプロジェクトのサブタイプのデータを含めることができます。 各プロジェクトのサブタイプは、プロジェクトの種類の **GUID** によって識別されます。 プロジェクトのサブタイプでは、実装内のの列挙をサポートして `VSHPROPID_ AddItemTemplatesGuid` プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> サブタイプの GUID 値を返すことによって、特定の flavored プロジェクトインスタンスに対して追加項目テンプレートの代替セットを使用するように指定できます。 プロパティが指定されていない場合は、 `VSHPROPID_AddItemTemplatesGuid` 基本プロジェクト GUID が使用されます。

 [ **新しい項目の追加** ] ダイアログボックスで項目をフィルター処理するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> プロジェクトのサブタイプアグリゲーターオブジェクトにインターフェイスを実装します。 たとえば、プロジェクトを集計することによってデータベースプロジェクトを実装するプロジェクトのサブタイプでは、フィルター処理を実装することで、[ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **新しい項目の追加** ] ダイアログボックスから特定の項目をフィルター処理できます。さらに、でをサポートすることにより、データベースプロジェクト固有の項目を追加でき `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> ます。 [ **新しい項目の追加** ] ダイアログボックスにフィルターを適用して項目を追加する方法の詳細については、「 [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトの拡張に通常使用されるオブジェクトの Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
