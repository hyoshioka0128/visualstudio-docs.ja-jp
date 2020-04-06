---
title: VS パッケージの管理 |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60745d07679ae53b85d169473ed37ab314b67624
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702652"
---
# <a name="manage-vspackages"></a>VSPackage を管理する
ほとんどの場合、プロジェクトテンプレートと項目テンプレートはパッケージを自動的に登録してロードするため、VSPackages の管理について心配する必要はありません。 ただし、状況によっては、パッケージを管理するためにもう少し学習する必要があります。

## <a name="use-the-experimental-instance"></a>実験用インスタンスの使用
 実験インスタンスの詳細については、「[実験](../extensibility/the-experimental-instance.md)インスタンス」を参照してください。

## <a name="register-and-unregister-vspackages"></a>VS パッケージの登録と登録解除
 VSPackages およびその他の種類の拡張機能を登録および登録解除する方法については、「 [VSPackages の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

## <a name="load-a-vspackage"></a>VS パッケージを読み込む
 VS パッケージは、特定の CMDUICONTEXT GUID がオンになっているときに自動読み込みに設定できます。 詳細については、「 [VS パッケージの読み込み](../extensibility/loading-vspackages.md)」を参照してください。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>非同期パッケージを使用して VS パッケージをバックグラウンドで読み込む
 この`AsyncPackage`クラスは、Visual Studio で UI の応答性を向上するために、バックグラウンド スレッドでパッケージを読み込む機能を有効にします。 詳細については、「[方法 : AsyncPackage を使用して VSPackage をバックグラウンドで読み込む](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)」を参照してください。

## <a name="rule-based-ui-context-for-extensions"></a>拡張機能のルール ベースの UI コンテキスト
 ルール ベースの UI コンテキストでは、拡張機能の作成者は、UI コンテキストがアクティブ化され、関連付けられた VSPackages が読み込まれる正確な条件を定義できます。 詳細については、「[方法 : Visual Studio 拡張機能に対してルール ベースの UI コンテキストを使用する](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)」を参照してください。

## <a name="diagnose-extension-performance"></a>拡張機能のパフォーマンスを診断する
拡張機能は、起動とソリューションの読み込みのパフォーマンスに影響を与える可能性があります。 Visual Studio 拡張機能の影響を計算する方法と、拡張機能がパフォーマンスに影響を与える拡張機能として表示されるかどうかをテストするためにローカルで分析する方法について説明します。 詳細については、「方法[: 拡張機能のパフォーマンスを診断する](how-to-diagnose-extension-performance.md)」を参照してください。

## <a name="troubleshoot-vspackages"></a>VS パッケージのトラブルシューティング
 読み込まない、またはエラーが発生している VSPackage のトラブルシューティングのテクニックを見つける: [VSPackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
