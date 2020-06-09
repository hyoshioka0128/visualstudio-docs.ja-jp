---
title: C++ プロジェクトでのデバッグ機能の有効化 (-D_DEBUG) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 19d341cba47e0a3d2259cc57d239c63420095347
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737956"
---
# <a name="enabling-debug-features-in-c-projects-d_debug"></a>C++ プロジェクトでのデバッグ機能の有効化 (/D_DEBUG)
[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] では、シンボル **_DEBUG** を定義してプログラムをコンパイルすると、アサーションなどのデバッグ機能が有効になります。 **_DEBUG** は、次のいずれかの方法で定義できます。

- ソース コードで **#define _DEBUG** を指定します。または

- **/D_DEBUG** コンパイラ オプションを指定します。 (ウィザードを使用して Visual Studio のプロジェクトを作成した場合は、デバッグ構成で **/D_DEBUG** が自動的に定義されます。)

  **_DEBUG** を定義すると、コンパイラでは **#ifdef _DEBUG** と `#endif` で囲まれたコードのセクションがコンパイルされます。

  MFC プログラムのデバッグ構成は、MFC ライブラリのデバッグ バージョンとリンクする必要があります。 MFC ヘッダー ファイルによって、 **_DEBUG** や **_UNICODE** など、定義済みのシンボルに基づいて、リンクする MFC ライブラリの適正なバージョンが決定されます。 詳細については、「[MFC ライブラリのバージョン](/cpp/mfc/mfc-library-versions)」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)