---
title: Web パーツまたはアプリケーション ページの再利用できるコントロールの作成 | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- SharePoint development in Visual Studio, user controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b174e1e16802838f19cec6dce727ea3199df730f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015135"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する
  Visual Studio では、SharePoint で実行されるアプリケーション ページと Web パーツで使用できる、再利用可能なカスタム コントロールを作成できます。 これらのコントロールは、ユーザー コントロールと呼ばれます。 ユーザー コントロールは、ASP.NET Web ページと同様に動作する一種の複合コントロールです。既存の Web サーバー コントロールやマークアップをユーザー コントロールに追加し、コントロールのプロパティとメソッドを定義することができます。 その後、それらを ASP.NET Web ページに埋め込むと、1 つの単位として機能します。

## <a name="create-a-user-control"></a>ユーザー コントロールを作成する
 ユーザー コントロールを作成するには、**空の SharePoint プロジェクト**に**ユーザー コントロール**を追加します。 詳細については、「[方法:SharePoint アプリケーション ページまたは Web パーツのユーザー コントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)」を参照してください。

 **ユーザー コントロール**項目を追加すると、Visual Studio によってプロジェクトにフォルダーが作成され、そのフォルダーにいくつかのファイルが追加されます。 各ファイルの説明を次の表に示します。

|ファイル|説明|
|----------|-----------------|
|ユーザー コントロール ファイル|ユーザー コントロールを定義します。 このファイルにコントロールとマークアップを追加して、ユーザー コントロールをデザインします。|
|コード ファイル|ユーザー コントロールの背後にあるコードを格納します。 このファイルには、イベントを処理するコードを追加します。|
|デザイナー コード ファイル|デザイナーによって生成されるコードを格納します。直接編集することはできません。|

## <a name="design-the-user-control"></a>ユーザー コントロールをデザインする
 Visual Studio の Visual Web Developer デザイナーを使用してユーザー コントロールをデザインします。 このデザイナーは、プロジェクトでユーザー コントロール ファイルを開き、 **[デザイン]** タブをクリックすると表示されます。

## <a name="consume-the-user-control"></a>ユーザー コントロールを使用する
 ユーザー コントロールは、アプリケーション ページまたは Web パーツに含めるまでは SharePoint に表示されません。

 アプリケーション ページにユーザー コントロールを含めるには、ASP.NET ユーザー コントロールを追加する Web ページを開きます。 デザイン ビューに切り替え、ソリューション エクスプローラーでカスタム ユーザー コントロール ファイルを選択して、ページにドラッグします。 ASP.NET ユーザー コントロールがページに追加され、デザイナーによって @ Register ディレクティブが作成されます。これは、ページがユーザー コントロールを認識するために必要です。 これで、コントロールのパブリック プロパティおよびメソッドを操作できるようになりました。

 Web パーツにユーザー コントロールを追加するには、Web パーツ コード ファイルの Web パーツ <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> コレクションにユーザー コントロールを追加します。 次の例では、Web パーツの <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> コレクションにユーザー コントロールを追加します。

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>ユーザー コントロールをデバッグする
 ユーザー コントロールをデバッグするには、SharePoint プロジェクトのアプリケーション ページまたは Web パーツにユーザー コントロールが含まれていることを確認します。 次に、Visual Studio プロジェクトでコードをデバッグするのと同じように、ユーザー コントロールのコードをデバッグできます。

 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 SharePoint で、ユーザー コントロールを含むアプリケーション ページを開きます。 ユーザー コントロールが Web パーツに含まれている場合は、SharePoint の Web パーツ ページに Web パーツを追加します。

 SharePoint プロジェクトのデバッグの詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: SharePoint アプリケーション ページまたは Web パーツのユーザー コントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|SharePoint で実行されるアプリケーション ページと Web パーツで使用できる、再利用可能なカスタム コントロールを作成する方法について説明します。|
