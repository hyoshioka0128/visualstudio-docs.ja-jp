---
title: Visual Studio コマンドテーブル (.Vsct) Files |Microsoft Docs
description: コマンドテーブルの構成ファイルについて説明します。これは、VSPackage に含まれる一連のコマンドを記述するテキストファイルです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c1baef0936cfe37d09fb8c65f2675bb9f4208f45
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963407"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio Command Table (.Vsct) ファイル
コマンドテーブル構成ファイルは、VSPackage に含まれる一連のコマンドを記述したテキストファイルです。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コマンドテーブル (vsct) コンパイラは、XML ベースの構成ファイル (vsct ファイル) をバイナリコマンドテーブル出力 (cto) ファイルにコンパイルします。 結果として得られる cto ファイルは、コマンドテーブル (CTC) コンパイラを使用して ctc 構成ファイルをコンパイルすることによって作成されるファイルと同じです。 ただし、xml ベースの vsct ファイルには、XML エディターや XML IntelliSense など、いくつかの利点があります。

 Vsct ファイルの構文とセマンティクスの詳細については、「XML コマンドテーブルの設計」 (「」を参照してください [。Vsct) ファイル](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

## <a name="in-this-section"></a>このセクションの内容
 [XML コマンド テーブル (.Vsct) ファイルの設計](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 Vsct ファイルをデザインする方法について説明します。

 [方法: .Vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 Vsct ファイルを作成するためのメソッドを比較します。 新しい vsct ファイルを手動で作成するプロセスについて説明します。

## <a name="related-sections"></a>関連項目
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)

 コマンドテーブルの XML 構成ファイルの各セクションの詳細について説明します。

 [コマンドテーブルの構成 (を実行します。Ctc) ファイル](/previous-versions/bb165153(v=vs.100)) には、非推奨の ctc ファイル形式の概要が示されています。

 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンドテーブル形式の指定について説明します。

 [VSPackage のリソース](../../extensibility/internals/resources-in-vspackages.md)

 マネージ Vspackage でマネージリソースとアンマネージリソースを使用する方法について説明します。

 [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。