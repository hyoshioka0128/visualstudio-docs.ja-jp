---
title: コードの自動化の提供 |Microsoft Docs
description: コードモデルを実装する方法について説明します。これには、内部データ構造によって決定されるインターフェイスを実装する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 57d5337ae088560bb94a6af39902e90b6af02686
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060966"
---
# <a name="providing-automation-for-code"></a>コードのオートメーションの提供
コードのオートメーションモデルを作成する必要はありません。 環境 SDK には、そのためのサンプルが用意されていません。 コードモデルの詳細については、オブジェクトを参照してください <xref:EnvDTE.CodeModel> 。

 コードモデルを実装するには、内部データ構造によって決定されるインターフェイスを実装する必要があります。 オブジェクトは、クラスから派生する必要があり `IDispatch` ます。

 拡張するオブジェクトとは、 <xref:EnvDTE.CodeModel> <xref:EnvDTE.FileCodeModel> オブジェクトから使用でき、 <xref:EnvDTE.Project> 次のようになります。

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 `CodeModel` `FileCodeModel` オブジェクトとオブジェクトから返されたオブジェクトに、インターフェイスまたはインターフェイスだけを実装することを選択でき `Project` <xref:EnvDTE.ProjectItem> ます。 このインターフェイスには、プロジェクトシステムに適した機能をすべて提供します。

 標準およびインターフェイスからは使用できない機能 (メソッドやプロパティなど) を追加する場合は `CodeModel` 、 `FileCodeModel` 標準から継承する独自のインターフェイスを作成します。 エンドユーザーが見つけられるように、プロジェクトシステムでドキュメント化してください。 標準のインターフェイスを返しますが、ユーザーはメソッドを呼び出すことも、インターフェイスにキャストすることもでき `QueryInterface` ます (存在する場合)。

## <a name="see-also"></a>こちらもご覧ください
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)
