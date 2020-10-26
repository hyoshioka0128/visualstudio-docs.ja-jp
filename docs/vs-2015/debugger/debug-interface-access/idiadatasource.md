---
title: IDiaDataSource |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource interface
ms.assetid: 6260ac76-4f9d-4144-ba22-32f8620b32c2
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a02eb9048c0e9338e6300fc63666af4db535b3ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198587"
---
# <a name="idiadatasource"></a>IDiaDataSource
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグシンボルのソースへのアクセスを開始します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDiaDataSource : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDiaDataSource` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDiaDataSource::get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md)|前回の読み込みエラーのファイル名を取得します。|  
|[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)|プログラムデータベース (.pdb) ファイルをデバッグデータソースとして開き、準備します。|  
|[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)|プログラムデータベース (.pdb) ファイルが、指定された署名情報と一致することを開き、確認します。.pdb ファイルをデバッグデータソースとして準備します。|  
|[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)|を開き、.exe/.dll ファイルに関連付けられているデバッグデータを準備します。|  
|[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)|メモリ内データストリームを介してアクセスされるプログラムデータベース (.pdb) ファイルに格納されているデバッグデータを準備します。|  
|[IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)|シンボルに対してクエリを実行するためのセッションを開きます。|  
  
## <a name="remarks"></a>注釈  
 インターフェイスの load メソッドの1つを呼び出すと、 `IDiaDataSource` シンボルソースが開きます。 [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)メソッドの呼び出しが成功すると、データソースのクエリをサポートする[IDiaSession](../../debugger/debug-interface-access/idiasession.md)インターフェイスが返されます。 Load メソッドがファイルに関連するエラーを返す場合、 [IDiaDataSource:: get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md) メソッドの戻り値には、エラーに関連付けられているファイル名が含まれます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスは、 `CoCreateInstance` クラス識別子とのインターフェイス ID を使用して関数を呼び出すことによって取得され `CLSID_DiaSource` `IID_IDiaDataSource` ます。 この例は、このインターフェイスを取得する方法を示しています。  
  
## <a name="example"></a>例  
  
```cpp#  
  
      IDiaDataSource* pSource;  
HRESULT hr = CoCreateInstance(CLSID_DiaSource,  
                              NULL,  
                              CLSCTX_INPROC_SERVER,  
                              IID_IDiaDataSource,  
                              (void**) &pSource);  
if (FAILED(hr))  
{  
    // Report error and exit  
}  
```  
  
## <a name="requirements"></a>要件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
