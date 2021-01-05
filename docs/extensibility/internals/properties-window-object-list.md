---
title: プロパティウィンドウオブジェクトリスト |Microsoft Docs
description: Visual Studio IDE のプロパティウィンドウのオブジェクトリストとの対話に使用するインターフェイスについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 92fcce4dc62cdc84d15ca6dc51420791d4460340
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875428"
---
# <a name="properties-window-object-list"></a>プロパティ ウィンドウのオブジェクト一覧
[ **プロパティ** ] ウィンドウの [オブジェクト] ボックスの一覧では、選択範囲を、選択した1つまたは複数のウィンドウ内で使用可能な他のオブジェクトに変更できます。 この一覧内から別のオブジェクトを選択すると、への呼び出しがトリガーされ <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 、新しいオブジェクトが選択されたことが環境に通知されます。 次に、[ **プロパティ** ] ウィンドウに表示される情報が変更され、新しく選択されたオブジェクトに関連付けられたプロパティが表示されます。

## <a name="the-object-list"></a>オブジェクトの一覧
 オブジェクトの一覧は、オブジェクト名 (太字で表示) とオブジェクトの種類の2つのフィールドで構成されています。

 オブジェクトの種類の左側に太字で表示されているオブジェクト名は、インターフェイスによって提供されるプロパティを使用して、オブジェクト自体から取得され `Name` <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> ます。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>では、の唯一のメソッドは、 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> そのインターフェイスのコクラスに対してを返します。 [ **プロパティ** ] ウィンドウでは、を使用して <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> コクラスの名前を取得します。これは、ドロップダウンリストにオブジェクト名として表示されます。

 オブジェクトにプロパティがない場合は、 `Name` オブジェクトリストの名前領域に名前が表示されません。 オブジェクトの一覧に名前が表示されるようにするには、オブジェクトに Name プロパティを追加します。

 COM オブジェクトがを実装していない場合、[ <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> **プロパティ** ] ウィンドウには、一覧の左側のオブジェクト名の代わりにインターフェイス名が表示されます。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
