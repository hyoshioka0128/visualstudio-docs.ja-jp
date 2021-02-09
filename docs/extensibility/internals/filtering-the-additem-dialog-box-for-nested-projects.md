---
title: 入れ子になったプロジェクトの [AddItem] ダイアログボックスのフィルター処理Microsoft Docs
description: 親プロジェクトの IVsFilterAddProjectItemDlg インターフェイスを実装することによって、Visual Studio で入れ子になったプロジェクトの [AddItem] ダイアログボックスをフィルター処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 668a1c3bae34caa2dc6a12def2bcee56765adbb1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99886952"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>入れ子になったプロジェクトの [AddItem] ダイアログボックスをフィルター処理する
入れ子になったプロジェクトに対して [ **AddItem** ] ダイアログボックスを表示すると、ダイアログボックスに表示される項目を親プロジェクトで制御できます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>インターフェイスを使用すると、[ **AddItem** ] ダイアログボックスに表示されるノードをフィルター処理できます。 子プロジェクトで [ **AddItem** ] ダイアログボックスが表示されている場合、親は、 `IVsFilterAddProjectItemDlg` 子のプロジェクトに表示されるインターフェイスとフィルター項目を実装できます。

 プロジェクトが特定の親プロジェクトの関数によってグループ化されている場合は、 `IVsFilterAddProjectItemDlg` 入れ子になったプロジェクトのショートカットメニューの [ **プロジェクト項目の追加** ] をユーザーが選択したときにを実装できます。 `IvsFilterAddProjectItemDlg displays`プロジェクト項目またはそのグループに固有のファイルのみを実装します。 他のグループのプロジェクト項目は、同じディレクトリに格納されている場合でも、ダイアログボックスからフィルターで除外されます。

 ユーザーが子の [ **AddItem** ] ダイアログボックスを開くと、親プロジェクトのインターフェイスの実装 `IVsFilterAddProjectItemDlg` が呼び出されます。

 インターフェイスでは、 `IVsFilterAddProjectItemDlg` カテゴリ別のフィルター処理を実装することもできます。 詳細については、「 [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) 」および「 [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [入れ子 (プロジェクトを)](../../extensibility/internals/nesting-projects.md)
