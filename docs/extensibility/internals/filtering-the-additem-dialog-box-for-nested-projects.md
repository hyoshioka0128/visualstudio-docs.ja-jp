---
title: 入れ子になったプロジェクトの [AddItem] ダイアログ ボックスのフィルタ処理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2bc97b6041f4844ff71fe1d38a7103e1219888be
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708380"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>入れ子になったプロジェクトの [AddItem] ダイアログ ボックスをフィルタ処理する
入れ子になったプロジェクトの**AddItem**ダイアログ ボックスを表示すると、親プロジェクトはダイアログ ボックスに表示する項目を制御できます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>インターフェイスを使用すると **、[AddItem]** ダイアログ ボックスに表示されるノードをフィルター処理できます。 子プロジェクトに **[AddItem]** ダイアログ ボックスが表示されると、`IVsFilterAddProjectItemDlg`親は、子プロジェクトに表示されるインターフェイスとフィルタ項目を実装できます。

 プロジェクトが特定の親プロジェクトの下で関数別にグループ化されている`IVsFilterAddProjectItemDlg`場合、ユーザーが入れ子になったプロジェクトのショートカット メニューで **[プロジェクト項目の追加]** を選択したときに実装できます。 その`IvsFilterAddProjectItemDlg displays`グループに固有のプロジェクト項目またはファイルのみを実装します。 他のグループのプロジェクト項目は、同じディレクトリに保存されている場合でも、ダイアログ ボックスから除外されます。

 ユーザーが子の**AddItem**ダイアログ ボックスを開くと、親プロジェクトのインターフェイスの実装`IVsFilterAddProjectItemDlg`が呼び出されます。

 インターフェイス`IVsFilterAddProjectItemDlg`は、カテゴリ別のフィルター処理を実装することもできます。 詳細については、「 [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)」および「[プロジェクトテンプレートと項目テンプレートを登録](../../extensibility/internals/registering-project-and-item-templates.md)する 」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [プロジェクトのネスト](../../extensibility/internals/nesting-projects.md)
