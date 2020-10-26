---
title: 'IDebugProgramNode2:: GetProgramName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetProgramName
helpviewer_keywords:
- IDebugProgramNode2::GetProgramName
ms.assetid: 510c7f5d-48ff-4d9f-ad79-fbad9f15239d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c46cb55140159bff12d297adbc5c0346ffe0409
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148556"
---
# <a name="idebugprogramnode2getprogramname"></a>IDebugProgramNode2::GetProgramName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プログラムの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetProgramName (   
   BSTR* pbstrProgramName  
);  
```  
  
```csharp  
int GetProgramName (   
   out string pbstrProgramName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrProgramName`  
 入出力プログラムの名前を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 プログラムの名前は、プログラムのパスと同じではありませんが、プログラムの名前はそのようなパスの一部である場合があります。  
  
## <a name="example"></a>例  
 次の例は、IDebugProgramNode2 インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CProgram` います。 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 関数は、 `MakeBstr` 指定された文字列のコピーを BSTR として割り当てます。  
  
```cpp#  
HRESULT CProgram::GetProgramName(BSTR* pbstrProgramName) {    
   if (!pbstrProgramName)    
      return E_INVALIDARG;    
  
   // Assign the member program name to the passed program name.    
   *pbstrProgramName = MakeBstr(m_pszProgramName);    
   return NOERROR;    
}    
```  
  
## <a name="see-also"></a>参照  
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
