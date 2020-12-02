---
title: 基本プロジェクト | のオブジェクトモデルの拡張Microsoft Docs
description: プロジェクトのサブタイプを使用して、Visual Studio で基本プロジェクトのオートメーションオブジェクトモデルを拡張する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e4e3d7ad3f19aedc59288d6799e97d91499939c9
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96479460"
---
# <a name="extend-the-object-model-of-the-base-project"></a>基本プロジェクトのオブジェクトモデルを拡張する

プロジェクトのサブタイプは、基本プロジェクトのオートメーションオブジェクトモデルを次の場所で拡張することができます。

- プロジェクト Extender (" \<ProjectSubtypeName> "): これにより、プロジェクトのサブタイプは、オブジェクトのカスタムメソッドを使用してオブジェクトを提供でき <xref:EnvDTE.Project> ます。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用してオブジェクトを公開でき `Project` ます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されているインターフェイスは、からのオブジェクトを提供する必要があり `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> `itemid` ます (VSITEMID の値に対応[します)。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- ProjectItem (" \<ProjectSubtypeName> "): プロジェクトのサブタイプが、プロジェクト内の特定のオブジェクトからのカスタムメソッドを持つオブジェクトを提供できるようにします。 <xref:EnvDTE.ProjectItem> プロジェクトのサブタイプは、オートメーションエクステンダーを使用してこのオブジェクトを公開できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されているインターフェイスは、の `VSHPROPID_ExtObjectCATID` オブジェクト <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> (必要な CATID に対応する) を提供する必要があり <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> ます。

- プロジェクト. プロパティ: このコレクションは、オブジェクトの構成に依存しないプロパティを公開します。 `Project` `Project` プロパティについて詳しくは、「<xref:EnvDTE.Project.Properties%2A>」をご覧ください。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されているインターフェイスは、からのオブジェクトを提供する必要があり `VSHPROPID_BrowseObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> `itemid` ます (VSITEMID の値に対応し[ます)。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- 構成. Properties: このコレクションは、特定の構成 (たとえば、デバッグ) のためのプロジェクトの構成に依存するプロパティを公開します。 詳細については、「<xref:EnvDTE.Configuration>」を参照してください。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されたインターフェイスは、 `VSHPROPID_CfgBrowseObjectCATID` VSITEMID の値に対応する CATID のオブジェクトを提供し `itemid` [ます。ルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>))。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject> 1 つの構成参照オブジェクトを別の構成と区別するために使用されます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
