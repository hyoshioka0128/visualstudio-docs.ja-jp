---
title: 'IDiaSession:: findInlineeLinesByLinenum |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d16bc6f3e2e8f190e3a26023407237509984cece
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841728"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したソースファイルと行番号で、直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findInlineeLinesByVA (   
   IDiaSymbol*           compiland,  
   IDiaSourceFile*       file,  
   DWORD                 linenum,  
   DWORD                 column,  
   IDiaEnumLineNumbers** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `compiland`  
 から行番号を検索するコンパイル単位を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。  
  
 `file`  
 から検索するソースファイルを表す [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。  
  
 `linenum`  
 から1から始まる行番号を指定します。  
  
> [!NOTE]
> 0を使用してすべての行を指定することはできません (すべての行を検索するには、 [IDiaSession:: findlines](../../debugger/debug-interface-access/idiasession-findlines.md) メソッドを使用します)。  
  
 `column`  
 から列番号を指定します。 すべての列を指定するには0を使用します。 列は、1行に対するバイトオフセットです。  
  
 `ppResult`  
 入出力取得された行番号の一覧を含む [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
