---
title: 'CA1822: メンバーを static としてマークします |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkMembersAsStatic
- CA1822
helpviewer_keywords:
- MarkMembersAsStatic
- CA1822
ms.assetid: 743f0af7-41d1-4852-8d97-af0688b31118
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ce4aa6aef9c70d0d628603afa7a256c309f280d
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917942"
---
# <a name="ca1822-mark-members-as-static"></a>CA1822: メンバーを static に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1822: メンバーを静的としてマーク](/visualstudio/code-quality/ca1822-mark-members-as-static)する」を参照してください。

|||
|-|-|
|TypeName|MarkMembersAsStatic|
|CheckId|CA1822|
|[カテゴリ]|Microsoft.Performance|
|互換性に影響する変更点|非重大-変更に関係なく、メンバーがアセンブリの外部で参照できない場合。<br /><br /> 非互換性-`this` キーワードを使用してメンバーをインスタンスメンバーに変更するだけです。<br /><br /> 中断-メンバーをインスタンスメンバーから静的メンバーに変更し、アセンブリの外部から参照できる場合。|

## <a name="cause"></a>原因
 インスタンスデータにアクセスしないメンバーは、静的 ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)]では Shared) としてマークされていません。

## <a name="rule-description"></a>規則の説明
 インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 非仮想呼び出しサイトを生成すると、現在のオブジェクトポインターが null でないことを確認するために、呼び出しごとに実行時にチェックが行われなくなります。 これにより、パフォーマンスを重視するコードに対して、測定可能なパフォーマンスの向上を実現できます。 場合によっては、現在のオブジェクトインスタンスにアクセスできなかった場合、正確性の問題が発生することがあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 メンバーを静的 (または [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]で共有) としてマークするか、メソッド本体で ' this '/' Me ' を使用します (該当する場合)。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 以前に出荷されたコードについては、この修正プログラムが互換性に影響する変更になるという警告を抑制するのは安全です。

## <a name="related-rules"></a>関連規則
 [CA1811: 呼び出されていないプライベート コードを使用しません](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1812: インスタンス化されていない内部クラスを使用しないでください](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1804: 使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
