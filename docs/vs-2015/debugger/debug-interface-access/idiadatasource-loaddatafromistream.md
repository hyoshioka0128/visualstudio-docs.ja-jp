---
title: 'IDiaDataSource:: loadDataFromIStream |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromIStream method
ms.assetid: 8fe33eea-1457-4b8c-ae19-f1ede5578483
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 35644f06ae929e4168d5dc44d6fc488de020a637
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547456"
---
# <a name="idiadatasourceloaddatafromistream"></a>IDiaDataSource::loadDataFromIStream
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

メモリ内データストリームを介してアクセスされるプログラムデータベース (.pdb) ファイルに格納されているデバッグデータを準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT loadDataFromIStream (   
   IStream* pIStream  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pIStream  
 から <xref:IStream> 使用するデータストリームを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、このメソッドで使用できる戻り値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|  
|E_INVALIDARG|無効なパラメーター。|  
|E_UNEXPECTED|データソースは既に準備されています。|  
  
## <a name="remarks"></a>注釈  
 このメソッドを使用すると、実行可能ファイルのデバッグデータをオブジェクトを介してメモリから取得でき <xref:IStream> ます。  
  
 検証せずに .pdb ファイルを読み込むには、 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。  
  
 特定の条件に対して .pdb ファイルを検証するには、 [IDiaDataSource:: loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) メソッドを使用します。  
  
 (コールバックメカニズムを使用して) データ読み込みプロセスにアクセスするには、 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用します。  
  
## <a name="see-also"></a>参照  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)   
 [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)   
 [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
