---
title: '[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する |マイクロソフトドキュメント'
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710246"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する
新しいプロジェクトタイプを作成する場合は、[**新しいプロジェクト**]ダイアログボックスで新しいディレクトリを登録して、テンプレートとして使用するためにそれらを表示することもできます。 次のコード例では、新しいディレクトリ (ノードとも呼ばれます) を登録する方法について説明します。 この例では、VSPackage *CLSID_Package*によって公開されるテンプレートが登録されています。 その結果、[**新しいプロジェクト**] ダイアログ ボックスの左側には *、Folder_Label_ResID*リソースによって決定される名前を持つ追加されたノードが表示されます。 このリソースは、VSPackage サテライト DLL から読み込まれます。

 **Folder**値は *、Folder_Label_ResID*ノードが表示されるフォルダーの GUID を表します。 この例では、GUID は [**新しい**プロジェクト] ダイアログ ボックスの [**プロジェクトの種類**] ウィンドウの **[その他**のプロジェクト] フォルダーを表します。 **[その他のプロジェクト]** の値が存在しない場合、ラベルは最上位レベルに配置されます。

 値`TemplatesDir`は、プロジェクト テンプレートを含むディレクトリの完全パスを指定します。 これらのファイルは *、複製する .vsz*ファイルまたは一般的なテンプレート ファイルのいずれかです。

 を指定`TemplatesLocalizedSubDir`する場合は、ローカライズされたテンプレートを格納するサブディレクトリの名前を指定する文字列`TemplatesDir`のリソース ID である必要があります。 文字列[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]リソースが読み込まれている場合はサテライト DLL から読み込まれるので、各サテライト DLL には異なるサブディレクトリ名を含めることができます。 値`SortPriority`は、並べ替えの優先順位を指定します。

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
- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
