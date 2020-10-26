---
title: IDebugGenericFieldDefinition |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldDefinition interface
ms.assetid: b5a853b7-221e-4d62-8948-07423089d75d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 224b9a5c0e2412b9ae89c1767348b8fbd1a528be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180866"
---
# <a name="idebuggenericfielddefinition"></a>IDebugGenericFieldDefinition
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

マネージコードのジェネリック型のフィールドの定義を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugGenericFieldDefinition : IUnknown  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[ConstructInstantiation](../../../extensibility/debugger/reference/idebuggenericfielddefinition-constructinstantiation.md)|型引数の配列を指定して、フィールドインスタンスを構築します。|  
|[GetFormalTypeParams](../../../extensibility/debugger/reference/idebuggenericfielddefinition-getformaltypeparams.md)|パラメーターの数を指定して、型パラメーターを取得します。|  
|[TypeParamCount](../../../extensibility/debugger/reference/idebuggenericfielddefinition-typeparamcount.md)|ジェネリックフィールドに関連付けられている型パラメーターの数を取得します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: Sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
