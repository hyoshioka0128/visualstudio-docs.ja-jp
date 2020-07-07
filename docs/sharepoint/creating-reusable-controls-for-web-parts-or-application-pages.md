---
title: Web パーツまたはアプリケーションページの再利用可能なコントロールを作成する |Microsoft Docs
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
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015135"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>Web パーツまたはアプリケーションページの再利用可能なコントロールを作成する
  Visual Studio では、SharePoint で実行されるアプリケーションページと Web パーツで使用できる、再利用可能なカスタムコントロールを作成できます。 これらのコントロールは、ユーザーコントロールと呼ばれます。 ユーザーコントロールは、ASP.NET Web ページと同様に動作する複合コントロールの一種です。既存の Web サーバーコントロールやマークアップをユーザーコントロールに追加し、コントロールのプロパティとメソッドを定義することができます。 その後、それらを1つの単位として機能する ASP.NET Web ページに埋め込むことができます。

## <a name="create-a-user-control"></a>ユーザーコントロールを作成する
 ユーザーコントロールを作成するには、**空の SharePoint プロジェクト**に**ユーザーコントロール**を追加します。 詳細については、「[方法: SharePoint アプリケーションページまたは web パーツのユーザーコントロールを作成](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)する」を参照してください。

 **ユーザーコントロール**項目を追加すると、Visual Studio によってプロジェクトにフォルダーが作成され、フォルダーに複数のファイルが追加されます。 各ファイルの説明を次の表に示します。

|ファイル|説明|
|----------|-----------------|
|ユーザーコントロールファイル|ユーザーコントロールを定義します。 このファイルにコントロールとマークアップを追加して、ユーザーコントロールをデザインします。|
|コードファイル|ユーザーコントロールの背後にあるコードを格納します。 このファイルのイベントを処理するコードを追加します。|
|デザイナーコードファイル|デザイナーによって生成されるコードが含まれており、直接編集することはできません。|

## <a name="design-the-user-control"></a>ユーザーコントロールをデザインする
 Visual Studio の Visual Web Developer デザイナーを使用して、ユーザーコントロールをデザインします。 このデザイナーは、プロジェクトでユーザーコントロールファイルを開き、[**デザイン**] タブをクリックすると表示されます。

## <a name="consume-the-user-control"></a>ユーザーコントロールを使用する
 ユーザーコントロールは、アプリケーションページまたは Web パーツに含めるまでは SharePoint に表示されません。

 アプリケーションページにユーザーコントロールを含めるには、ASP.NET ユーザーコントロールを追加する Web ページを開きます。 デザインビューに切り替え、ソリューションエクスプローラーでカスタムユーザーコントロールファイルを選択して、ページにドラッグします。 ASP.NET ユーザーコントロールがページに追加され、デザイナーによって @ Register ディレクティブが作成されます。このディレクティブは、ページがユーザーコントロールを認識するために必要です。 これで、コントロールのパブリックプロパティとメソッドを操作できるようになりました。

 ユーザーコントロールを web パーツに含めるには、web パーツのコードファイルの Web パーツコレクションにユーザーコントロールを追加し <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> ます。 次の例では、Web パーツのコレクションにユーザーコントロールを追加し <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> ます。

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>ユーザーコントロールをデバッグする
 ユーザーコントロールをデバッグするには、SharePoint プロジェクトのアプリケーションページまたは Web パーツにユーザーコントロールが含まれていることを確認します。 次に、Visual Studio プロジェクトでコードをデバッグするのと同じように、ユーザーコントロールのコードをデバッグできます。

 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 SharePoint で、ユーザーコントロールを含むアプリケーションページを開きます。 ユーザーコントロールが Web パーツに含まれている場合は、SharePoint の web パーツページに Web パーツを追加します。

 SharePoint プロジェクトのデバッグの詳細については、「 [sharepoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|[説明]|
|-----------|-----------------|
|[方法: SharePoint アプリケーションページまたは web パーツのユーザーコントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|SharePoint で実行されるアプリケーションページと Web パーツで使用できる、再利用可能なカスタムコントロールを作成する方法について説明します。|
