---
title: 'エラー: 混合モード デバッグ プロセスがサポートされるは、Microsoft .NET Framework 4 を使用している場合にのみ x64 以上 |Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: e4b0216c-7006-4832-883f-08e982ba8d3f
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5dfb5d43ef78e16a5280c7faff92a3ea7e791c43
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805620"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>エラー: x64 プロセスの混合モード デバッグは、Microsoft .NET Framework 4 以上を使用している場合にのみサポートされます
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ネイティブ コードとマネージド コードの混合を 64 プロセスでデバックするには、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Version 4 が必要です。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Version 4 より前のバージョンを使用した 64 ビット プロセスの混合モード デバッグはサポートされません。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   次のいずれかの操作を実行します。  
  
    -   [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] を Version 4 にアップグレードします。  
  
    -   デバッグのため、32 ビット バージョンのアプリケーションをビルドします。  
  
## <a name="see-also"></a>関連項目  
 [デバイスのリモート ツールのセットアップ](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)



