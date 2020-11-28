---
title: '方法: ASPX マークアップをローカライズする |Microsoft Docs'
description: ハードコーディングされた文字列値を、ローカライズされたリソースを参照する式に置き換えることにより、SharePoint で ASPX マークアップをローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0a4fcf724a8ae1586354f620a68b32e9f281b545
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304663"
---
# <a name="how-to-localize-aspx-markup"></a>方法: ASPX マークアップをローカライズする
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) ページは通常、ハードコーディングされた文字列値を使用します。 これらの文字列をローカライズするには、ローカライズされたリソースを参照する式で置き換えます。

## <a name="localize-aspx-markup"></a>ASPX マークアップのローカライズ

#### <a name="to-localize-aspx-markup"></a>ASPX マークアップをローカライズするには

1. 個別のリソースファイルを追加します。1つは既定の言語用で、もう1つはローカライズされた言語ごとに1つです。

     コードではなくマークアップのみをローカライズする場合は、グローバルリソースファイルプロジェクト項目を追加します。 コードとマークアップをローカライズする場合は、[リソースファイル] プロジェクト項目を追加します。

    1. グローバルリソースファイルを追加するには、**ソリューションエクスプローラー** で、SharePoint プロジェクトアイテムのショートカットメニューを開き、[ **Add**  >  **新しいアイテム** の追加] を選択します。 [SharePoint **2010** ] ノードで、[ **グローバルリソースファイル** ] テンプレートを選択します。

    2. リソースファイルを追加するには、**ソリューションエクスプローラー** で、SharePoint プロジェクトアイテムのショートカットメニューを開き、[ **Add**  >  **新しいアイテム** の追加] を選択します。 **Visual Basic** または **Visual C#** のいずれかのノードで、[**リソースファイル**] テンプレートを選択します。

    > [!NOTE]
    > [配置の種類] プロパティを有効にするには、SharePoint プロジェクト項目にリソースファイルを追加してください。 このプロパティは、後で必要になります。 ソリューションに SharePoint プロジェクトアイテムがない場合は、空の SharePoint プロジェクトを追加して、既定の *Elements.xml* ファイルを削除できます。

2. 既定の言語リソースファイルに、MyAppResources などの *.resx* 拡張子を付加して追加した名前を付けます。 ローカライズされたリソースファイルごとに同じ基本名を使用しますが、カルチャを追加し [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] ます。 たとえば、ドイツ語のローカライズされたリソースに *MyAppResources.de* という名前を指定します。

3. 各リソースファイルの [ **展開の種類** ] プロパティの値を **appglobalresource** に変更して、サーバーの App_GlobalResources フォルダーに配置されるようにします。

4. ASPX マークアップに加えてコードをローカライズするためにリソースを使用している場合は、各ファイルの [ **ビルドアクション** ] プロパティの値を [ **埋め込みリソース**] のままにします。 リソースファイルのみを使用してマークアップをローカライズする場合は、必要に応じて、ファイルのプロパティ値を **コンテンツ** に変更できます。 詳細については、「 [SharePoint ソリューションのローカライズ](../sharepoint/localizing-sharepoint-solutions.md)」を参照してください。

5. 各リソースファイルを開き、各ファイルで同じ文字列 Id を使用して、ローカライズされた文字列を追加します。

6. [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]ASPX ページまたはコントロールのマークアップで、ハードコーディングされた文字列を、次の形式を使用する値に置き換えます。

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     たとえば、アプリケーションページのラベルコントロールのテキストをローカライズするには、次のように変更します。

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     から

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. F5 キーを **押し** て、アプリケーションをビルドして実行します。

8. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた文字列がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: フィーチャーをローカライズする](../sharepoint/how-to-localize-a-feature.md)
- [方法: リソース ファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
- [方法: コードをローカライズする](../sharepoint/how-to-localize-code.md)
