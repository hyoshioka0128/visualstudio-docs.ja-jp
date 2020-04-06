---
title: コードの自動化を提供する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CodeModel object
ms.assetid: 21cb3e63-f25c-404b-bc1d-a32ad0fdd4d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bd13b7db2065069ff1540dbfc921570c2b230b8a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705991"
---
# <a name="providing-automation-for-code"></a>コードのオートメーションの提供
コードのオートメーション モデルを作成する必要はありません。 環境 SDK には、この操作のサンプルは用意されていません。 コード モデルの詳細については、オブジェクト<xref:EnvDTE.CodeModel>を参照してください。

 コード モデルを実装するには、内部データ構造によって決定されるインターフェイスを実装する必要があります。 オブジェクトは、クラスから派生する`IDispatch`必要があります。

 拡張したオブジェクトと 、<xref:EnvDTE.CodeModel><xref:EnvDTE.FileCodeModel>は、<xref:EnvDTE.Project>オブジェクトから使用でき、次のようになります。

- <xref:EnvDTE.Project.CodeModel%2A>

- <xref:EnvDTE.ProjectItem.FileCodeModel%2A>

 オブジェクトから`CodeModel`返すオブジェクトの`FileCodeModel`インターフェイスまたは インターフェイスだけを実装するように`Project`<xref:EnvDTE.ProjectItem>選択できます。 プロジェクト システムに適した、このインターフェイスから機能を提供します。

 標準や`FileCodeModel`インターフェイスからは使用できない機能 (メソッドやプロパティなど) を追加する場合`CodeModel`は、標準から継承する独自のインターフェイスを作成します。 エンド ユーザーがプロジェクト システムを探すことを知ることができるように、プロジェクト システムでドキュメント化してください。 標準インターフェイスを返しますが、ユーザーはメソッドを`QueryInterface`呼び出したり、インターフェイスが存在することがわかっている場合は、インターフェイスにキャストできます。

## <a name="see-also"></a>関連項目
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)
