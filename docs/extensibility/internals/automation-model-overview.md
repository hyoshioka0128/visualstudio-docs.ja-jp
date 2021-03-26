---
title: オートメーションモデルの概要 |Microsoft Docs
description: Visual studio のアドインまたは拡張機能を記述できるオブジェクトのセットで構成される Visual Studio のオートメーションモデルについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d763fea140ddac1b4dba955421c563700373dc22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086236"
---
# <a name="automation-model-overview"></a>オートメーションモデルの概要
オートメーションモデルは、Visual Studio アドインまたは拡張機能を記述できるオブジェクトのセットで構成されます。 アドインは、Visual Studio 環境を操作したり、一般的なタスクを自動化したりできるアプリケーションです。 Visual Studio 拡張機能では、Visual Studio のカスタムコンポーネントを作成したり、テキストエディターなどの標準コンポーネントの機能を追加したりできます。

## <a name="objects-in-the-automation-model"></a>オートメーションモデル内のオブジェクト
 オートメーションモデルは、共通環境の主要なファセットを制御するオブジェクトの関連グループで構成されます。 次の図は、オートメーションモデルを構成する Visual Studio オブジェクトの広範なセットを示しています。

 ![Visual Studio オートメーションオブジェクトグラフ](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 詳細については、「 [Visual Studio 環境の拡張](/previous-versions/esk3eey8(v=vs.140))」を参照してください。

 環境によって、さまざまな機能領域のモデルが提供されます。 たとえば、コードで見つかる可能性のあるさまざまな要素のコードモデルがあります。 さまざまなドキュメント要素のドキュメントモデルがあります。 プロジェクト領域の1つの領域は、VSPackage プロバイダーにとって特に重要です。 新しいプロジェクトの種類は、オートメーションモデルの場合とほぼ同じ方法でオートメーションモデルに寄与する可能性があり [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ます。 このプロセスについては、「 [vspackage の自動化を提供](../../extensibility/internals/providing-automation-for-vspackages.md)する」で説明しています。

 環境のオートメーションモデルの拡張を検討できる場所は次のとおりです。

- Project

- ドキュメント

- コード

- Build

オートメーションの詳細については、「 [Visual Studio のオートメーションと拡張機能](/previous-versions/visualstudio/visual-studio-2015/extensibility/extensibility-in-visual-studio?preserve-view=true&view=vs-2015)」を参照してください。 このドキュメントとそのドキュメントには、VSPackage の自動化を提供する方法についての意思決定に役立つリンクが記載されています。

## <a name="see-also"></a>こちらもご覧ください
- [方法: アドインを作成する](/previous-versions/80493a3w(v=vs.140))