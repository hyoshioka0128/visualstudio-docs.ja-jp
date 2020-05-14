---
title: セキュリティおよびローカライズされたサテライト アセンブリ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- key pairs for strong-named assemblies
- strong-named assemblies, security considerations
- satellite assemblies, localized
- code signing, assemblies
- security [Visual Studio], assemblies
- strong-named assemblies, localized
- assemblies [Visual Studio], security
- localization, satellite assemblies
ms.assetid: 6d953840-b301-47d5-8d34-30c1b29b5071
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 866e313a36af5ef72f910a5eafbf7b31c971d890
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672904"
---
# <a name="security-and-localized-satellite-assemblies"></a>セキュリティおよびローカライズされたサテライト アセンブリ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

メイン アセンブリで厳密な名前付けを使用している場合、サテライト アセンブリをメイン アセンブリと同じ秘密キーで署名する必要があります。 公開キーと秘密キーのペアがメイン アセンブリとサテライト アセンブリで一致しない場合、リソースは読み込まれません。 アセンブリへの署名の詳細については、「[方法 : 厳密な名前でアセンブリに署名する](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67)」を参照してください。

 通常、組織の署名のグループまたは外部の署名機関には、秘密キーを使って署名させる必要があります。 これは、秘密キーの機密性によるもので、多くの場合、アクセスは数人のユーザーに制限されます。 開発時には遅延署名を使用することができます。 詳細については、「[アセンブリへの遅延署名](https://msdn.microsoft.com/library/9d300e17-5bf1-4360-97da-2aa55efd9070)」を参照してください。

## <a name="see-also"></a>関連項目
 [アセンブリのセキュリティに関する考慮事項 ](https://msdn.microsoft.com/library/1b5439c1-f3d5-4529-bd69-01814703d067) [Key セキュリティの概念を ](https://msdn.microsoft.com/library/3cfced4f-ea02-4e66-ae98-d69286363e98) [.NET Framework ](../ide/introduction-to-international-applications-based-on-the-dotnet-framework.md) アプリケーション [Localizing ](../ide/localizing-applications.md) とローカライズに基づいて国際対応アプリケーションに [Introduction するプログラム](../ide/globalizing-and-localizing-applications.md)
