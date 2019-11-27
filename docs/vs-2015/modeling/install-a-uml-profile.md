---
title: UML プロファイルをインストールする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, profiles
ms.assetid: 586f9ba5-4d01-4a1d-b001-32e2efaa4f24
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 14911cda4cfc2be5fece6005a879427c10529bbc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298906"
---
# <a name="install-a-uml-profile"></a>UML プロファイルのインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML プロファイルを使用して Visual Studio を拡張できます。 プロファイルを使用すると、UML モデルで生成できる要素に、ステレオタイプおよびプロパティを追加できます。 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 プロファイルを使用して生成された UML モデルを受け取った場合、同じプロファイルをインストールしていなければ、一部のプロパティは表示されません。

 プロファイルは、Visual Studio 拡張機能の中で配布されます。 拡張機能には、メニュー コマンドなどの他の機能も含まれる場合があります。 詳細については、「 [Visual Studio 拡張機能の管理](https://go.microsoft.com/fwlink/?LinkId=160728)」を参照してください。

### <a name="to-install-a-uml-profile-on-your-computer"></a>UML プロファイルをコンピューターにインストールするには

1. プロファイルは、Visual Studio 拡張機能ファイル (`.vsix`) 形式で提供されます。 このファイル内には、これ以外の機能も含まれている場合があります。

     `.vsix` ファイルを、コンピューターの任意の場所に移動します。

2. Windows エクスプローラー (またはエクスプローラー) で `.vsix` ファイルをダブルクリックするか、このファイルを [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 内で開きます。

3. 表示されるダイアログボックスで **[インストール]** をクリックします。

4. 拡張機能をアンインストールするか、一時的に無効にするには、 **[ツール]** メニューの **[拡張機能マネージャー]** を開きます。

### <a name="to-uninstall-or-disable-a-profile-extension"></a>プロファイルの拡張機能をアンインストールまたは無効にするには

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能マネージャー]** をクリックします。

2. 削除する拡張機能をクリックし、 **[無効化]** または **[アンインストール]** をクリックします。

## <a name="see-also"></a>関連項目
 プロファイル[とステレオタイプを使用してモデルをカスタマイズ](../modeling/customize-your-model-with-profiles-and-stereotypes.md)[するプロファイルを定義して UML を拡張する](../modeling/define-a-profile-to-extend-uml.md)
