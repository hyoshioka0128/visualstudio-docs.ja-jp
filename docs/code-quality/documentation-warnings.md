---
title: ドキュメントルール
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation rules
- managed code analysis rules, documentation rules
- rules, documentation
author: mavasani
ms.author: mavasani
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f4ec6a0dd154dae89145add26c60a8b1322a444
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808653"
---
# <a name="documentation-rules"></a>ドキュメントルール

ドキュメントルールでは、外部から参照可能な Api に [XML ドキュメントコメント](/dotnet/csharp/codedoc) を適切に使用することで、適切にドキュメント化されたライブラリの作成をサポートしています。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1200:プレフィックスで cref タグを使用しません](../code-quality/ca1200.md) | XML ドキュメントタグの [cref](/dotnet/csharp/programming-guide/xmldoc/cref-attribute) 属性は、"コード参照" を意味します。 タグの内部テキストが、型、メソッド、プロパティなど、コード要素であることを指定します。 プレフィックスでタグを使用するのは避けて `cref` ください。これにより、コンパイラが参照を検証できなくなります。 また、Visual Studio 統合開発環境 (IDE: integrated development environment) が、リファクタリング中にこれらのシンボル参照を検索および更新できないようにします。 |

## <a name="see-also"></a>こちらもご覧ください

- [コード分析規則](../code-quality/code-analysis-for-managed-code-warnings.md)
