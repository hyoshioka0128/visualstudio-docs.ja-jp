---
title: 'CA2106: セキュリティで保護されたアサート |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2106
- SecureAsserts
helpviewer_keywords:
- CA2106
- SecureAsserts
ms.assetid: 91feb36e-6e2c-436c-8272-5aee31f77e98
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: eb0e097c2f13fa9d9279a5f3e9761a53cb6e4b1d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547746"
---
# <a name="ca2106-secure-asserts"></a>CA2106:アサートをセキュリティで保護します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SecureAsserts|
|CheckId|CA2106|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メソッドによってアクセス許可がアサートされますが、呼び出し元に対してセキュリティ チェックが実行されていません。

## <a name="rule-description"></a>ルールの説明
 セキュリティ チェックを実行せずにセキュリティ アクセス許可をアサートすると、悪用される可能性があるセキュリティの弱点がコード内に残る場合があります。 セキュリティのアクセス許可がアサートされると、セキュリティスタックウォークが停止します。 呼び出し元に対してチェックを実行せずにアクセス許可をアサートすると、呼び出し元はアクセス許可を使用して間接的にコードを実行できます。 セキュリティチェックなしのアサートは、アサートを有害な方法で使用できないことが確実な場合にのみ許可されます。 呼び出したコードが無害である場合、またはユーザーが呼び出したコードに任意の情報を渡すことができない場合、アサートは無害です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドまたはその宣言する型にセキュリティ要求を追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 セキュリティに関する注意事項を慎重に確認した後にのみ、この規則からの警告を非表示にします。

## <a name="see-also"></a>参照
 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> [安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)
