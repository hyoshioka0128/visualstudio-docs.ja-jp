---
title: Dotfuscator Community をアップグレードする
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, 保護, Community Edition, 難読化, .NET, 無料, Visual Studio 2019, Visual Studio 2017, Visual Studio, アップグレード, コマンド ライン
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator upgrade
- upgrade Dotfuscator
- upgrading Dotfuscator
- register Dotfuscator
- registering Dotfuscator
- Dotfuscator command line
- Dotfuscator Professional
description: Visual Studio に含まれている Dotfuscator Community の無料コピーをアップグレードする方法について説明します。
ms.assetid: c7c60904-27f9-4f1f-b79b-ddf65041b810
author: Joe-Sewell-PreEmptive
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 555b23f33ee1e3541afc6181a9ec6c4ece833b81
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748892"
---
# <a name="upgrade-dotfuscator-community"></a>Dotfuscator Community をアップグレードする

Dotfuscator Community には、Microsoft Visual Studio を使用しているすべての開発者がすぐに利用できる多くのアプリケーション保護機能と強化機能がありますが、
Dotfuscator のバージョンをアップグレードすると、さらに多くの機能を利用できるようになります。

## <a name="registering-dotfuscator-community"></a>Dotfuscator Community の登録

Dotfuscator Community の登録ユーザーは、[コマンドライン サポート][cli]などの追加機能にアクセスできます。コマンドラインを使用すると、Dotfuscator Community を自動ビルド プロセスに簡単に統合できます。 また、登録することで、[難読化されたスタック トレースをデコードする][decode-obfuscated]ために使用される組み込みツールへのアクセスが許可されます。

登録は無料で、簡単な手順ですぐに実行できます。
Dotfuscator Community に登録するには、[Dotfuscator Community の完全なユーザー ガイドの手順][register-ce]を参照してください。

## <a name="dotfuscator-professional"></a>Dotfuscator Professional

Dotfuscator Community では基本的なレベルの保護機能が提供され、***PreEmptive Protection - Dotfuscator Professional*** には、次のような強化された難読化変換機能と保護機能が含まれています。

* *知的財産の保護*
  * Enhanced Overload Induction™、ランダムな識別子選択など、追加の名前変更オプション。
  * エンタープライズレベルの難読化変換へのアクセス ([自動コード逆コンパイルを阻止する目的の変換など][control-flow])。
  * [機密性の高い文字列を難読化][string-encryption]し、逆コンパイルされたコードの単純な検索不可能にする機能。
  * [所有権と配布文字列をアセンブリに慎重に埋め込み][watermarking]、不正なソフトウェア リークのソースを判断できる機能。
  * [複数のアセンブリを組み合わせ][linking]て、懸案事項の分離を除去することで、攻撃者がコード要素の役割を判断するのをさらに困難にする機能。
  * [使用されていないコードをアプリケーションから自動的に削除][pruning]して、付属される機密性の高いコードの量を減らす機能。
* *アプリケーション整合性の保護*
  * その他の[アプリケーション保護動作][check-actions]。
  * アプリケーションの有効期限前の警告期間を指定する機能。
  * 有効期限の警告期間中、または有効期限後にアプリケーション コードを通知する機能。

Dotfuscator Professional は業界標準の [.NET 難読化ツール][net-obfuscator]です。継続的なサポート、保守、製品の更新が必要な企業の開発者に適しています。
また、Dotfuscator Professional は Visual Studio との統合が強化され、商業目的の使用についてライセンスが付与されます。

Dotfuscator Professional の高度なアプリケーション保護機能の詳細については、PreEmptive Solutions の [Dotfuscator の概要に関するページ][product-about]と、[Community Edition との比較][product-compare]を参照してください。
[preemptive.com では、完全にサポートされている評価版を入手できます][eval]。

## <a name="see-also"></a>関連項目

[Dotfuscator Community の完全なユーザー ガイドのこのトピック][full]

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[control-flow]:  https://www.preemptive.com/products/dotfuscator/features#controlflow
[string-encryption]:  https://www.preemptive.com/products/dotfuscator/features#string
[watermarking]:  https://www.preemptive.com/products/dotfuscator/features#watermarking
[linking]:  https://www.preemptive.com/products/dotfuscator/features#linking
[pruning]:  https://www.preemptive.com/products/dotfuscator/features#pruning

[check-actions]:  https://www.preemptive.com/dotfuscator/pro/userguide/en/protection_checks_overview.html#actions

[net-obfuscator]:  https://www.preemptive.com/products/dotfuscator/overview
[eval]:  https://www.preemptive.com/eval-request

[product-about]:  https://www.preemptive.com/products/dotfuscator/overview
[product-compare]:  https://www.preemptive.com/products/dotfuscator/compare-editions

[cli]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_cli.html
[register-ce]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html#register

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrades.html
[decode-obfuscated]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_decode_stack_trace.html
