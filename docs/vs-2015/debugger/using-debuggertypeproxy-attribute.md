---
title: デバッガーを使用して Typeproxy 属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerTypeProxyAttribute class
- DebuggerTypeProxy attribute
ms.assetid: 943f3bb1-993e-4800-a47e-0af78b063014
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f6e349dd5bea4e0d89c31864960a5438d1e2b13f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684070"
---
# <a name="using-debuggertypeproxy-attribute"></a>DebuggerTypeProxy 属性の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッガーの Typeproxyattribute] (assetId: qualifyHint =&False の場合は autoUpgrade = True) プロキシ (またはスタンドイン) を型に対して指定し、デバッガーウィンドウでの型の表示方法を変更します。 プロキシを指定した変数を表示すると、元の型の代理としてプロキシが**表示**されます。 デバッガーの変数ウィンドウには、プロキシ型のパブリック メンバーのみが表示されます。 プライベート メンバーは表示されません。  
  
 この属性は次の対象に適用できます。  
  
- 構造体  
  
- クラス  
  
- アセンブリ  
  
  型プロキシ クラスには、プロキシで置換される型の引数を使用するコンストラクターが必要です。 デバッガーでは、対象となる型の変数を表示するときに、毎回、新しい型プロキシ クラスのインスタンスが作成されます。 その結果、パフォーマンスが低下する可能性があります。 そのため、コンストラクターでの作業は必要最小限に抑えます。  
  
  パフォーマンスの低下を最小限にするために、式エバリュエーターでは、型の表示プロキシに関する属性はチェックされません。ただし、デバッガー ウィンドウで + 記号をクリックして型を展開したときや、<xref:System.Diagnostics.DebuggerBrowsableAttribute> を使用するときはチェックされます。 そのため、表示型に属性を指定するのは避けます。 属性は、表示型の本体で使用できるようにします。  
  
  型プロキシは、属性の対象となるクラスに入れ子にした、プライベート クラスにすることをお勧めします。 こうすることで、内部のメンバーに簡単にアクセスできます。  
  
  <xref:System.Diagnostics.DebuggerTypeProxyAttribute> をアセンブリ レベルで使用する場合は、プロキシに置換される型を `Target` パラメーターで指定します。  
  
  <xref:System.Diagnostics.DebuggerDisplayAttribute> および <xref:System.Diagnostics.DebuggerTypeProxyAttribute> と共にこの属性を使用する方法の例については、[DebuggerDisplay 属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)に関する記事を参照してください。  
  
## <a name="using-generics-with-debuggertypeproxy"></a>ジェネリックと DebuggerTypeProxy の使用  
 ジェネリックのサポートは限定的です。 C# では、`DebuggerTypeProxy` はオープン型のみをサポートします。 オープン型 (構築されていない型とも呼ばれます) とは、その型パラメーターの引数によってインスタンス化されていないジェネリック型のことです。 クローズ型 (構築された型とも呼ばれます) は、サポートされていません。  
  
 オープン型の構文は次のようになります。  
  
 `Namespace.TypeName<,>`  
  
 `DebuggerTypeProxy` 内でジェネリック型を対象として使用する場合は、この構文を使用する必要があります。 `DebuggerTypeProxy` の機構は、型パラメーターを推論します。  
  
 C# のオープン型とクローズ型の詳細については、[C# 言語仕様](https://msdn.microsoft.com/library/e5d5a5cc-636b-4bff-b9c8-a8edc6207c22)の「セクション 20.5.2 オープン型とクローズ型」を参照してください。  
  
 Visual Basic にはクローズ型の構文はないため、Visual Basic で同じ処理はできません。 代わりに、オープン型の名前の文字列形式を使用する必要があります。  
  
 `"Namespace.TypeName'2"`  
  
## <a name="see-also"></a>参照  
 [デバッガーの表示属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)   
  [デバッガー表示属性によるデバッグ機能の拡張](https://msdn.microsoft.com/library/72bb7aa9-459b-42c4-9163-9312fab4c410)
