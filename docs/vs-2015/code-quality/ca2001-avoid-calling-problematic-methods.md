---
title: 'CA2001: 問題のあるメソッドを呼び出さないでください。Microsoft Docs'
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
ms.openlocfilehash: 318b7b8adddd674a9b8ecb93441d69a76ab574dd
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586780"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001:問題が発生する可能性のあるメソッドは呼び出しません
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
 不要で危険性のあるメソッド呼び出しを行わないようにします。

 この規則違反は、メンバーが次のいずれかのメソッドを呼び出した場合に発生します。

|Method|説明|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|GC を呼び出しています。Collect はアプリケーションのパフォーマンスに大きな影響を与える可能性があり、ほとんど必要ありません。 詳細については、MSDN の[プエルトリコ Mariani の Performance ちょっとの](https://docs.microsoft.com/archive/blogs/ricom/when-to-call-gc-collect)ブログエントリを参照してください。|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|予期しない動作が原因で、スレッドの中断と再開が非推奨とされました。  、 <xref:System.Threading> <xref:System.Threading.Mutex>、などの名前空間の他の<xref:System.Threading.Monitor>クラスを使用<xref:System.Threading.Semaphore>して、スレッドを同期したりリソースを保護したりします。|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|Safehandle.dangerousgethandle メソッドは、無効なハンドルを返す可能性があるため、セキュリティ上のリスクが生じます。 Safehandle.dangerousgethandle メソッド<xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A>を安全<xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A>に使用する方法の詳細については、「」および「」のメソッドを参照してください。|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|これらのメソッドは、予期しない場所からアセンブリを読み込むことができます。 たとえば、アセンブリを読み込むメソッドの詳細については、MSDN Web サイトの「Suzanne クックの .NET CLR Note のブログ投稿[LoadFile](https://docs.microsoft.com/archive/blogs/suzcook/loadfile-vs-loadfrom)と[バインドコンテキストの選択](https://docs.microsoft.com/archive/blogs/suzcook/choosing-a-binding-context)」を参照してください。|
|[Cosetproxyblanket](https://msdn.microsoft.com/library/ms692692.aspx) (Ole32)<br /><br /> [CoInitializeSecurity](https://msdn.microsoft.com/library/ms693736.aspx) (Ole32)|マネージプロセスでユーザーコードの実行が開始されるまでに、CoSetProxyBlanket を確実に呼び出すには遅すぎます。 共通言語ランタイム (CLR) は、ユーザーの P/Invoke の成功を妨げる可能性がある初期化アクションを実行します。<br /><br /> マネージアプリケーションに CoSetProxyBlanket を呼び出す必要がある場合は、ネイティブコード (C++) 実行可能ファイルを使用してプロセスを開始し、ネイティブコードで CoSetProxyBlanket を呼び出して、マネージコードアプリケーションをプロセスで開始することをお勧めします。 (必ずランタイムバージョン番号を指定してください。)|

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、危険なメソッドまたは問題のあるメソッドへの呼び出しを削除するか置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則のメッセージは、問題のあるメソッドに代わる手段がない場合にのみ、非表示にする必要があります。

## <a name="see-also"></a>参照
 [信頼性の警告](../code-quality/reliability-warnings.md)
