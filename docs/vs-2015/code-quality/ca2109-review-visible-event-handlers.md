---
title: 'CA2109: 表示されているイベントハンドラーを確認します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2109
- ReviewVisibleEventHandlers
helpviewer_keywords:
- ReviewVisibleEventHandlers
- CA2109
ms.assetid: 8f8fa0ee-e94e-400e-b516-24d8727725d7
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3ddcab6e0f416837bcd7b01521a6d77ddce691b9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520979"
---
# <a name="ca2109-review-visible-event-handlers"></a>CA2109:表示するイベント ハンドラーを確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ReviewVisibleEventHandlers|
|CheckId|CA2109|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクトのイベント ハンドラー メソッドが検出されました。

## <a name="rule-description"></a>ルールの説明
 外部から参照できるイベント処理メソッドは、レビューが必要なセキュリティ上の問題を示します。

 イベント ハンドラー メソッドは、絶対に必要な場合を除き公開しないでください。 公開されたメソッドを呼び出すイベントハンドラーは、デリゲート型とイベントシグネチャが一致する限り、任意のイベントに追加できます。 イベントは、任意のコードによって発生する可能性があり、ボタンのクリックなどのユーザー操作に応じて、信頼性の高いシステムコードによって頻繁に発生します。 イベント処理メソッドにセキュリティチェックを追加しても、メソッドを呼び出すイベントハンドラーがコードによって登録されるのを防ぐことはできません。

 要求では、イベントハンドラーによって呼び出されたメソッドを確実に保護することはできません。 セキュリティ要求は、呼び出し履歴の呼び出し元を調べることによって、信頼されていない呼び出し元からコードを保護するのに役立ちます。 イベントハンドラーをイベントに追加するコードは、イベントハンドラーのメソッドが実行されるときに、必ずしも呼び出し履歴に存在するとは限りません。 そのため、イベントハンドラーメソッドが呼び出されたときに、呼び出し履歴に信頼性の高い呼び出し元しか存在しない可能性があります。 これにより、イベントハンドラーメソッドによって行われた要求が成功します。 また、メソッドが呼び出されると、要求されたアクセス許可がアサートされる場合があります。 このような理由から、この規則の違反を修正しないというリスクは、イベント処理方法を確認した後にのみ評価することができます。 コードを確認するときは、次の点を考慮してください。

- イベントハンドラーは、アクセス許可のアサートやアンマネージコードのアクセス許可の抑制など、危険または悪用可能な操作を実行しますか。

- スタック上で信頼性の高い呼び出し元のみを使用していつでも実行できるため、コードに対するセキュリティ上の脅威はどのようなものですか。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドを確認し、次の内容を評価します。

- イベント処理メソッドを非パブリックにすることはできますか。

- すべての危険な機能をイベントハンドラーから移動できますか。

- セキュリティ要求が課された場合、他の方法でも実現できますか。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告を抑制するのは、セキュリティレビューを慎重に行って、コードがセキュリティ上の脅威を引き起こさないことを確認してからです。

## <a name="example"></a>例
 次のコードは、悪意のあるコードによって誤用される可能性のあるイベント処理メソッドを示しています。

 [!code-csharp[FxCop.Security.EventSecLib#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.EventSecLib/cs/FxCop.Security.EventSecLib.cs#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> <xref:System.EventArgs?displayProperty=fullName>
 [セキュリティ確認要求](https://msdn.microsoft.com/324c14f8-54ff-494d-9fd1-bfd20962c8ba)
