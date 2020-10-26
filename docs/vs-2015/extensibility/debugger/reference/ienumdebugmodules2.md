---
title: IEnumDebugModules2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f66587f462e1bbfb60704c5c75dc2299cb9ce36
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160981"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、モジュールの一覧を列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IEnumDebugModules2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、プログラム用に読み込まれたモジュールの一覧を表すために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 Visual Studio は、このインターフェイスを取得するために [Enummodules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) を呼び出します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IEnumDebugModules2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|列挙シーケンス内の指定された数のモジュールを取得します。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|列挙シーケンス内の指定された数のモジュールをスキップします。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|モジュールの数を取得します。|  
  
## <a name="remarks"></a>注釈  
 Visual Studio では、主にこのインターフェイスを使用して [ **モジュール** ] ウィンドウを更新します。  
  
 Visual Studio でのデバッグのために、プログラムはモジュールの境界を越えることができるコード命令の論理的なシーケンスです。そのため、単一の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのモジュールの一覧が必要になります。 リスト内の最初のモジュールには、通常、関連付けられているプログラムの最初のエントリポイントが含まれています。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
