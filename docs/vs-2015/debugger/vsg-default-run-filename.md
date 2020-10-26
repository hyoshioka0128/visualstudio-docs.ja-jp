---
title: VSG_DEFAULT_RUN_FILENAME | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ea549d2f-c857-458c-93c7-bc5a2d11d15d
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2980d34028c58a6abadb2df21bf22c8d37cda6e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160760"
---
# <a name="vsg_default_run_filename"></a>VSG_DEFAULT_RUN_FILENAME
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス ログ ファイルの既定のファイル名を定義します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
#define VSG_DEFAULT_FILENAME filename  
```  
  
#### <a name="parameters"></a>パラメーター  
 `filename`  
 グラフィックス情報がプログラムによってキャプチャされたとき、グラフィックス ログ ファイルに既定で与えられるファイル名。  
  
## <a name="value"></a>[値]  
 グラフィックス ログ ファイルのファイル名を表すリテラル文字列。 既定では、L"default.vsglog" です。  
  
```cpp  
#define VSG_DEFAULT_FILENAME L"default.vsglog"  
```  
  
## <a name="remarks"></a>Remarks  
 プリプロセッサ シンボル `DONT_SAVE_VSGLOG_TO_TEMP` が定義されている場合、ファイル名はキャプチャされるアプリケーションの現在のディレクトリに対する相対パスになるか、または絶対パスです。それ以外の場合は、ユーザーの一時ファイル ディレクトリに対する相対パスになり、絶対パスにすることはできません。  
  
 定義されたファイル名を変更するには、プログラムで `vsgcapture.h` を含める前にファイル名を再定義する必要があります。  
  
## <a name="example"></a>例  
 次の例に、キャプチャ ファイルの既定のファイル名を変更する方法を示します。  
  
```cpp  
// Redefine the default capture filename before including vsgcapture.h  
#define VSG_DEFAULT_FILENAME L"capture.vsglog"  
  
#include <vsgcapture.h>  
```  
  
## <a name="see-also"></a>参照  
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)
