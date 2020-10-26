---
title: '[新しいプロジェクト] ダイアログボックスにディレクトリを追加する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 827e383bba13c9742deb654bf3d680adeb3c109b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80710246"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログボックスにディレクトリを追加する
新しいプロジェクトの種類を作成するときに、[ **新しいプロジェクト** ] ダイアログボックスに新しいディレクトリを登録して、テンプレートとして使用できるように表示することもできます。 次のコード例では、新しいディレクトリ (ノードとも呼ばれる) を登録する方法について説明します。 この例では、VSPackage、 *CLSID_Package*によって公開されているテンプレートが登録されています。 結果として、[ **新しいプロジェクト** ] ダイアログボックスの左側には、追加したノードが、 *Folder_Label_ResID* リソースによって決定される名前と共に提供されます。 このリソースは、VSPackage サテライト DLL から読み込まれます。

 **フォルダー**の値は、 *Folder_Label_ResID*ノードが表示されるフォルダーの GUID を表します。 この例では、GUID は [**新しいプロジェクト**] ダイアログボックスの [**プロジェクトの種類**] ペインにある [**その他のプロジェクト**] フォルダーを表します。 [ **その他のプロジェクト** ] の値が存在しない場合、ラベルは最上位レベルに配置されます。

 値は、 `TemplatesDir` プロジェクトテンプレートが格納されているディレクトリの完全パスを指定します。 これらのファイルには、 *.vsz* ファイルまたは複製する一般的なテンプレートファイルを指定できます。

 を指定する場合 `TemplatesLocalizedSubDir` 、 `TemplatesDir` ローカライズされたテンプレートを保持するのサブディレクトリに名前を指定する文字列のリソース ID にする必要があります。 では、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サテライト dll がある場合は文字列リソースを読み込みます。サテライト dll がある場合は、各サテライト dll に異なるサブディレクトリ名を含めることができます。 `SortPriority`値は並べ替えの優先順位を指定します。

```
NoRemove NewProjectTemplates
{
    NoRemove TemplateDirs
  {
    ForceRemove %CLSID_Package%
    {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
      {
        val Folder = s '{DCF2A94A-45B0-11D1-ADBF-00C04FB6BE4C}'
        val TemplatesDir = s '%Template_Path%'
        val TemplatesLocalizedSubDir = s '#100'
        val SortPriority = d 1000
      }
    }
  }
}
```

## <a name="see-also"></a>関連項目
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しい項目の追加] ダイアログボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
