---
title: マネージド コードのコード分析
ms.date: 08/27/2020
description: Visual Studio での .NET Compiler Platform ベースのコードアナライザーについて説明します。 これらのアナライザーがマネージアセンブリの FxCop 静的分析に代わる理由を理解します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 542747f650888b384a9f9c4910b0d9caea93e948
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860569"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>Visual Studio での .NET のコード分析の概要

Visual Studio では、マネージコードのコード分析を2とおりの方法で実行できます。 [従来の分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)では、マネージアセンブリの FxCop 静的分析とも呼ばれ、最新の [.NET Compiler Platform ベースのコードアナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。 .NET Compiler Platform ベースのコードアナライザー。入力時にコードを分析します。従来の FxCop 静的コード分析は、コンパイルされたコードのみを分析します。
