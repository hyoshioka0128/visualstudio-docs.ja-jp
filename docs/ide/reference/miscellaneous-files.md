---
title: その他のファイル
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.newfile
- VS.OpenWith
- MiscellaneousFilesProject
helpviewer_keywords:
- solutions, miscellaneous files
- standalone files
- Solution Explorer, miscellaneous files
- Miscellaneous Files folder
- files [Visual Studio], miscellaneous
ms.assetid: 5b96640b-8efe-48a4-8d0a-1ae3f9587e44
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6fb01d0ce09778866074cc8f303c3e4da60f0de1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668967"
---
# <a name="miscellaneous-files"></a>その他のファイル

プロジェクトまたはソリューションから独立してファイルを操作するには、Visual Studio エディターを使用することをお勧めします。 ソリューションを開いているときに、ファイルをソリューションやプロジェクトに追加せずに開いて編集できます。 個別の操作したいファイルのことは、"その他のファイル" と呼びます。 "その他のファイル" は、ソリューションやプロジェクトの外部にあり、ビルドには含まれません。また、ソース管理の対象になっているソリューションに含めることはできません。

プロジェクトまたはソリューションとは関係なくファイルを開くことは、さまざまな理由で役立ちます。 たとえば、プロジェクト ベースのソリューションの開発に不可欠ではないが、そのソリューションの開発中に表示したいファイルがあります。 こうしたファイルの例としては、開発メモ (指示書)、データベース スキーマ、コード クリップなどがあります。 また、スタンドアロンのファイルも作成できます。

![ソリューション プロジェクト](../../ide/reference/media/projects_solutions_misc.gif)

ソリューション エクスプローラーで、該当するファイルに対する **[その他のファイル]** フォルダーを表示するには、そのフォルダー用のオプションを有効にする必要があります。 [[ドキュメント] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/documents-environment-options-dialog-box.md) から、オプションを設定することができます。 "その他のファイル" を閉じた後も特定のソリューションやプロジェクトとの関連付けを維持するには、そのためのオプションを有効にする必要があります。

**[その他のファイル]** フォルダーは、ファイルをリンクとして表します。 このフォルダーはソリューションの一部ではありませんが、設定によっては、ソリューションを開いたときに、前回ソリューションを閉じたときに開いていた "その他のファイル" の一部またはすべてが再び開かれます。

> [!NOTE]
> 一部のファイルは **[その他のファイル]** フォルダーに表示されません。これらは、.zip ファイルや .doc ファイルのような IDE では変更できないファイルです。 IDE では、外部エディターでしか変更できないファイルは追跡されません。

## <a name="commands-available-in-the-ide"></a>IDE で使用できるコマンド

メニュー、ツール バー、およびそれらに含まれるコマンドは、開いたファイルの形式によって変化します。 たとえば、テキスト ファイルを開くと、[テキスト エディター] ツール バーが表示されて、そのコマンドを使用できるようになります。 その後 XML スキーマ ファイルを開くと、[XML スキーマ] ツール バーが表示されます。 XML スキーマを編集している間は、[テキスト エディター] ツール バーのコマンド ([テキスト エディター] ツール バー自体) は使用できなくなります。 このとき、XML スキーマがアクティブなウィンドウであるため、現在の選択コンテキストはこの XML スキーマにあります。 プロジェクト ファイルから "その他のファイル" に切り替えると、プロジェクト関連のコマンドはすべて表示されなくなり、そのファイルに直接関連するコマンドだけが表示されます。

## <a name="folder-display-options"></a>フォルダー表示オプション

**[その他のファイル]** フォルダーの表示オプションを設定すれば、"その他のファイル" を開いていない場合でも、このフォルダーが表示されるようにすることができます。 ソリューション ファイルは、"その他のファイル" の一覧を永久に管理するわけではありません。 ソリューション ファイルでは、直前に使用した (MRU) ファイル リストをユーザー別に保存するためのオプション機能が使用されます。

## <a name="see-also"></a>関連項目

- [プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../develop-code-in-visual-studio-without-projects-or-solutions.md)
- [ソリューションおよびプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)
- [[ドキュメント] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/documents-environment-options-dialog-box.md)
