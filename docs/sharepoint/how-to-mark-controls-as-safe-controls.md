---
title: '方法: コントロールを安全なコントロールとしてマークする |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cd7ed13504d3d91f4239a8ea070454e1c31b1114
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016258"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>方法: コントロールを安全なコントロールとしてマークする
  セキュリティを強化するために、SharePoint では、スクリプトインジェクションや Web コントロールに対して保護されている Web コントロールを区別しています。 保護されたコントロール (または*安全なコントロール*) は、信頼されていないユーザーがアクセスできます。 パッケージにアセンブリを追加するときに、SharePoint プロジェクトアイテムの "安全なコントロールエントリ" プロパティまたは**パッケージデザイナー**で、コントロールを安全としてマークできます。 詳細については、「

- [web.config ファイルの設定](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12))[は、Web パーツアセンブリを安全なコントロールとして](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))変更および登録します。

> [!IMPORTANT]
> これらの手順は、説明を目的としています。 コントロールが安全であることが確実である場合にのみ、コントロールを安全にマークします。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>安全なコントロールエントリのプロパティに安全なコントロールをマークする

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>セーフコントロールエントリのプロパティでコントロールをセーフまたは安全としてマークするには

1. 視覚的 Web パーツプロジェクトを使用して SharePoint ソリューションを作成します。

2. 2つのコントロールを Web パーツに追加します。テキストボックスとボタンです。 これらの名前はそれぞれ既定値の TextBox1 と Button1 のままにします。

3. 2つのエントリを Web パーツの "**安全なコントロールエントリ**" プロパティに追加します。 これを行うには、[**プロパティ**] ウィンドウの [**セーフコントロールエントリ**] プロパティの横にある省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックします。

     [**安全なコントロールエントリ**] ダイアログボックスが表示されます。

4. [**セーフコントロールエントリ**] ダイアログボックスで、[**追加**] ボタンを2回クリックして、[**メンバー** ] ウィンドウに2つの安全なコントロールエントリを追加します。1つはボタン用、もう1つはテキストボックス用です。

5. 最初の安全なコントロールエントリを選択してから、 **safe**プロパティの値を**False**に、 **Type Name**プロパティを**Button1**に、その**安全をスクリプトプロパティに対して** **false**に変更します。

     このステップでは、ボタンコントロールが安全でないコントロールとして識別されます。

6. 一覧で2番目のセーフコントロールエントリを選択します。 [**セーフ**] プロパティの値を [ **true** ] のままにして、[**型名**] プロパティを [ **TextBox1** ] に設定し、[**スクリプト**] プロパティを [ **true**] に設定します。

     テキストボックスコントロールは、スクリプトインジェクションに対して安全なコントロールとしてマークされるようになりました。

7. **[OK]** をクリックしてダイアログ ボックスを閉じます。

## <a name="marking-safe-controls-in-the-package-designer"></a>パッケージデザイナーでのセーフコントロールのマーク付け

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>パッケージデザイナーでコントロールを safe または unsafe としてマークするには

1. 視覚的 Web パーツプロジェクトを使用して SharePoint ソリューションを作成します。

2. 2つのコントロールを Web パーツに追加します。テキストボックスとボタンです。 これらの名前はそれぞれ既定値の TextBox1 と Button1 のままにします。

     コントロールの名前空間は、後で使用されるため、メモしておいてください。

3. メニューバーで、 **[ビルド]**[ソリューションのビルド] の順に選択し、  >  **Build Solution**プロジェクトをビルドします。

4. 別の SharePoint ソリューションを作成します。

5. **ソリューションエクスプローラー**で、*パッケージファイルの*ショートカットメニューを開き、[**開く**] をクリックして**パッケージデザイナー**を開きます。

6. **パッケージデザイナー**で、[**詳細設定**] タブを選択します。

7. [追加の**アセンブリ**] の [**追加**] ボタンをクリックし、一覧から [既存の**アセンブリの追加**] を選択します。

8. [**既存のアセンブリの追加**] ダイアログボックスで、[**ソースパス**] の横にある省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択します。

9. 手順 1. で作成した SharePoint ソリューションからアセンブリを選択し、[**開く**] をクリックします。

10. この例では、**配置ターゲット**オプションを GlobalAssemblyCache のままにします。

     この手順により、アセンブリがシステムグローバルアセンブリキャッシュ (GAC) に配置されます。 アセンブリを Web アプリケーション (Bin) フォルダーに配置する場合は、代わりにそのオプションを選択します。 詳細については、「 [SharePoint Foundation での Web パーツの配置](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))」を参照してください。

11. [**セーフコントロール**] ボックスで、 **[ここをクリックして新しい項目を追加**します] ボタンを選択します。

12. 次の表のプロパティの値を入力します。

    |プロパティ名|値|
    |-------------------|-----------|
    |名前空間|コントロールの完全修飾された名前空間 ( **BdcModelProject1**など)。|
    |種類名|ボタン 1|
    |アセンブリ名|厳密なアセンブリ名。たとえば、14.0.0.0、Culture = ニュートラル、PublicKeyToken = 71e9bce111eのように、厳密なアセンブリ名を指定します。|
    |Safe|[**セーフ**] チェックボックスをオフにします。|
    |スクリプトに対して安全|[**スクリプトに対して安全**] チェックボックスをオフのままにします。|

    > [!NOTE]
    > **パッケージデザイナー**の **[詳細設定**] タブで追加したアセンブリの**アセンブリ名**の値をトークンにすることはできません。厳密な名前のアセンブリである必要があります。 詳しくは、「[厳密な名前付きアセンブリの作成と使用](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))」をご覧ください。

13. **Tab**キーを押して、別の安全なコントロールエントリを作成します。

14. **[ここをクリックして新しい項目を追加**します] ボタンをもう一度クリックします。

15. 次の表のプロパティの値を入力します。

    |プロパティ名|値|
    |-------------------|-----------|
    |名前空間|コントロールの完全修飾された名前空間 ( **BdcModelProject1**など)。|
    |種類名|TextBox1|
    |アセンブリ名|厳密なアセンブリ名。たとえば、14.0.0.0、Culture = ニュートラル、PublicKeyToken = 71e9bce111eのように、厳密なアセンブリ名を指定します。|
    |Safe|[**セーフ**] チェックボックスをオンにします。|
    |スクリプトに対して安全|[**スクリプトに対して安全**] チェックボックスをオンにします。|

16. **Tab**キーを選択し、[ **OK** ] をクリックしてダイアログボックスを閉じます。

## <a name="see-also"></a>関連項目
- [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
