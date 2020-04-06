---
title: エディタと言語サービス拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e37165dc5fe9ac010545304218e807d923b424b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712021"
---
# <a name="editor-and-language-service-extensions"></a>エディターおよび言語サービス拡張
Visual Studio コード エディターのほとんどの機能を拡張できます。 エディターは、Windows プレゼンテーションファンデーション (WPF) に基づいており、マネージ コードで記述されています。 この設計は、以前のバージョンの Visual Studio のデザインとは異なりますが、同じ機能のほとんどを提供します。 エディターを拡張するには、マネージ機能拡張フレームワーク (MEF) を使用します。

 Visual Studio SDK には、以前のバージョン用に作成された VSPackage をサポートする*shim*と呼ばれるアダプターが用意されています。 VSPackage が既に存在する場合は、パフォーマンスと信頼性を向上させるために新しいテクノロジに更新することをお勧めします。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)|エディター項目テンプレートの使用方法について説明します。|
|[エディタと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)|コア エディターのデザインと機能を紹介し、それを拡張する方法を示すドキュメントへのリンク。|
|[エディタのレガシーインターフェイス](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)|既存のコードからコア エディターにアクセスする方法を説明するドキュメントへのリンク。|
|[カスタム エディターとデザイナーを作成する](../extensibility/creating-custom-editors-and-designers.md)|カスタム エディターの作成方法を説明するドキュメントへのリンク。|
|[従来の言語サービスの拡張性](../extensibility/internals/legacy-language-service-extensibility.md)|プログラミング言語を Visual Studio に統合する方法を説明するドキュメントへのリンク。|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|マネージ機能拡張フレームワーク (MEF) について説明します。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Windows プレゼンテーション ファウンデーション (WPF) を紹介します。|
