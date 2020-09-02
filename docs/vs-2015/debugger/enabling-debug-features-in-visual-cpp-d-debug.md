---
title: Visual C++ でのデバッグ機能の有効化 (-D_DEBUG) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- /D_DEBUG compiler option [C++]
- debugging [C++], enabling debug features
- debugging [MFC], enabling debug features
- assertions, enabling debug features
- D_DEBUG compiler option
- MFC libraries, debug version
- debug builds, MFC
- _DEBUG macro
ms.assetid: 276e2254-7274-435e-ba4d-67fcef4f33bc
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cffa8592c2048c6c6b39eee5c4ca654c41448933
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686703"
---
# <a name="enabling-debug-features-in-visual-c-d_debug"></a>Visual C++ でのデバッグ機能の使用 (/D_DEBUG)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vcprvc](../includes/vcprvc-md.md)] では、シンボル **_DEBUG** を定義してプログラムをコンパイルすると、アサーションなどのデバッグ機能が有効になります。 **_DEBUG** は、次のいずれかの方法で定義できます。  
  
- ソース コードで **#define _DEBUG** を指定します。または  
  
- **/D_DEBUG** コンパイラ オプションを指定します。 (ウィザードを使用して Visual Studio のプロジェクトを作成した場合は、デバッグ構成で **/D_DEBUG** が自動的に定義されます。)  
  
  **_DEBUG** を定義すると、コンパイラでは **#ifdef _DEBUG** と `#endif` で囲まれたコードのセクションがコンパイルされます。  
  
  MFC プログラムのデバッグ構成は、MFC ライブラリのデバッグ バージョンとリンクする必要があります。 MFC ヘッダー ファイルによって、 **_DEBUG** や **_UNICODE** など、定義済みのシンボルに基づいて、リンクする MFC ライブラリの適正なバージョンが決定されます。 詳細については、「[MFC ライブラリのバージョン](https://msdn.microsoft.com/library/3d7a8ae1-e276-4cf8-ba63-360c2f85ad0e)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ネイティブコードのデバッグ](../debugger/debugging-native-code.md)   
 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
