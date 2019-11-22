---
title: '[Web プロジェクト] ([オプション] ダイアログ ボックス - [プロジェクトおよびソリューション]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.WebProjects
ms.assetid: ea813046-1ae6-4c9f-9784-dc41494101b9
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5456ef4935feb2ad6f08e2a0b7ff24ad58089e1f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297872"
---
# <a name="options-dialog-box-projects-and-solutions-web-projects"></a>[Web プロジェクト] ([オプション] ダイアログ ボックス - [プロジェクトおよびソリューション])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 内での開発で Web プロジェクトによって使用される Web サーバーを設定します。 このダイアログ ボックスを表示するには、 **[ツール]** メニューの [オプション] をクリックします。 **[プロジェクトおよびソリューション]** を展開し、 **[Web プロジェクト]** をクリックします。

 既定では、(たとえば、F5 キーまたは Ctrl + F5 キーを使用して) Visual Studio で Web プロジェクトを実行すると、Visual Studio では Visual Studio 開発サーバーが使用されます。 詳細については、「 [ASP.NET Web プロジェクト用の Visual Studio の Web サーバー](https://msdn.microsoft.com/31d4f588-df59-4b7e-b9ea-e1f2dd204328)」を参照してください。

> [!NOTE]
> 使用している設定またはエディションによっては、ダイアログ ボックスで使用可能なオプションや、メニュー コマンドの名前や位置がヘルプに記載されている内容と異なる場合があります。 このヘルプ ページは、**Web 設定**を考慮して記述されています。 設定を表示または変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="settings"></a>設定
 **Use the 64-bit version of IIS Express for web sites and projects** Select this option to use IIS Express instead of the Visual Studio Development Server. 詳細については、「[Introducing IIS Express](https://weblogs.asp.net/scottgu/introducing-iis-express)」 (IIS Express の紹介) と「[IIS Express の概要](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview)」を参照してください。 既定では、このオプションは無効です。

 **Warn before running web applications when there are errors in the error list** If this box is checked, you will be warned if you try to run your web application when it does not compile  without errors.
