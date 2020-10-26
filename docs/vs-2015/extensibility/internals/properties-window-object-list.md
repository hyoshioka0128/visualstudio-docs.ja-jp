---
title: プロパティウィンドウオブジェクトリスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 95ef509491e05daf575e211ae479c815994eb3d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148332"
---
# <a name="properties-window-object-list"></a>プロパティ ウィンドウのオブジェクト一覧
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[ **プロパティ** ] ウィンドウの [オブジェクト] ボックスの一覧では、選択範囲を、選択した1つまたは複数のウィンドウ内で使用可能な他のオブジェクトに変更できます。 この一覧内から別のオブジェクトを選択すると、への呼び出しがトリガーされ <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 、新しいオブジェクトが選択されたことが環境に通知されます。 次に、[ **プロパティ** ] ウィンドウに表示される情報が変更され、新しく選択されたオブジェクトに関連付けられたプロパティが表示されます。  
  
## <a name="the-object-list"></a>オブジェクトの一覧  
 オブジェクトの一覧は、オブジェクト名 (太字で表示) とオブジェクトの種類の2つのフィールドで構成されています。  
  
 オブジェクトの種類の左側に太字で表示されているオブジェクト名は、インターフェイスによって提供されるプロパティを使用して、オブジェクト自体から取得され `Name` <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> ます。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>では、の唯一のメソッドは、 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> そのインターフェイスのコクラスに対してを返します。 [ **プロパティ** ] ウィンドウでは、を使用して <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> コクラスの名前を取得します。これは、ドロップダウンリストにオブジェクト名として表示されます。  
  
 オブジェクトにプロパティがない場合は、 `Name` オブジェクトリストの名前領域に名前が表示されません。 オブジェクトの一覧に名前が表示されるようにするには、オブジェクトに Name プロパティを追加します。  
  
 COM オブジェクトがを実装していない場合、[ <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> **プロパティ** ] ウィンドウには、一覧の左側のオブジェクト名の代わりにインターフェイス名が表示されます。  
  
## <a name="see-also"></a>参照  
 [プロパティの拡張](../../extensibility/internals/extending-properties.md)
