---
title: 管理オブジェクトのカスタムビューを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.data.elements
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- data types [C#], custom
- custom data types
- managed code, custom data types
- autoexp.dat file
- mcee_cs.dat file
- debugger, expanding data types
- mcee_mc.dat file
ms.assetid: 9969e9b2-9008-4729-8a14-0d6deaa61576
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb5b56404c7ddc99b7999b47cf3c2a899f915efd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72578027"
---
# <a name="create-custom-views-of-managed-objects"></a>マネージド オブジェクトのカスタム ビューを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio でデバッガーの変数ウィンドウにデータ型を表示する方法をカスタマイズできます。  
  
## <a name="attributes"></a>属性  
 C# および Visual Basic では、<xref:System.Diagnostics.DebuggerTypeProxyAttribute>、<xref:System.Diagnostics.DebuggerDisplayAttribute>、および <xref:System.Diagnostics.DebuggerBrowsableAttribute> を使用して、カスタム データの展開を追加できます。  
  
 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] コードでは、Visual Basic は DebuggerBrowsable 属性をサポートしません。 この制限は、.NET Framework の新しいバージョンで解除されています。  
  
## <a name="visualizers"></a>ビジュアライザー  
 マネージド データ型を表示するには、ビジュアライザーを記述します。 詳細については、[ビジュアライザーを記述する](../debugger/how-to-write-a-visualizer.md)  
  
## <a name="native-code"></a>ネイティブ コード  
 ネイティブ コードの場合、カスタム データ型の展開を autoexp.dat ファイルに追加します。autoexp.dat は、Program Files\Microsoft Visual Studio 11.0\Common7\Packages\Debugger ディレクトリにあります。 `autoexp` 規則の記述手順は、このファイルに含まれています。  
  
> [!CAUTION]
> このファイルの構造と自動展開規則の構文は、Visual Studio のリリースごとに異なる可能性があります。  
  
 また、ネイティブ型の表示は、式エバリュエーター アドインを記述してカスタマイズできます。 詳細については、「 [Eeaddin サンプル: デバッグ式エバリュエーターアドイン](https://msdn.microsoft.com/d4f6b068-c812-45bc-9ec0-7e0363c4bb9e)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [デバッガ Typeproxy 属性の使用](../debugger/using-debuggertypeproxy-attribute.md)   
 [デバッガーの表示属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)   
 [ウォッチウィンドウとクイックウォッチウィンドウ](../debugger/watch-and-quickwatch-windows.md)   
 [デバッガー表示属性によるデバッグ機能の拡張](https://msdn.microsoft.com/library/72bb7aa9-459b-42c4-9163-9312fab4c410)
