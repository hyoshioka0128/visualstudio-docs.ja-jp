---
title: 実験用インスタンス |Microsoft Docs
description: Visual Studio SDK が、テストされていないアプリケーションをデバッグモードで実行するための実験的な領域を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4786f450b108c8a6c1eaefc6f86f7adf57e9269e
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715861"
---
# <a name="the-experimental-instance"></a>実験用インスタンス
テストされていないアプリケーションから Visual Studio 開発環境を保護するために、VSSDK には実験に使用できる実験的な領域が用意されています。 通常どおり Visual Studio を使用して新しいアプリケーションを開発しますが、この実験用インスタンスを使用して実行します。

 VSIX パッケージを持つすべてのアプリケーションは、Visual Studio の実験的なインスタンスをデバッグモードで起動します。

 特定のソリューション以外で Visual Studio の実験用インスタンスを開始する場合は、コマンドウィンドウで次のコマンドを実行します。

 " *\<Visual studio installation path>* \Common7\IDE\devenv.exe"/rootsuffix Exp

> [!NOTE]
> 実験用インスタンスは、ノードとノードの下のレジストリに書き込まれ `<version number>Exp` `<version number>Exp_Config` ます。 たとえば、Visual Studio 2015 の実験的なレジストリ領域は次のようになります。
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` および `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 開発中は、実験用インスタンスで拡張機能を実行することをお勧めします。 拡張機能を配置すると、開発インスタンスで実行されます。 アプリケーションの登録の詳細については、「 [vspackage の登録](../extensibility/internals/registering-vspackages.md)」を参照してください。
