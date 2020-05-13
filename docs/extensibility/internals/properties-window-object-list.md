---
title: プロパティ ウィンドウ オブジェクト リスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ffe11ae6ebb4e692686c884b663a4f93d1466535
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706151"
---
# <a name="properties-window-object-list"></a>プロパティ ウィンドウのオブジェクト一覧
**[プロパティ]** ウィンドウのオブジェクト リストはドロップダウン リストで、選択したオブジェクトを 1 つまたは複数の選択ウィンドウ内で使用可能な他のオブジェクトに変更できます。 このリストから別のオブジェクトを選択すると、新しい<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A>オブジェクトが選択されたことを環境に通知する呼び出しがトリガーされます。 次に **、[プロパティ]** ウィンドウに表示される情報が変更され、新しく選択したオブジェクトに関連付けられているプロパティが表示されます。

## <a name="the-object-list"></a>オブジェクトリスト
 オブジェクトリストは、オブジェクト名(太字で表示)とオブジェクトタイプの2つのフィールドで構成されています。

 オブジェクト型の左側に太字で表示されるオブジェクト名は、インターフェイスによって提供されるプロパティを`Name`使用してオブジェクト自体から取得されます<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>の唯一のメソッド<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>は、<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>そのインターフェイスのコクラスに対して返されます。 **[プロパティ]** <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>ウィンドウでは、コクラスの名前を取得します。

 オブジェクトに`Name`プロパティがない場合、オブジェクト リストの [名前] 領域に名前は表示されません。 オブジェクトリストに名前を表示する場合は、Name プロパティをオブジェクトに追加できます。

 COM オブジェクトが実装<xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>されていない場合は、**プロパティ**ウィンドウの左側のオブジェクト名の代わりにインターフェイス名が表示されます。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
