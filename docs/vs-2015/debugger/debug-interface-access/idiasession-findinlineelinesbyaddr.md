---
title: 'IDiaSession:: findInlineeLinesByAddr |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: bb70e408-eed1-4c9c-b5b1-44323125f48b
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2b35850367ef4bcc4e49cc3d6e76b41a2e9f4cd7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151697"
---
# <a name="idiasessionfindinlineelinesbyaddr"></a>IDiaSession::findInlineeLinesByAddr
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

クライアントが、指定された親シンボルによって直接または間接的にインライン化されているすべての関数の行番号情報を反復処理できるようにする列挙体を取得します。指定したアドレス範囲内に含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findInlineeLinesByAddr (   
   IDiaSymbol*           parent,   DWORD                 isect,   DWORD                 offset,   DWORD                 length,  
   IDiaEnumLineNumbers** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `parent`  
 から `IDiaSymbol` 親を表すオブジェクトです。  
  
 `isect`  
 からアドレスのセクション部分を指定します。  
  
 `offset`  
 からアドレスのオフセットコンポーネントを指定します。  
  
 `length`  
 からこのクエリでカバーするアドレス範囲をバイト数で指定します。  
  
 `ppResult`  
 入出力 `IDiaEnumLineNumbers` 取得された行番号の一覧を含むオブジェクトを保持します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
