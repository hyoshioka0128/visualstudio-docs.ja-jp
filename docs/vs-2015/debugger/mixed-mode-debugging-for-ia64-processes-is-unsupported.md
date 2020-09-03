---
title: IA64 プロセスの混合モードのデバッグはサポートされていません。 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 20bc1e38-049b-4388-87c4-936815d85b46
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c3cf7308b3302c682f32a2db9837f86cd0173260
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203285"
---
# <a name="mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>IA64 プロセスの混合モードのデバッグはサポートされていません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、IA64 プロセスでマネージド コードとネイティブ コードの混合モードのデバッグはサポートされていません。 つまり、デバッグ中にマネージド コードからネイティブ コードにステップ インすることや、ネイティブ コードからマネージド コードにステップ インすることはできません。  
  
### <a name="workarounds"></a>問題回避  
  
- マネージド コードとネイティブ コードを個別のデバッガー セッション内でデバッグする。  
  
     \- または -  
  
     次の手順に示すように、混合コードを 32 ビット プロセスとしてデバッグする。  
  
### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>プラットフォームを 32 ビットに変更するには (Visual Basic または C#)  
  
1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
2. プロパティ ページで、 **[コンパイル]** タブまたは **[デバッグ]** タブをクリックします。  
  
3. **[プラットフォーム]** をクリックし、プラットフォームの一覧から [x86] を選択します。  
  
     Visual Basic コンパイラおよび C# コンパイラの既定では、どの CPU 上でも実行されるコードが生成されます。 64 ビット コンピューター上では、これらのバイナリは 64 ビット プロセスとして実行されます。 32 ビット プロセスとして実行するには、 **[Any CPU]** でなく **[Win32]** を選択する必要があります。  
  
### <a name="to-change-the-platform-to-32-bit-cc"></a>プラットフォームを 32 ビットに変更するには (C/C++)  
  
1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
2. プロパティ ページで **[プラットフォーム]** をクリックし、プラットフォームの一覧の [Win32] をクリックします。  
  
## <a name="see-also"></a>参照  
 [64 ビット アプリケーションをデバッグする](../debugger/debug-64-bit-applications.md)
