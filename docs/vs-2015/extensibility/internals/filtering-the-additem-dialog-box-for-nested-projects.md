---
title: 入れ子になったプロジェクトの [AddItem] ダイアログボックスのフィルター処理Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7bb98eac2bc481aa5e3652144dfbcadf70430d04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538097"
---
# <a name="filtering-the-additem-dialog-box-for-nested-projects"></a>入れ子になったプロジェクトのための [AddItem] ダイアログ ボックスのフィルター処理
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

入れ子になったプロジェクトに対して [ **AddItem** ] ダイアログボックスを表示すると、ダイアログボックスに表示される項目を親プロジェクトで制御できます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>インターフェイスを使用すると、[ **AddItem** ] ダイアログボックスに表示されるノードをフィルター処理できます。 子プロジェクトで [ **AddItem** ] ダイアログボックスが表示されている場合、親は、 `IVsFilterAddProjectItemDlg` 子のプロジェクトに表示されるインターフェイスとフィルター項目を実装できます。  
  
 プロジェクトが特定の親プロジェクトの関数によってグループ化されている場合は、 `IVsFilterAddProjectItemDlg` 入れ子になったプロジェクトのショートカットメニューの [ **プロジェクト項目の追加** ] をユーザーが選択したときにを実装できます。 `IvsFilterAddProjectItemDlg displays`プロジェクト項目またはそのグループに固有のファイルのみを実装します。 他のグループのプロジェクト項目は、同じディレクトリに格納されている場合でも、ダイアログボックスからフィルターで除外されます。  
  
 ユーザーが子の [ **AddItem** ] ダイアログボックスを開くと、親プロジェクトのインターフェイスの実装 `IVsFilterAddProjectItemDlg` が呼び出されます。  
  
 インターフェイスでは、 `IVsFilterAddProjectItemDlg` カテゴリ別のフィルター処理を実装することもできます。 詳細については、「 [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) 」および「 [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [プロジェクトテンプレートと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)   
 [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
