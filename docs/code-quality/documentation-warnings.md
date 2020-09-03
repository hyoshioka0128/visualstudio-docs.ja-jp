---
title: ドキュメントの警告
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation warnings
- managed code analysis warnings, documentation warnings
- warnings, documentation
author: mavasani
ms.author: mavasani
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4946c69bbbe4bf1c240967ebd93ef58cfa79e333
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72807097"
---
# <a name="documentation-warnings"></a>ドキュメントの警告

ドキュメント警告は、外部から参照可能な Api に [XML ドキュメントコメント](/dotnet/csharp/codedoc) を適切に使用して、適切にドキュメント化されたライブラリを作成することをサポートしています。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1200:プレフィックスで cref タグを使用しません](../code-quality/ca1200.md) | XML ドキュメントタグの [cref](/dotnet/csharp/programming-guide/xmldoc/cref-attribute) 属性は、"コード参照" を意味します。 タグの内部テキストが、型、メソッド、プロパティなど、コード要素であることを指定します。 プレフィックスでタグを使用するのは避けて `cref` ください。これにより、コンパイラが参照を検証できなくなります。 また、Visual Studio 統合開発環境 (IDE: integrated development environment) が、リファクタリング中にこれらのシンボル参照を検索および更新できないようにします。 |

## <a name="see-also"></a>関連項目

- [コード分析の警告](../code-quality/code-analysis-for-managed-code-warnings.md)
