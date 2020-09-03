---
title: 相互運用性に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis warnings, interoperability warnings
- interoperability warnings
- warnings, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fd914a65ff23b05130cb0c36162bb96a3d30aa52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656504"
---
# <a name="interoperability-warnings"></a>相互運用性に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

相互運用性の警告は、COM クライアントとの対話をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1400: P/Invoke エントリポイントが存在する必要があります](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)|パブリック メソッドまたはプロテクト メソッドが System.Runtime.InteropServices.DllImportAttribute 属性を使用してマークされています。 アンマネージ ライブラリの位置を特定できないか、メソッドがライブラリ内の関数と一致しません。|
|[CA1401: P/Invoke を表示できません](../code-quality/ca1401-p-invokes-should-not-be-visible.md)|パブリック型のパブリックメソッドまたはプロテクトメソッドには System.Runtime.InteropServices.DllImportAttribute 属性があります (Visual Basic で Declare キーワードによっても実装されています)。 このようなメソッドは公開しないでください。|
|[CA1402:COM 参照可能インターフェイスでのオーバーロードを避けてください](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md)|オーバーロードされたメソッドが COM クライアントに公開されると、最初のメソッド オーバーロードだけが名前を保持します。 後続のオーバーロードは、名前にアンダースコア文字 (_) およびオーバーロードの宣言の順序に対応する整数が付加され、一意の名前に変更されます。|
|[CA1403:Auto 配置の型を COM 参照可能にすることはできません](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)|COM 参照可能な値型は、StructLayoutAttribute 属性が Layoutkind.explicit に設定された InteropServices を使用してマークされます。これらの型のレイアウトは、のバージョン間で変わる可能性が [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] あります。これにより、特定のレイアウトを期待する COM クライアントが中断されます。|
|[CA1404: P/Invoke の直後に GetLastError を呼び出します。](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)|GetLastWin32Error メソッドまたはそれと同等の GetLastError 関数が呼び出されましたが、直前 [!INCLUDE[TLA2#tla_win32](../includes/tla2sharptla-win32-md.md)] の呼び出しがプラットフォーム呼び出しメソッドに対して行われていません。|
|[CA1405:COM 参照可能な型の基本型は COM 参照可能でなければなりません](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md)|COM 参照可能な型が、COM 参照不可能な型から派生しています。|
|[CA1406:Visual Basic 6 クライアントに対しては Int64 引数を使用しません](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)|Visual Basic 6 COM クライアントでは、64 ビット整数にアクセスできません。|
|[CA1407:Com 参照可能な型で静的メンバーを使用しません](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)|COM では静的メソッドをサポートしていません。|
|[CA1408:AutoDual ClassInterfaceType を使用しないでください](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)|デュアル インターフェイスを使用する型を使用することで、クライアントを特定のインターフェイス レイアウトに対応付けることができます。 将来のバージョンで、この型またはその基本型のレイアウトに変更が加えられると、インターフェイスに対応付けられた COM クライアントが切り離されます。 既定では、ClassInterfaceAttribute 属性が指定されていない場合、ディスパッチ専用インターフェイスが使用されます。|
|[CA1409:COM 参照可能な型は作成可能でなければなりません](../code-quality/ca1409-com-visible-types-should-be-creatable.md)|COM から参照できると明確にマークされている参照型に、パブリックのパラメーター付きコンストラクターが含まれますが、パブリックの既定 (パラメーターなし) コンストラクターが含まれません。 パブリックの既定コンストラクターがない型は、COM クライアントで作成できません。|
|[CA1410:COM 登録メソッドは一致しなければなりません](../code-quality/ca1410-com-registration-methods-should-be-matched.md)|型は、属性を使用してマークされたメソッドを宣言し <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> ますが、属性を使用してマークされているメソッドを宣言しません <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> 。また、その逆も同様です。|
|[CA1411:COM 登録メソッドは参照可能であることはできません](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)|InteropServices 属性または InteropServices 属性属性を使用してマークされているメソッドは、外部から参照できています。または参照してください。|
|[CA1412:ComSource インターフェイスを IDispatch として設定します](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)|型が System.Runtime.InteropServices.ComSourceInterfacesAttribute 属性によってマークされていますが、1 つ以上の指定されたインターフェイスが ComInterfaceType.InterfaceIsIDispatch に設定された System.Runtime.InteropServices.InterfaceTypeAttribute 属性によってマークされていません。|
|[CA1413:Com 参照可能な値型ではパブリックでないフィールドを使用しません](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)|COM から参照できる値型の非パブリック インスタンス フィールドは、COM クライアントで表示できます。 フィールドの内容をレビューして、公開するべきではない情報や、設計またはセキュリティに意図しない影響を及ぼす情報が含まれていないかどうかを確認してください。|
|[CA1414: ブール型の P/Invoke 引数を MarshalAs に設定します。](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md)|Boolean データ型は、アンマネージ コードの複数の表現を持っています。|
|[CA1415: P/Invoke を正しく宣言します。](../code-quality/ca1415-declare-p-invokes-correctly.md)|このルール [!INCLUDE[TLA2#tla_win32](../includes/tla2sharptla-win32-md.md)] は、オーバーラップ構造パラメーターへのポインターを持ち、対応するマネージパラメーターが構造体へのポインターではない関数を対象とするプラットフォーム呼び出しメソッドの宣言を検索し <xref:System.Threading.NativeOverlapped?displayProperty=fullName> ます。|
