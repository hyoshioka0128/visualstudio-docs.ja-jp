---
title: '方法 : Windows のオートメーションを提供する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c8716fbaa56cdb77063597fd5e07f6e469cc86a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707948"
---
# <a name="how-to-provide-automation-for-windows"></a>方法: ウィンドウのオートメーションを提供する

ドキュメント ウィンドウとツール ウィンドウのオートメーションを提供できます。 オートメーションの提供は、オートメーション オブジェクトをウィンドウで使用できるようにする場合や、環境が既製のオートメーション オブジェクトを提供していない場合に、タスク リストと同様に、常に推奨されます。

## <a name="automation-for-tool-windows"></a>ツール ウィンドウのオートメーション

環境は、次の手順で説明されているように標準<xref:EnvDTE.Window>オブジェクトを返すことによって、ツール ウィンドウのオートメーションを提供します。

1. __VSFPROPIDを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>使用して、環境を介してメソッドを呼び出[します。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>)オブジェクトを`VSFPROPID`取得するパラメーターとして`Window`VSFPROPID_ExtWindowObjectします。

2. 呼び出し元がツール ウィンドウの VSPackage 固有の<xref:EnvDTE.Window.Object%2A>オートメーション オブジェクトを`QueryInterface`要求`IExtensibleObject`すると<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>、環境は`IDispatch`、、または インターフェイスを呼び出します。 両方`IExtensibleObject`とも`IVsExtensibleObject`メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A>提供します。

3. その後、環境が`GetAutomationObject`メソッドを渡`NULL`して呼び出すと、VSPackage 固有のオブジェクトを返して応答します。

4. を呼`QueryInterface`び`IExtensibleObject`出`IVsExtensibleObject`して失敗した場合、環境`QueryInterface`は`IDispatch`を呼び出します。

## <a name="automation-for-document-windows"></a>ドキュメント ウィンドウのオートメーション

標準<xref:EnvDTE.Document>オブジェクトは環境からも利用できますが、エディターは インターフェイスを実装<xref:EnvDTE.Document>`IExtensibleObject`し、 に応答することで、独自のオブジェクトの実装`GetAutomationObject`を持つことができます。

また、エディターは、または<xref:EnvDTE.Document.Object%2A>`IVsExtensibleObject``IExtensibleObject`インターフェイスを実装することによって、メソッドを通じて取得された VSPackage 固有のオートメーション オブジェクトを提供できます。 [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)は、RTF ドキュメント固有のオートメーション オブジェクトを提供します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
