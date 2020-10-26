---
title: 実験用インスタンス |Microsoft Docs
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
ms.openlocfilehash: 8e2284767a0aa6be58c0f7e38c912783728914cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699041"
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
