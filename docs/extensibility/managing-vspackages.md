---
title: Vspackage の管理 |Microsoft Docs
description: Vspackage の管理について説明します。これにより、Visual Studio によって提供される既定の VSPackage 管理と、カスタマイズする方法とタイミングを簡単に使用できるようになります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2b0e3b95ee3c715eb21028b6c156b7a62ea82d41
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943219"
---
# <a name="manage-vspackages"></a>VSPackage を管理する
ほとんどの場合、Vspackage の管理について心配する必要はありません。プロジェクトと項目テンプレートによってパッケージが登録され、自動的に読み込まれるためです。 ただし、状況によっては、パッケージを管理するためにもう少し学習が必要になる場合があります。

## <a name="use-the-experimental-instance"></a>実験用インスタンスを使用する
 実験用インスタンスの詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

## <a name="register-and-unregister-vspackages"></a>Vspackage の登録と登録解除
 Vspackage とその他の種類の拡張機能を登録および登録解除する方法については、「 [vspackage の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

## <a name="load-a-vspackage"></a>VSPackage を読み込む
 Vspackage は、特定の CMDUICONTEXT GUID が有効になっている場合に自動読み込みするように設定できます。 詳細については、「 [Load vspackage](../extensibility/loading-vspackages.md)」を参照してください。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>AsyncPackage を使用してバックグラウンドで Vspackage を読み込む
 クラスは、 `AsyncPackage` Visual Studio での UI の応答性を向上させるために、バックグラウンドスレッドでのパッケージの読み込みを有効にします。 詳細については、「 [方法: AsyncPackage を使用してバックグラウンドで vspackage を読み込む](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)」を参照してください。

## <a name="rule-based-ui-context-for-extensions"></a>拡張機能のルールベースの UI コンテキスト
 ルールベースの UI コンテキストを使用すると、拡張機能の作成者は、UI コンテキストがアクティブ化され、関連付けられている Vspackage が読み込まれる正確な条件を定義できます。 詳細については、「 [方法: 規則ベースの UI コンテキストを Visual Studio 拡張機能に使用する](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)」を参照してください。

## <a name="diagnose-extension-performance"></a>拡張機能のパフォーマンスを診断する
拡張機能は、起動時およびソリューションの読み込みのパフォーマンスに影響を与える可能性があります。 Visual Studio 拡張機能の影響がどのように計算されるか、および拡張機能がパフォーマンスに影響する拡張機能として表示されるかどうかをテストするためにローカルで分析する方法について説明します。 詳細については、「 [方法: 拡張機能のパフォーマンスを診断する](how-to-diagnose-extension-performance.md)」を参照してください。

## <a name="troubleshoot-vspackages"></a>Vspackage のトラブルシューティング
 ロードできない、またはエラーが発生している Vspackage のトラブルシューティングの手法については、 [vspackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)に関するものをご覧ください。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
