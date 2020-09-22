---
title: 'IDiaSession:: findLinesByLinenum |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByLinenum method
ms.assetid: 76d5622d-9a91-4c2a-a98f-263af5d1daef
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d7ef4ab516bffbc13f47616c2f20fdd71cac38b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841776"
---
# <a name="idiasessionfindlinesbylinenum"></a>IDiaSession::findLinesByLinenum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソースファイル内の指定した行番号が含まれているコンパイル単位の行番号を確認します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findLinesByLinenum (   
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
 入出力取得された行番号の一覧を含む [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) objta を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="example"></a>例  
 次の例では、ソースファイルを開き、このファイルによって提供される compilands を列挙し、各コンパイル単位が開始されるソースファイル内の行番号を検索する方法を示します。  
  
```cpp#  
void ShowLinesInCompilands(IDiaSession *pSession, LPCOLESTR filename)  
{  
    IDiaEnumSourceFiles* pEnum;  
    IDiaSourceFile*      pFile;  
    DWORD                celt;  
  
    pSession->findFile ( NULL, filename, nsFNameExt, &pEnum );  
    while ( pEnum->Next ( 1, &pFile, &celt ) == S_OK ) // for each file  
    {  
        IDiaEnumSymbols* pEnumCompilands;  
        IDiaSymbol* pCompiland;  
  
        pFile->get_compilands ( &pEnumCompilands );  
        // for each compiland  
        while ( pEnumCompilands->Next ( 1, &pCompiland, &celt ) == S_OK )  
        {  
            IDiaEnumLineNumbers* pEnum;  
            // Find first compiland closest to line 1 of the file.  
            if (pSession->findLinesByLinenum( pCompiland, pFile, 1, 0, &pEnum ) == S_OK)  
            {  
                IDiaLineNumber *pLineNumber;  
                DWORD lineCount;  
                while ( pEnum->Next(1,&pLineNumber,&lineCount) == S_OK)  
                {  
                     DWORD lineNum;  
                     if (pLineNumber->get_line(&lineNum) == S_OK)  
                     {  
                          printf("compiland starts in source at line number = %lu\n",lineNum);  
                     }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSession:: Find? Byaddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
