---
title: Vspackage | の自動化を提供するMicrosoft Docs
description: VSPackage 固有のオブジェクトを実装し、標準オートメーションオブジェクトを実装することによって、Vspackage の自動化を実現する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9a19b5e0e543052dad492ab319595c8ef76dfe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060953"
---
# <a name="providing-automation-for-vspackages"></a>VSPackage でのオートメーションの提供
Vspackage の自動化を提供するには、VSPackage 固有のオブジェクトを実装し、標準オートメーションオブジェクトを実装するという2つの主な方法があります。 通常、これらは、環境のオートメーションモデルを拡張するために一緒に使用されます。

## <a name="vspackage-specific-objects"></a>VSPackage-Specific オブジェクト
 オートメーションモデル内の特定の場所では、VSPackage に固有のオートメーションオブジェクトを提供する必要があります。 たとえば、新しいプロジェクトでは、VSPackage のみが提供する個別のオブジェクトが必要です。 これらのオブジェクトの名前は、レジストリに入力され、環境オブジェクトへの呼び出しによって取得され `DTE` ます。

 VSPackage 固有のオブジェクトは、オートメーションコンシューマーが標準オブジェクトの Object プロパティを通じて提供されたオブジェクトを使用する場合にも取得できます。 たとえば、標準のオブジェクトにはプロパティがあり、これ `Window` は `Object` プロパティとして一般的に知られてい `Windows.Object` ます。 コンシューマーが VSPackage に実装されているウィンドウでを呼び出す場合は、 `Window.Object` 独自の設計の特定のオートメーションオブジェクトを返します。

#### <a name="projects"></a>プロジェクト
 Vspackage は、独自の VSPackage 固有のオブジェクトを使用して、新しいプロジェクトの種類のオートメーションモデルを拡張できます。 VSPackage の新しいオートメーションオブジェクトを提供する主な目的は、オブジェクトまたはオブジェクトから一意のプロジェクトオブジェクトを区別することです <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> <xref:VSLangProj80.VSProject2> 。 この違いは、プロジェクトの種類を他のプロジェクトの種類とは別に並べて表示したり、繰り返したりする方法を提供する場合に便利です。 詳細については、「 [プロジェクトオブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)」を参照してください。

#### <a name="events"></a>イベント
 環境のイベントアーキテクチャには、独自の VSPackage 固有のオブジェクトを追加するための別の場所が用意されています。 たとえば、独自の一意のイベントオブジェクトを作成することによって、プロジェクトの環境のイベントモデルを拡張できます。 独自のプロジェクトの種類に新しい項目が追加されたときに、独自のイベントを提供することができます。 詳細については、「 [イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)」を参照してください。

#### <a name="window-objects"></a>ウィンドウ オブジェクト
 Windows は、呼び出されたときに、VSPackage 固有のオートメーションオブジェクトを環境に戻すことができます。 から派生したオブジェクト、またはプロパティを使用して、配置されているウィンドウオブジェクトを拡張するオブジェクトを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> <xref:EnvDTE.IExtensibleObject> `IDispatch` ます。 たとえば、この方法を使用して、ウィンドウフレームに配置されているコントロールのオートメーションを提供できます。 このオブジェクトのセマンティクスと、それによって拡張される可能性のあるその他のオブジェクトは、設計の対象となります。 詳細については、「 [方法: Windows のオートメーションを提供する](../../extensibility/internals/how-to-provide-automation-for-windows.md)」を参照してください。

#### <a name="options-pages-on-the-tools-menu"></a>[ツール] メニューの [オプション] ページ
 ページを作成して、ページを実装し、レジストリに情報を追加して独自のオプションを作成することによって、ツール、オプションのオートメーションモデルを拡張することができます。 その後、他のオプションページと同様に、環境オブジェクトモデルを使用してページを呼び出すことができます。 Vspackage を通じて環境に追加する機能の設計にオプションページが必要な場合は、オートメーションサポートも追加する必要があります。 詳細については、「 [オプションページのオートメーションサポート](../../extensibility/internals/automation-support-for-options-pages.md)」を参照してください。

## <a name="standard-automation-objects"></a>標準オートメーションオブジェクト
 プロジェクトのオートメーションを拡張するには、 `IDispatch` 他のプロジェクトオブジェクトの横にある標準のオートメーションオブジェクト (から派生) を実装し、標準のメソッドとプロパティを実装します。 標準オブジェクトの例としては、ソリューション階層に挿入されるプロジェクトオブジェクト (、、、など) があり `Projects` `Project` `ProjectItem` `ProjectItems` ます。 新しいプロジェクトの種類ごとに、これらのオブジェクト (および場合によっては、プロジェクトのセマンティクスに応じて他のオブジェクト) を実装する必要があります。

 つまり、これらのオブジェクトは、VSPackage 固有のプロジェクトオブジェクトの逆の利点を提供します。 標準のオートメーションオブジェクトを使用すると、同じオブジェクトをサポートする他のプロジェクトと同様の方法でプロジェクトを使用できます。 そのため、一般オブジェクトおよびオブジェクトに対して記述されたアドインは、 `Project` `ProjectItem` 任意の種類のプロジェクトに対して機能できます。 詳細については、「 [プロジェクトモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。
