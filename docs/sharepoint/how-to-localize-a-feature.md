---
title: '方法: フィーチャーをローカライズする |Microsoft Docs'
description: ハードコーディングされた文字列値を、ローカライズされたリソースを参照する式に置き換えることにより、SharePoint で機能のタイトルと説明をローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- features [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4a3c427f207f6aac9f6a827eb6c24b799d635b46
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913601"
---
# <a name="how-to-localize-a-feature"></a>方法: フィーチャーをローカライズする
  既定では、機能のタイトルと説明はハードコーディングされた文字列値を使用します。 機能のタイトルと説明をローカライズするには、文字列を、ローカライズされたリソースを参照する式に置き換えます。

## <a name="localize-a-feature"></a>機能をローカライズする

#### <a name="to-localize-a-feature"></a>機能をローカライズするには

1. **ソリューションエクスプローラー** で、[ **feature1.feature** ] ノードのショートカットメニューを開き、[**機能リソースの追加**] を選択します。

2. [ **リソースの追加** ] ダイアログボックスで、既定の言語機能リソースファイルのカルチャとして、一覧から [ **インバリアント言語** ] を選択します。

3. ローカライズされた言語ごとに前の手順を繰り返して、ローカライズされた機能リソースファイルに対して選択した言語を選択します。

     個別の機能リソースファイルが作成されます。1つは既定の言語用で、もう1つはサポートするローカライズ言語用です。

4. リソースエディターで各リソースファイルを開き、すべての文字列 Id とその値を入力します。

     たとえば、既定の機能リソースファイルでは、" **My Feature title**" という値の **タイトル** の文字列 Id と、 **[機能の説明**] の値を示す **説明** の2番目の文字列 id を入力します。 ローカライズされたリソースファイルごとに、既定の機能リソースで使用されているのと同じ文字列 Id を使用しますが、値にはローカライズされた文字列を入力します。

5. すべてのリソース値を入力したら、機能のショートカットメニュー ( *feature1.feature* など) を開き、[ **デザイナーの表示** ] を選択してフィーチャーデザイナーで機能を開きます。

6. 機能の [ **タイトル** ] フィールドと [ **説明** ] フィールドをローカライズするには、次の書式を使用してボックスに値を入力します。

     `$Resources:` *文字列 ID*

     たとえば、[**機能タイトル**] ボックスに「$Resources:**title** 」と入力し、[**機能の説明**] ボックスに $Resources:**説明** を入力します。

     文字列 Id は、リソースファイルで使用されているものと一致している必要があります。

7. F5 キーを **押し** て、アプリケーションをビルドして実行します。

8. SharePoint で、[ **サイトの操作** ] メニューを開き、[サイトの **設定**] を選択します。次に、[ **サイトの操作** ] セクションで、[ **サイト機能の管理** ] リンクを選択します。

9. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた機能のタイトルと説明がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: リソース ファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
- [方法: ASPX マークアップをローカライズする](../sharepoint/how-to-localize-aspx-markup.md)
- [方法: コードをローカライズする](../sharepoint/how-to-localize-code.md)
