---
title: エディターと言語サービスの拡張 |Microsoft Docs
description: Windows Presentation Foundation を使用して実装され、マネージコードで記述されている Visual Studio code エディターのほとんどの機能を拡張できます。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 2b15d5f970bfc6a32489991b578a54f2eadc96ea
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995825"
---
# <a name="editor-and-language-service-extensions"></a>エディターと言語サービスの拡張機能
Visual Studio code エディターのほとんどの機能を拡張できます。 このエディターは Windows Presentation Foundation (WPF) に基づいており、マネージコードで記述されています。 この設計は、以前のバージョンの Visual Studio の設計とは異なりますが、ほとんど同じ機能を提供します。 エディターを拡張するには、Managed Extensibility Framework (MEF) を使用します。

 Visual Studio SDK には、以前のバージョン用に記述された Vspackage をサポートするための *shim* と呼ばれるアダプターが用意されています。 ただし、既存の VSPackage がある場合は、パフォーマンスと信頼性を向上させるために、新しいテクノロジに更新することをお勧めします。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)|エディター項目テンプレートの使用方法について説明します。|
|[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)|コアエディターのデザインと機能を紹介するドキュメントへのリンクと、それを拡張する方法を示します。|
|[エディター内のレガシインターフェイス](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)|既存のコードからコアエディターにアクセスする方法を説明するドキュメントへのリンクです。|
|[カスタムエディターとデザイナーを作成する](../extensibility/creating-custom-editors-and-designers.md)|カスタムエディターを作成する方法を説明するドキュメントへのリンク。|
|[従来の言語サービスの機能拡張](../extensibility/internals/legacy-language-service-extensibility.md)|プログラミング言語を Visual Studio に統合する方法について説明するドキュメントへのリンクです。|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Managed Extensibility Framework (MEF) について説明します。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Windows Presentation Foundation (WPF) について説明します。|
