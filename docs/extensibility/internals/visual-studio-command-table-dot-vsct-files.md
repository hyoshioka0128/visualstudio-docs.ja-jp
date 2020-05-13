---
title: ビジュアル スタジオ コマンド テーブル (.Vsct) ファイル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d18367436d1ee1b889558a35723e4e3cec865945
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704023"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio Command Table (.Vsct) ファイル
コマンド テーブル構成ファイルは、VSPackage に含まれるコマンドのセットを記述するテキスト ファイルです。 コマンド[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]テーブル (VSCT) コンパイラは、XML ベースの構成ファイル (.vsct ファイル) をバイナリ コマンド テーブル出力 (.cto) ファイルにコンパイルします。 結果として生成される .cto ファイルは、コマンド テーブル (CTC) コンパイラを使用して .ctc 構成ファイルをコンパイルして作成したものと同じです。 ただし、XML ベースの .vsct ファイルには、XML エディターや XML IntelliSense などのいくつかの利点があります。

 vsct ファイルの構文とセマンティクスの詳細については[、「XML コマンド テーブルの設計」を参照してください。Vsct) ファイル](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

## <a name="in-this-section"></a>このセクションの内容
 [XML コマンド テーブル (.Vsct) ファイルの設計](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 vsct ファイルのデザイン方法について説明します。

 [方法: .Vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 vsct ファイルを作成するためのメソッドを比較します。 新しい .vsct ファイルを手動で作成するプロセスについて説明します。

## <a name="related-sections"></a>関連項目
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)

 コマンド テーブル XML 構成ファイルの各セクションについて詳しく説明します。

 [コマンド テーブルの構成 (.Ctc) ファイル](https://msdn.microsoft.com/library/3413dda1-f372-4669-bcf0-c64d3463842c)廃止された .ctc ファイル形式の概要を示します。

 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンド テーブルの形式指定について説明します。

 [VSPackage のリソース](../../extensibility/internals/resources-in-vspackages.md)

 マネージ VSPackages でマネージ リソースとアンマネージ リソースを使用する方法について説明します。

 [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
