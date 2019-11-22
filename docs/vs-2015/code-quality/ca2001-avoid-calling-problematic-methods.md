---
title: 'CA2001: Avoid calling problematic methods | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2001
- AvoidCallingProblematicMethods
helpviewer_keywords:
- CA2001
- AvoidCallingProblematicMethods
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 287f83d23db75206183fb1ee1461e461a05a6182
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298483"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001: 問題が発生する可能性のあるメソッドは呼び出しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メンバーが危険性または問題のあるメソッドを呼び出します。

## <a name="rule-description"></a>規則の説明
 Avoid making unnecessary and potentially dangerous method calls.

 A violation of this rule occurs when a member calls one of the following methods.

|メソッド|説明|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|Calling GC.Collect can significantly affect application performance and is rarely necessary. For more information, see the [Rico Mariani's Performance Tidbits](https://go.microsoft.com/fwlink/?LinkId=169256) blog entry on MSDN.|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|Thread.Suspend and Thread.Resume have been deprecated because of their unpredictable behavior.  Use other classes in the <xref:System.Threading> namespace, such as <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex>, and <xref:System.Threading.Semaphore> to synchronize threads or protect resources.|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|The DangerousGetHandle method poses a security risk because it can return a handle that is not valid. See the <xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A> and the <xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A> methods for more information about how to use the DangerousGetHandle method safely.|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|These methods can load assemblies from unexpected locations. For example, see Suzanne Cook's .NET CLR Notes blog posts [LoadFile vs. LoadFrom](https://go.microsoft.com/fwlink/?LinkId=164450) and [Choosing a Binding Context](https://go.microsoft.com/fwlink/?LinkId=164451) on the MSDN Web site for information about methods that load assemblies.|
|[CoSetProxyBlanket](https://go.microsoft.com/fwlink/?LinkID=169250) (Ole32)<br /><br /> [CoInitializeSecurity](https://go.microsoft.com/fwlink/?LinkId=169255) (Ole32)|By the time the user code starts executing in a managed process, it is too late to reliably call CoSetProxyBlanket. The common language runtime (CLR) takes initialization actions that may prevent the users P/Invoke from succeeding.<br /><br /> If you do have to call CoSetProxyBlanket for a managed application, we recommend that you start the process by using a native code (C++) executable, call CoSetProxyBlanket in the native code, and then start your managed code application in process. (Be sure to specify a runtime version number.)|

## <a name="how-to-fix-violations"></a>違反の修正方法
 To fix a violation of this rule, remove or replace the call to the dangerous or problematic method.

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 You should suppress messages from this rule only when no alternatives to the problematic method are available.

## <a name="see-also"></a>参照
 [信頼性の警告](../code-quality/reliability-warnings.md)
