---
title: マネージド コードのコード分析
ms.date: 08/27/2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d13a8afdfcbeb6ae9f91e39779af8b82b2461000
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89091403"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>Visual Studio での .NET のコード分析の概要

Visual Studio では、マネージコードのコード分析を2とおりの方法で実行できます。 [従来の分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)では、マネージアセンブリの FxCop 静的分析とも呼ばれ、最新の [.NET Compiler Platform ベースのコードアナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。 .NET Compiler Platform ベースのコードアナライザー。入力時にコードを分析します。従来の FxCop 静的コード分析は、コンパイルされたコードのみを分析します。
