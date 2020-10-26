---
title: 'IEEDataStorage:: GetData |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a58f644a71601b16317c4fe63271f4f816da77d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149292"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オブジェクトから指定されたバイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetData(  
   ULONG  dataSize,  
   ULONG* sizeGotten,  
   BYTE*  data  
);  
```  
  
```csharp  
int GetData(  
   uint     dataSize,  
   out uint sizeGotten,  
   byte[]   data  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dataSize`  
 から取得するバイト数。配列は、 `data` 少なくともこのバイト数を保持する必要があります。  
  
 `sizeGotten`  
 入出力実際に取得されたバイト数を返します。  
  
 `data`  
 [入力、出力]要求されたデータを格納する配列。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、取得プロセスでバイトをスキップする方法がないため、すべてのデータバイトをローカル配列に取得することをお勧めします。 この場合、パラメーターは `dataSize` [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) メソッドによって返される値である必要があります。  
  
## <a name="see-also"></a>参照  
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)   
 [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
