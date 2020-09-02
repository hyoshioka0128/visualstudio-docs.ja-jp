---
title: 'IDebugMethodField:: EnumLocals |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2306bbf0c44a883c584346c3dbb3dd70e9b39175
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162608"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

メソッドの選択されたローカル変数の列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumLocals(   
   IDebugAddress*     pAddress,  
   IEnumDebugFields** ppLocals  
);  
```  
  
```csharp  
int EnumLocals(  
   IDebugAddress        pAddress,   
   out IEnumDebugFields ppLocals  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pAddress`  
 からローカルの取得元のコンテキストまたはスコープを選択するデバッグアドレスを表す [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト。  
  
 `ppLocals`  
 入出力ローカルのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。それ以外の場合は、ローカル変数がない場合は null 値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、は S_OK を返します。ローカルがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 指定されたデバッグアドレスを含むブロック内で定義されている変数のみが列挙されます。 コンパイラによって生成されるローカルを含むすべてのローカル変数が必要な場合は、 [Enumalllocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) メソッドを呼び出します。  
  
 メソッドには、複数のスコープコンテキストまたはブロックを含めることができます。 たとえば、次の不自然なメソッドには、2つの内部ブロックとメソッド本体自体の3つのスコープが含まれています。  
  
```csharp  
public void func(int index)  
{  
    // Method body scope  
    int a = 0;  
    if (index == 1)  
    {  
        // Inner scope 1  
        int temp1 = a;  
    }  
    else  
    {  
        // Inner scope 2  
        int temp2 = a;  
    }  
}  
```  
  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)オブジェクトは、 `func` メソッド自体を表します。 `EnumLocals`アドレスに設定された[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)を使用してメソッドを呼び出すと、 `Inner Scope 1` などの変数を含む列挙が返さ `temp1` れます。  
  
## <a name="see-also"></a>参照  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
