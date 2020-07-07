---
title: '方法: コードをローカライズする |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6c1963ff0b6ef317dfa1a2c8154a1628710dc562
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016685"
---
# <a name="how-to-localize-code"></a>方法: コードをローカライズする
  ローカライズされていないコードでは、ハードコーディングされた文字列値が使用されています。 コードの文字列をローカライズするには、それらを <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> の呼び出しに置き換えます。このメソッドは、ローカライズされたリソースを参照します。

## <a name="localize-code"></a>コードのローカライズ

#### <a name="to-localize-code"></a>コードをローカライズするには

1. **ソリューションエクスプローラー**で、プロジェクト項目のショートカットメニューを開き、[モジュールの**追加**] を選択し  >  **Module**ます。

     [**リソースファイル**] テンプレートを選択します。

    > [!NOTE]
    > Deployment Type プロパティを使用できるように、SharePoint プロジェクト項目にリソース ファイルを必ず追加します。 このプロパティは、後で必要になります。

2. 既定の言語リソースファイルに、 *MyAppResources*などの *.resx*拡張子を付加して追加した名前を付けます。

3. ローカライズ言語ごとに手順 1. と 2. を繰り返して、SharePoint プロジェクト項目にそれぞれのリソース ファイルを追加します。

     ローカライズされた各リソース ファイルに対しては、同じ基本名にカルチャ ID を加えた名前を使用します  たとえば、ドイツ語のローカライズされたリソースに*MyAppResources.de*という名前を指定します。

4. 各リソース ファイルを開いて、ローカライズされた文字列を追加します。 各ファイルで同じ文字列 ID を使用します。

5. 各リソースファイルの [**展開の種類**] プロパティの値を**appglobalresource**に変更すると、各ファイルがサーバーの App_GlobalResources フォルダーに配置されます。

6. 各ファイルの "**ビルドアクション**" プロパティの値は、**埋め込みリソース**としてそのままにします。

     埋め込みリソースはプロジェクトの DLL にコンパイルされます。

7. プロジェクトをビルドして、リソースのサテライト DLL を作成します。

8. **パッケージデザイナー**で [**詳細設定**] タブを選択し、サテライトアセンブリを追加します。

9. [**場所**] ボックスで、" *de \\ \<Project Item Name>.resources.dll*" などの場所のパスにカルチャ ID フォルダーを付加します。

10. ソリューションで System.Web アセンブリがまだ参照されていない場合は System.Web アセンブリへの参照を追加し、<xref:System.Web> に対するディレクティブをコードに追加します。

11. UI テキスト、エラー、メッセージ テキストなど、ユーザーへの表示用にコード内でハードコーディングされている文字列をすべて見つけます。 それらの文字列を、次の構文を使用する <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> メソッドの呼び出しに置き換えます。

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. F5 キーを**押し**て、アプリケーションをビルドして実行します。

13. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた文字列がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのローカライズ](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: フィーチャーをローカライズする](../sharepoint/how-to-localize-a-feature.md)
- [方法: ASPX マークアップをローカライズする](../sharepoint/how-to-localize-aspx-markup.md)
- [方法: リソースファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
