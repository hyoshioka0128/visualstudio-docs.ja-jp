---
title: '方法: Windows の自動化を提供する |Microsoft Docs'
description: VisualStudio メソッドを使用して、Visual Studio でドキュメントとツールウィンドウの自動化を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 518a9d53b0bf03a1c57046789452ed007e6188f6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888980"
---
# <a name="how-to-provide-automation-for-windows"></a>方法: windows の自動化を提供する

ドキュメントとツールウィンドウの自動化を提供できます。 オートメーションオブジェクトをウィンドウで使用できるようにする場合は常にオートメーションを提供することをお勧めします。また、作業リストの場合と同様に、事前に作成されたオートメーションオブジェクトが環境に用意されていません。

## <a name="automation-for-tool-windows"></a>ツールウィンドウの自動化

環境では、次の手順で説明するように標準のオブジェクトを返すことによって、ツールウィンドウの自動化を提供し <xref:EnvDTE.Window> ます。

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>__VSFPROPID を使用して、環境経由でメソッドを呼び出し[ます。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)オブジェクトを `VSFPROPID` 取得するには、パラメーターとして VSFPROPID_ExtWindowObject `Window` します。

2. 呼び出し元がを通じて、ツールウィンドウの VSPackage 固有のオートメーションオブジェクトを要求すると、 <xref:EnvDTE.Window.Object%2A> 環境は `QueryInterface` `IExtensibleObject` 、、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> またはインターフェイスを呼び出し `IDispatch` ます。 `IExtensibleObject`と `IVsExtensibleObject` の両方がメソッドを提供し <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> ます。

3. その後、環境がメソッドを渡すときに `GetAutomationObject` `NULL` 、VSPackage 固有のオブジェクトを返すことによって応答します。

4. `QueryInterface`との呼び出し `IExtensibleObject` が失敗した場合 `IVsExtensibleObject` 、環境は `QueryInterface` を呼び出し `IDispatch` ます。

## <a name="automation-for-document-windows"></a>ドキュメントウィンドウの自動化

標準 <xref:EnvDTE.Document> オブジェクトは環境からも使用できますが、 <xref:EnvDTE.Document> インターフェイスを実装してに応答することによって、エディターはオブジェクトの独自の実装を持つことができ `IExtensibleObject` `GetAutomationObject` ます。

また、エディターは、 <xref:EnvDTE.Document.Object%2A> インターフェイスまたはインターフェイスを実装することによって、メソッドを通じて取得される VSPackage 固有のオートメーションオブジェクトを提供でき `IVsExtensibleObject` `IExtensibleObject` ます。 [Vssdk サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)は、RTF ドキュメント固有のオートメーションオブジェクトを提供します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
