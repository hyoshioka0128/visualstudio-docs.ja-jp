---
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bd11e57c8e2ec03da1dcfa9ff76b3b3ec2ded5e9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149303"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

対象のコンピュータに関する情報のクエリを実行できるようにします。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugWindowsComputerPort2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 このインターフェイスは、セッションデバッグマネージャーのポートオブジェクトによって実装されます。  
  
## <a name="methods"></a>メソッド  
 次の表に、のメソッドを示し `IDebugWindowsComputerPort2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|デバッガーが実行されているコンピューターに関する情報を取得します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
