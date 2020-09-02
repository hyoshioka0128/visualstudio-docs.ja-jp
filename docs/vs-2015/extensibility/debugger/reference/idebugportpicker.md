---
title: IDebugPortPicker |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f3e030facd8c70aec4fdc480b01c90ee4c0acda7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188391"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ポートを選択するためのカスタマイズされた UI を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugPortPicker : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 このインターフェイスは、ポートサプライヤーによって実装されます。 ポートサプライヤーは、ポートピッカーを CLSID として公開し、公開された CLSID でメトリックをポイントすることによって、そのポートの選択を定義し `metricPortPickerCLSID` ます。  
  
## <a name="methods"></a>メソッド  
 次の表に、のメソッドを示し `IDebugPortPicker` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|指定されたダイアログボックスを表示し、ユーザーがポートを選択できるようにします。|  
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|サービスプロバイダーを設定します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
