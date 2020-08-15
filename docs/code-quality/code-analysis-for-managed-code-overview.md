---
title: マネージド コードのコード分析
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 901c66a97a763345ee32b1a1540a7998934d0ff3
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248979"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio でのマネージコードのコード分析の概要

Visual Studio では、マネージコードのコード分析を2とおりの方法で実行できます。 [従来の分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)では、マネージアセンブリの FxCop 静的分析とも呼ばれ、最新の [.NET Compiler Platform ベースのコードアナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。 .NET Compiler Platform ベースのコードアナライザー。入力時にコードを分析します。従来の FxCop 静的コード分析は、コンパイルされたコードのみを分析します。
