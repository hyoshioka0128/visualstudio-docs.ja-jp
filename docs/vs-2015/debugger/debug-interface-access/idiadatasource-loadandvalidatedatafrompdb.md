---
title: 'IDiaDataSource:: loadAndValidateDataFromPdb |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f19a910af45ed70ae74c72441890ecae6c81d2a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198629"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プログラムデータベース (.pdb) ファイルが、指定された署名情報と一致することを確認し、デバッグデータソースとして .pdb ファイルを準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT loadAndValidateDataFromPdb (   
   LPCOLESTR pdbPath,  
   GUID*     pcsig70,  
   DWORD     sig,  
   DWORD     age  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdbPath`  
 から.Pdb ファイルへのパス。  
  
 `pcsig70`  
 から.Pdb ファイルの署名に対して検証する GUID 署名。 以降の .pdb ファイルだけに [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] GUID シグネチャがあります。  
  
 `sig`  
 から.Pdb ファイルの署名に対して検証する32ビット署名。  
  
 `age`  
 から確認する有効期間の値。 Age は必ずしも既知の時刻値に対応しているわけではありません。 .pdb ファイルが対応する .exe ファイルと同期していないかどうかを判断するために使用されます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、このメソッドで使用できる戻り値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_PDB_NOT_FOUND|ファイルを開くことができませんでした。または、ファイルの形式が無効です。|  
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|  
|E_PDB_INVALID_SIG|署名が一致しません。|  
|E_PDB_INVALID_AGE|年齢が一致しません。|  
|E_INVALIDARG|無効なパラメーター。|  
|E_UNEXPECTED|データソースは既に準備されています。|  
  
## <a name="remarks"></a>注釈  
 .Pdb ファイルには、署名と有効期間の両方の値が含まれています。 これらの値は、.pdb ファイルまたは .pdb ファイルに一致する .exe ファイルまたは .dll ファイルにレプリケートされます。 このメソッドは、データソースを準備する前に、指定した .pdb ファイルの署名と有効期間が指定された値と一致することを確認します。  
  
 検証せずに .pdb ファイルを読み込むには、 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。  
  
 (コールバックメカニズムを使用して) データ読み込みプロセスにアクセスするには、 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用します。  
  
 メモリから .pdb ファイルを直接読み込むには、 [IDiaDataSource:: loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) メソッドを使用します。  
  
## <a name="example"></a>例  
  
```cpp#  
IDiaDataSource* pSource;  // Previously created data source.  
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);  
DWORD expectedFileSignature = 0x12345678;  
DWORD expectedAge           = 128;  
  
HRESULT hr;  
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",  
                                          &expectedGUIDSignature,  
                                          expectedFileSignature,  
                                          expectedAge);  
if (FAILED(hr))  
{  
    // Report an error  
}  
  
```  
  
## <a name="see-also"></a>参照  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
