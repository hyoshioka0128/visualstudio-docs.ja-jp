---
title: 'IDiaDataSource:: openSession |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::openSession method
ms.assetid: a3319ed0-3979-483b-9852-c0af96852c48
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4bec5507d15374e6e88afd4567d4b0fec9ca6cb7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198599"
---
# <a name="idiadatasourceopensession"></a>IDiaDataSource::openSession
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルに対してクエリを実行するためのセッションを開きます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT openSession (   
   IDiaSession** ppSession  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 ppSession  
 入出力開いているセッションを表す [IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 次の表に、このメソッドで使用できる戻り値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|E_UNEXPECTED|[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)オブジェクトは、以前はシンボルのソースで初期化されていません。|  
|E_INVALIDARG|無効な `ppSession` パラメーター。|  
|E_OUTOFMEMORY|セッションを開くためのメモリが不足しています。|  
  
## <a name="remarks"></a>注釈  
 このメソッドは、データソースの [IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを開きます。  
  
 `IDiaSession` オブジェクトは、データソースへのクエリを実装します。 セッションは、デバッグシンボルのセットごとに1つのアドレス空間を管理します。 データソースシンボルによって記述されている .exe ファイルまたは .dll ファイルが複数のアドレス範囲でアクティブになっている場合 (複数のプロセスが読み込まれている場合など)、各アドレス範囲に対して1つのセッションを使用する必要があります。  
  
## <a name="example"></a>例  
  
```cpp#  
IDiaSession* pSession;  
HRESULT hr = pSource->openSession( &pSession );  
if (FAILED(hr))  
{  
   // report error  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
