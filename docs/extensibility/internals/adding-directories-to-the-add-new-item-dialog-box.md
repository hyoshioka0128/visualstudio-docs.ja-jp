---
title: '[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する |マイクロソフトドキュメント'
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
ms.openlocfilehash: 1d4af79f95c87271e9a10eece6c728daa9a81305
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710250"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する
次のコード例は、[**新しい項目の追加**] ダイアログ ボックスのディレクトリの新しいセットを登録する方法を示しています。 **[新しい項目の追加**] ダイアログ ボックスのディレクトリは、プロジェクトごとに異なります。 したがって、ディレクトリは **、HKEY_LOCAL_MACHINE\ソフトウェア\VisualStudio\8.0Exp\プロジェクト**にある**プロジェクト**サブキーの下に登録されます。

## <a name="registry-script"></a>レジストリ スクリプト

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

 値`%Template_Path%`は、プロジェクト テンプレートを含むディレクトリの完全パスを指定します。 これらのテンプレートは、複製する *.vsz*ファイルまたはプロトタイプ テンプレート ファイルのいずれかです。

 値`SortPriority`は、並べ替えの優先順位を指定します。

## <a name="add-items-to-an-existing-project"></a>既存のプロジェクトに項目を追加する
 既存のプロジェクトに項目を追加することもできます。 たとえば、プロジェクトの[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]場合は、*\<ルート>\プログラム ファイル\Microsoft Visual Studio\VC#\CSharpProjectItems\LocalProjectItems*フォルダーに項目を追加できます。 この場合、C#`%GUID_Project%`プロジェクトの GUID です ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC})。

 プロジェクトのサブタイプをプログラミングして、既存のプロジェクトを拡張することもできます。 プロジェクトのサブタイプを使用すると、新しいプロジェクトタイプを書き込まずにプロジェクトを拡張できます。 プロジェクトのサブタイプの詳細については、「[プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
