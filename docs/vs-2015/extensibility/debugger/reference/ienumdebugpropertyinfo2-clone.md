---
title: 'IEnumDebugPropertyInfo2:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2::Clone
helpviewer_keywords:
- IEnumDebugPropertyInfo2::Clone
ms.assetid: 0ede1667-1071-4aa4-b887-260ea103d724
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 68e60c71b2c1f7298d56b26d4db881afd8f347da
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199581"
---
# <a name="ienumdebugpropertyinfo2clone"></a>IEnumDebugPropertyInfo2::Clone
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

現在の列挙体のコピーを別のオブジェクトとして返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone(  
   IEnumDebugPropertyInfo2** ppEnum  
);  
```  
  
```csharp  
int Clone(  
   out IEnumDebugPropertyInfo2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力この列挙体のコピーを別のオブジェクトとして返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
