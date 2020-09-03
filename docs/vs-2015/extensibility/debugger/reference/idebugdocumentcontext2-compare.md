---
title: 'IDebugDocumentContext2:: Compare |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7f09684c5e9587c6e3bb631674e009d0b36f4fc5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189410"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このドキュメントコンテキストと、指定されたドキュメントコンテキストの配列を比較します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Compare(   
   DOCCONTEXT_COMPARE       compare,  
   IDebugDocumentContext2** rgpDocContextSet,  
   DWORD                    dwDocContextSetLen,  
   DWORD*                   pdwDocContext  
);  
```  
  
```csharp  
int Compare(   
   enum_ DOCCONTEXT_COMPARE compare,  
   IDebugDocumentContext2[] rgpDocContextSet,  
   uint                     dwDocContextSetLen,  
   out uint                 pdwDocContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `compare`  
 から比較の種類を指定する [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md) 列挙の値です。  
  
 `rgpDocContextSet`  
 から比較対象のドキュメントコンテキストを表す [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトの配列。  
  
 `dwDocContextSetLen`  
 から比較するドキュメントコンテキストの配列の長さ。  
  
 `pdwDocContext`  
 入出力 `rgpDocContextSet` 比較を満たす最初のドキュメントコンテキストの配列内のインデックスを返します。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`一致が見つかった場合は、を返します。 一致が見つからなかった `S_FALSE` 場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 配列で渡される [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトは、呼び出されるオブジェクトを実装する同じデバッグエンジンによって実装される必要があります。 `IDebugDocumentContext2` そうでない場合、比較は無効になります。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)
