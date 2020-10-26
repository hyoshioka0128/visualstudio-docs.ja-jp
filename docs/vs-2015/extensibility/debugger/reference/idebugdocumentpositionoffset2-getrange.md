---
title: 'IDebugDocumentPositionOffset2:: GetRange |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2::GetRange
ms.assetid: 27da7130-0932-4f97-abde-05e6fb018606
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a028a2c88fe44aa6a117ddb81cff5788eec1732e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200232"
---
# <a name="idebugdocumentpositionoffset2getrange"></a>IDebugDocumentPositionOffset2::GetRange
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

現在のドキュメントの位置の範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetRange(  
   DWORD* pdwBegOffset,  
   DWORD* pdwEndOffset  
);  
```  
  
```csharp  
public int GetRange(  
   ref uint pdwBegOffset,  
   ref uint pdwEndOffset  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwBegOffset`  
 [入力、出力]範囲の開始位置のオフセット。 この情報が不要な場合は、このパラメーターを null 値に設定します。  
  
 `pdwEndOffset`  
 [入力、出力]範囲の終了位置のオフセット。 この情報が不要な場合は、このパラメーターを null 値に設定します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 位置ブレークポイントのドキュメント位置に指定された範囲は、実際にコードを提供するステートメントを検索するために、デバッグエンジン (DE) によって使用されます。 次に例を示します。  
  
```  
Line 5: // comment  
Line 6: x = 1;  
```  
  
 行5は、デバッグ中のプログラムにコードを提供しません。 5行目のブレークポイントを設定するデバッガーが、コードを提供する最初の行の特定の量を前方に検索する場合、デバッガーは、ブレークポイントが正しく配置される可能性のある追加の候補行を含む範囲を指定します。 次に、ブレークポイントを受け取る行が見つかるまで、行を順に検索します。  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)   
 [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
