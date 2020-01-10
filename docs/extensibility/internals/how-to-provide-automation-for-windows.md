---
title: '方法: Windows の自動化を提供する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f02860b76c80a05808d4e46f315fc3616a19f94f
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848848"
---
# <a name="how-to-provide-automation-for-windows"></a>方法: windows の自動化を提供する

ドキュメントとツールウィンドウの自動化を提供できます。 オートメーションオブジェクトをウィンドウで使用できるようにする場合は常にオートメーションを提供することをお勧めします。また、作業リストの場合と同様に、事前に作成されたオートメーションオブジェクトが環境に用意されていません。

## <a name="automation-for-tool-windows"></a>ツールウィンドウの自動化

環境では、次の手順で説明するように、標準の <xref:EnvDTE.Window> オブジェクトを返すことによって、ツールウィンドウを自動化できます。

1. __VSFPROPID を使用して、環境を介して <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> メソッドを呼び出し[ます。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)`Window` オブジェクトを取得するには `VSFPROPID` パラメーターとして VSFPROPID_ExtWindowObject ます。

2. 呼び出し元が <xref:EnvDTE.Window.Object%2A>を通じてツールウィンドウに対して VSPackage 固有のオートメーションオブジェクトを要求すると、環境は `IExtensibleObject`、<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>、または `IDispatch` インターフェイスの `QueryInterface` を呼び出します。 `IExtensibleObject` と `IVsExtensibleObject` はどちらも <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> メソッドを提供します。

3. その後、環境が `NULL`を渡す `GetAutomationObject` メソッドを呼び出すと、VSPackage 固有のオブジェクトを渡して応答します。

4. `IExtensibleObject` に対して `QueryInterface` を呼び出して `IVsExtensibleObject` が失敗した場合、環境は `IDispatch`の `QueryInterface` を呼び出します。

## <a name="automation-for-document-windows"></a>ドキュメントウィンドウの自動化

標準 <xref:EnvDTE.Document> オブジェクトは、環境からも使用できます。ただし、`IExtensibleObject` インターフェイスを実装し `GetAutomationObject`に応答することで、エディターは <xref:EnvDTE.Document> オブジェクトを独自に実装できます。

また、エディターは、`IVsExtensibleObject` または `IExtensibleObject` インターフェイスを実装することによって、<xref:EnvDTE.Document.Object%2A> メソッドを通じて取得される VSPackage 固有のオートメーションオブジェクトを提供できます。 [Vssdk サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)は、RTF ドキュメント固有のオートメーションオブジェクトを提供します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
