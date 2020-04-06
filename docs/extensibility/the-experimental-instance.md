---
title: 実験用インスタンス |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699041"
---
# <a name="the-experimental-instance"></a>実験用インスタンス
テストされていないアプリケーションから Visual Studio 開発環境を保護するために、VSSDK には実験用の領域があります。 通常どおり Visual Studio を使用して新しいアプリケーションを開発しますが、この実験用インスタンスを使用して実行します。

 VSIX パッケージを持つすべてのアプリケーションは、デバッグ モードで Visual Studio の実験用インスタンスを起動します。

 特定のソリューションの外部で Visual Studio の実験用インスタンスを起動する場合は、コマンド ウィンドウで次のコマンドを実行します。

 "*\<ビジュアル スタジオ インストール パス>* \Common7\IDE\devenv.exe" /ルートサフィックス Exp

> [!NOTE]
> 実験用インスタンスは、 および`<version number>Exp``<version number>Exp_Config`ノードの下のレジストリに書き込まれます。 たとえば、Visual Studio 2015 の実験用レジストリ領域は、
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` および `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 拡張機能を開発中に実験用インスタンスで実行することをお勧めします。 拡張機能を配置すると、開発インスタンスで実行されます。 アプリケーションの登録の詳細については、「 [VSPackages](../extensibility/internals/registering-vspackages.md)の登録 」を参照してください。
