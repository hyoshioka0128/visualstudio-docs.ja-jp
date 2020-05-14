---
title: VS パッケージのオートメーションの提供 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6364f9cbaf3409e076eeb77365e5d793c7be96cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705949"
---
# <a name="providing-automation-for-vspackages"></a>VSPackage でのオートメーションの提供
VSPackage にオートメーションを提供する主な方法は、VSPackage 固有のオブジェクトを実装することと、標準のオートメーション オブジェクトを実装する方法です。 一般に、これらは環境のオートメーション モデルを拡張するために一緒に使用されます。

## <a name="vspackage-specific-objects"></a>VS パッケージ固有のオブジェクト
 オートメーション モデル内の特定の場所では、VSPackage に固有のオートメーション オブジェクトを提供する必要があります。 たとえば、新しいプロジェクトでは、VSPackage のみが提供する個別のオブジェクトが必要です。 これらのオブジェクトの名前はレジストリに入力され、環境`DTE`オブジェクトの呼び出しによって取得されます。

 VSPackage 固有のオブジェクトは、オートメーション コンシューマーが標準オブジェクトの Object プロパティを通じて提供されるオブジェクトを使用する場合にも取得できます。 たとえば、標準`Window`オブジェクトには、一般的`Object`にプロパティと呼ばれるプロパティ`Windows.Object`があります。 コンシューマーが VSPackage`Window.Object`に実装されているウィンドウで を呼び出すときは、独自のデザインの特定のオートメーション オブジェクトを渡します。

#### <a name="projects"></a>プロジェクト
 VSPackage は、VSPackage 固有のオブジェクトを使用して、新しいプロジェクトの種類のオートメーション モデルを拡張できます。 VSPackage に新しいオートメーション オブジェクトを提供する主な目的は、一意のプロジェクト<xref:Microsoft.VisualStudio.VCProjectEngine.VCProject>オブジェクト<xref:VSLangProj80.VSProject2>を オブジェクトまたはオブジェクトと区別することです。 この差別化は、ソリューション内で並べて表示される場合に、他の種類のプロジェクトを別に、プロジェクトの種類を 1 つにまとめたり反復処理したりする場合に便利です。 詳細については、「[プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)」を参照してください。

#### <a name="events"></a>イベント
 環境のイベント アーキテクチャは、独自の VSPackage 固有のオブジェクトを追加する別の場所を提供します。 たとえば、独自のイベント オブジェクトを作成することで、プロジェクトの環境のイベント モデルを拡張できます。 新しい項目を独自のプロジェクトの種類に追加するときに、独自のイベントを提供する場合があります。 詳細については、「[イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)」を参照してください。

#### <a name="window-objects"></a>ウィンドウ オブジェクト
 呼び出されたときに、VSPackage 固有のオートメーション オブジェクトを環境に戻すことができます。 から<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>派生したオブジェクト<xref:EnvDTE.IExtensibleObject>、または`IDispatch`プロパティを戻すオブジェクトを実装し、そのオブジェクトがサイト化されているウィンドウ オブジェクトを拡張します。 たとえば、この方法を使用して、ウィンドウ フレーム内に設置されたコントロールのオートメーションを提供できます。 このオブジェクトのセマンティクスと、それが拡張する可能性のある他のオブジェクトは、設計する必要があります。 詳細については、「[方法 : Windows のオートメーションを提供する](../../extensibility/internals/how-to-provide-automation-for-windows.md)」を参照してください。

#### <a name="options-pages-on-the-tools-menu"></a>[ツール] メニューの [オプション] ページ
 ページを実装し、独自のオプションを作成するレジストリに情報を追加することで、ツール、オプションのオートメーション モデルを拡張するページを作成できます。 その後、他のオプション ページと同様に、環境オブジェクト モデルを通じてページを呼び出すことができます。 VSPackages を使用して環境に追加する機能のデザインにオプション ページが必要な場合は、オートメーション サポートも追加する必要があります。 詳細については、「[オプション ページのオートメーション サポート](../../extensibility/internals/automation-support-for-options-pages.md)」を参照してください。

## <a name="standard-automation-objects"></a>標準オートメーションオブジェクト
 プロジェクトのオートメーションを拡張するには、他のプロジェクト オブジェクトの横に表示`IDispatch`される標準オートメーション オブジェクト (から派生したもの) を実装し、標準のメソッドとプロパティを実装します。 標準オブジェクトの例としては`Projects`、 、 `Project`、`ProjectItem`および`ProjectItems`などのソリューション階層に挿入されるプロジェクト オブジェクトがあります。 すべての新しいプロジェクトの種類は、これらのオブジェクトを実装する必要があります (場合によっては、プロジェクトのセマンティクスに応じて他のオブジェクト)。

 ある意味では、これらのオブジェクトは、VSPackage 固有のプロジェクト オブジェクトの反対の利点を提供します。 標準のオートメーション オブジェクトを使用すると、同じオブジェクトをサポートする他のプロジェクトと同様に、プロジェクトを一般化して使用できます。 したがって、汎用`Project`および`ProjectItem`オブジェクトに対して記述されたアドインは、任意の種類のプロジェクトに対して機能できます。 詳細については、「[プロジェクトモデリング](../../extensibility/internals/project-modeling.md)」を参照してください。
