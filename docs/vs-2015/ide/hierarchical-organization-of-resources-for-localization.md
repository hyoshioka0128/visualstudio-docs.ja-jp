---
title: ローカリゼーション用リソースの階層編成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- resource files, localized
- localization [Visual Studio], resources
- fallback resources
- international applications [Visual Studio], storing resources
- satellite assemblies, resource hierarchies
- globalization [Visual Studio], resources
- satellite assemblies
- resources [Visual Studio], fallback system
- resource files, fallback processes
ms.assetid: dadf8f2c-f74c-44d7-bec0-a1e956d8d38d
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0a79caca18c7813605ff851eea6bda642e6300a0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645607"
---
# <a name="hierarchical-organization-of-resources-for-localization"></a>ローカリゼーション用リソースの階層編成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、ローカライズされたリソース (各カルチャに対応した文字列や画像などのデータ) は、UI カルチャの設定に従って個別のファイルに保存され、読み込まれます。 ローカライズされたリソースの読み込みの仕組みを理解するには、リソースが階層状に整理されていると考えるとわかりやすくなります。

## <a name="kinds-of-resources-in-the-hierarchy"></a>階層内のリソースの種類

- 階層の最上部には、既定のカルチャ (英語 ("en") など) のフォールバック リソースが配置されています。 これは独自のファイルを持たない唯一のリソースであり、メイン アセンブリに格納されています。

- フォールバック リソースの下には、ニュートラル カルチャのリソースがあります。 ニュートラル カルチャは、言語に関連付けられ、国や地域には関連付けられません。 たとえば、フランス語 ("fr") はニュートラル カルチャです (フォールバック リソースもニュートラル カルチャのリソースですが、特別なものであることに注意してください)。

- これらの下に、具体的なカルチャのリソースがあります。 具体的なカルチャは、言語および国/地域に関連付けられます。 たとえば、カナダ系フランス語 ("fr-CA") は、具体的なカルチャです。

  アプリケーションがローカライズされたリソース (文字列など) を読み込もうとして見つけられなかった場合、要求されたリソースを含むリソース ファイルが見つかるまで上の階層へと移動します。

  リソースを保存する最も良い方法は、できる限り汎用化することです。 つまり、可能であれば、具体的なカルチャではなくニュートラル カルチャのリソース ファイル内にローカライズされた文字列や画像を保存するということです。 たとえば、ベルギー系フランス語 ("fr-BE") カルチャのリソースがあり、そのすぐ上のリソースが英語のフォールバック リソースであるシステムのアプリケーションがあるとします。このアプリケーションを、別のユーザーがカナダ系フランス語のカルチャで構成されたシステムで開くと、問題が発生する可能性があります。 システムは "fr-CA" のサテライト アセンブリを検索しますが見つからないため、フランス語のリソースではなく、フォールバック リソース (この場合は英語) が含まれるメイン アセンブリを読み込みます。 次の図に、こうした好ましくないシナリオを示します。

  ![特定のリソースのみ](../ide/media/vbspecificresourcesonly.gif "Vb固有の Resourcesonly")

  推奨方法に従って "fr" カルチャのニュートラル リソース ファイル内にできる限り多くのリソースを配置した場合、カナダ系フランス語ユーザーに "fr-BE" カルチャ用のリソースは表示されませんが、文字列はフランス語で表示されます。 次の状況は、この推奨シナリオを示しています。

  ![NeutralSpecificResources グラフィック](../ide/media/vbneutralspecificresources.gif "vbNeutralSpecificResources")

## <a name="see-also"></a>参照
 ローカライズされた[リソース言語ローカリゼーション](../ide/neutral-resources-languages-for-localization.md)[セキュリティおよびローカライズされたサテライトアセンブリ](../ide/security-and-localized-satellite-assemblies.md)[アプリケーションのローカライズアプリケーション](../ide/localizing-applications.md)の[グローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)[方法: Windows フォームのカルチャと UI カルチャを設定するグローバリゼーション](https://msdn.microsoft.com/694e049f-0b91-474a-9789-d35124f248f0)[方法: ASP.NET Web ページのグローバリゼーション用のカルチャおよび UI カルチャを設定する](https://msdn.microsoft.com/library/76091f86-f967-4687-a40f-de87bd8cc9a0)
