---
title: '[新しい項目の追加] ダイアログボックスにディレクトリを追加する |Microsoft Docs'
description: レジストリスクリプトを使用してディレクトリを登録することにより、Visual Studio の [新しい項目の追加] ダイアログボックスにディレクトリを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d6a8090a47c275e66272ed3ee3e5d5a1eef1926d
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96189733"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログボックスにディレクトリを追加する
次のコード例は、[ **新しい項目の追加** ] ダイアログボックスのディレクトリの新しいセットを登録する方法を示しています。 [ **新しい項目の追加** ] ダイアログボックスのディレクトリは、プロジェクトごとに異なります。 そのため、ディレクトリは、 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects** にある **Projects** サブキーの下に登録されます。

## <a name="registry-script"></a>レジストリスクリプト

```
NoRemove Projects
{
  NoRemove %GUID_Project%
  {
    NoRemove AddItemTemplates
    {
      NoRemove TemplateDirs
      {
        ForceRemove %CLSID_Package%
        {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
          {
            val TemplatesDir = s '%Template_Path%'
            val SortPriority = d 2000
          }
        }
      }
    }
  }
}
```

 値は、 `%Template_Path%` プロジェクトテンプレートが格納されているディレクトリの完全パスを指定します。 これらのテンプレートには、 *.vsz* ファイルまたは複製する典型的なテンプレートファイルを指定できます。

 `SortPriority`値は並べ替えの優先順位を指定します。

## <a name="add-items-to-an-existing-project"></a>既存のプロジェクトへの項目の追加
 既存のプロジェクトに項目を追加することもできます。 たとえば、プロジェクトの場合は、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] *\<root> Studio\VC # \CSharpProjectItems\LocalProjectItems* フォルダーに項目を追加できます。 この場合、 `%GUID_Project%` は C# プロジェクト ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) の GUID です。

 また、プロジェクトのサブタイプをプログラミングすることによって、既存のプロジェクトを拡張することもできます。 プロジェクトのサブタイプを使用すると、新しいプロジェクトの種類を記述せずにプロジェクトを拡張できます。 プロジェクトのサブタイプの詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しいプロジェクト] ダイアログボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
