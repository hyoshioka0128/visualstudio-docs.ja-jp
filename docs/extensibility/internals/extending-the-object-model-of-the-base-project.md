---
title: 基本プロジェクトのオブジェクト モデルを拡張する |マイクロソフトドキュメント
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33186cd477ade7f562f6191393dabe8e94f4f194
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708397"
---
# <a name="extend-the-object-model-of-the-base-project"></a>基本プロジェクトのオブジェクト モデルを拡張する

プロジェクトのサブタイプは、次の場所で、基本プロジェクトのオートメーション オブジェクト モデルを拡張できます。

- Project.Extender("ProjectSubtypeName\<>") : これにより、プロジェクトのサブタイプは、オブジェクトからカスタム<xref:EnvDTE.Project>メソッドを持つオブジェクトを提供できます。 プロジェクトのサブタイプでは、オートメーション エクステンダーを`Project`使用してオブジェクトを公開できます。 メイン<xref:EnvDTE80.IInternalExtenderProvider>プロジェクトのサブタイプ アグリゲータに実装されるインターフェイスは`VSHPROPID_ExtObjectCATID`<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>、(VSITEMID の値`itemid`に対応する) のオブジェクトを提供する必要があります[。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- ProjectItem.Extender("ProjectSubtypeName\<>") ): これにより、プロジェクトサブタイプは、プロジェクト内の特定<xref:EnvDTE.ProjectItem>のオブジェクトからカスタム メソッドを持つオブジェクトを提供できます。 プロジェクトのサブタイプでは、オートメーション エクステンダーを使用してこのオブジェクトを公開できます。 メイン<xref:EnvDTE80.IInternalExtenderProvider>プロジェクト サブタイプ アグリゲータに実装されるインターフェイスは、(目的`VSHPROPID_ExtObjectCATID`<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>の<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>) CATID からオブジェクトを提供する必要があります。

- プロジェクト.プロパティ: このコレクションは、オブジェクトの構成に依存しない`Project`プロパティを公開します。 `Project` プロパティについて詳しくは、「<xref:EnvDTE.Project.Properties%2A>」をご覧ください。 プロジェクト サブタイプは、オートメーション エクステンダーを使用して、このコレクションにプロパティを追加できます。 メイン<xref:EnvDTE80.IInternalExtenderProvider>プロジェクトのサブタイプアグリゲータに実装されるインタフェースは`VSHPROPID_BrowseObjectCATID`<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>、(VSITEMID の値に対応する`itemid`)のオブジェクトを提供する必要[があります。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- 構成.プロパティ: このコレクションは、特定の構成 (たとえば、デバッグ) のプロジェクトの構成に依存するプロパティを公開します。 詳細については、「<xref:EnvDTE.Configuration>」を参照してください。 プロジェクト サブタイプは、オートメーション エクステンダーを使用して、このコレクションにプロパティを追加できます。 メイン<xref:EnvDTE80.IInternalExtenderProvider>プロジェクト サブタイプ アグリゲータに実装されたインターフェイスは、CATID`VSHPROPID_CfgBrowseObjectCATID`のオブジェクトを提供`itemid`します[(VSITEMID の値に対応します)。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>))。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>は、ある構成参照オブジェクトを別の構成参照オブジェクトと区別するために使用されます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
