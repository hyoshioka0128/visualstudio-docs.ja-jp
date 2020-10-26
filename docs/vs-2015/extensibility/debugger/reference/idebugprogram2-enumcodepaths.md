---
title: 'IDebugProgram2:: EnumCodePaths |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e4d34b1b6519407e02d4340a5108ef03cece12b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202768"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ソースファイル内の指定された位置のコードパスの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumCodePaths(   
   LPCOLESTR            pszHint,  
   IDebugCodeContext2*  pStart,  
   IDebugStackFrame2*   pFrame,  
   BOOL                 fSource,  
   IEnumCodePaths2**    ppEnum,  
   IDebugCodeContext2** ppSafety  
);  
```  
  
```csharp  
int EnumCodePaths(   
   string                 pszHint,  
   IDebugCodeContext2     pStart,  
   IDebugStackFrame2      pFrame,  
   Int                    fSource,  
   out IEnumCodePaths2    ppEnum,  
   out IDebugCodeContext2 ppSafety  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszHint`  
 からIDE の [ **ソース** ] ビューまたは [ **逆アセンブル** ] ビューで、カーソルの下にある単語。  
  
 `pStart`  
 から現在のコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。  
  
 `pFrame`  
 から現在のブレークポイントに関連付けられているスタックフレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。  
  
 `fSource`  
 から`TRUE`**ソース**ビューの場合は0以外 () `FALSE` 。**逆アセンブル**ビューの場合は 0 ()。  
  
 `ppEnum`  
 入出力コードパスのリストを格納している [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) オブジェクトを返します。  
  
 `ppSafety`  
 入出力選択したコードパスがスキップされた場合にブレークポイントとして設定される追加のコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクトを返します。 これは、たとえば、サーキットのブール式の場合に発生する可能性があります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 コードパスは、プログラムの実行中に現在のポイントにアクセスするために呼び出されたメソッドまたは関数の名前を記述します。 コードパスの一覧は、呼び出し履歴を表します。  
  
## <a name="see-also"></a>参照  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
