---
title: '[デバッグ セッションで実行可能] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.exefordebug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- executable files, specifying when debugging
- DLLs, debugging
- debugger, Executable for Debugging Session dialog box
- Executable for Debugging Session dialog box
ms.assetid: c0ddbe32-b99f-4425-acf1-f48842804f56
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c2ee71c5e23b0c5784cd2fe9b57b46fe28d41d30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157467"
---
# <a name="executable-for-debugging-session-dialog-box"></a>[デバッグ セッションで実行可能] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログ ボックスは、ダイナミック リンク ライブラリ (DLL: Dynamic-Link Library) をデバッグするときに、実行可能ファイルが指定されていない場合に表示されます。 Visual Studio では、DLL を直接起動できません。 代わりに、指定した実行可能ファイルが起動されます。 DLL は、実行可能ファイルから呼び出されたときにデバッグできます。  
  
 **実行可能ファイル名**  
 デバッグ中の DLL を呼び出す実行可能ファイルへのパス名を入力します。  
  
 **プロジェクトにアクセスする URL (ATL Server のみ)**  
 ATL Server の DLL をデバッグする場合は、プロジェクトが存在する URL を入力します。  
  
 URL を入力すると、これらの設定がプロジェクトの [プロパティ ページ] に格納されるため、後続のデバッグ セッションで設定を再入力する必要がなくなります。 設定変更が必要な場合は [プロパティ ページ] を開いて値を変更できます。 デバッグ セッションで実行可能ファイルを指定する方法の詳細については、「[DLL のデバッグ](../debugger/how-to-debug-native-dlls.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
