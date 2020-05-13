---
title: '方法: Visual Studio 2015 の展開時にプロダクト キーを自動的に適用する | Microsoft Docs'
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
ms.assetid: d79260be-6234-4fd3-89b5-a9756b4a93c1
caps.latest.revision: 11
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ec050cf8f365bfae2290593a0c7f215dcb2f39cc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185999"
---
# <a name="how-to-automatically-apply-product-keys-when-deploying-visual-studio"></a>方法: Visual Studio の展開時にプロダクト キーを自動的に適用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio に関する最新のドキュメントについては、「[Visual Studio の展開時にプロダクト キーを自動的に適用する](/visualstudio/install/automatically-apply-product-keys-when-deploying-visual-studio)」をご覧ください。

Visual Studio 2015 の配置を自動化するために使用されるスクリプトの一部として、プログラム的にプロダクト キーを適用することができます。 プロダクト キーは、Visual Studio のインストール中またはインストール完了後に、プログラム的にデバイスで設定できます。

## <a name="apply-the-license-during-installation"></a>インストール中にライセンスを適用する
 Visual Studio のセットアップ プロセス中にプロダクト キーを適用するには、/ProductKey パラメーターを使用します。 既にエンドユーザーにライセンスが付与されている状態で Visual Studio をインストールする場合は、このセットアップ パラメーターを /Silent パラメーターとともに使用できます。 /ProductKey パラメーターを使用するには、コマンド プロンプトを開きます。 セットアップ プログラム (例: vs_enterprise.exe や vs_professional.exe) を実行し、ダッシュが含まれていないプロダクト キー (25 文字) を指定して /ProductKey パラメーターを設定します。

 以下に例として、プロダクト キー AAAAABBBBBCCCCCDDDDDEEEEEEE を指定して Visual Studio 2015 Enterprise をインストールする場合のコマンドを示します。

 `vs_enterprise.exe [any other setup parameters] /ProductKey AAAAABBBBBCCCCCDDDDDDEEEEEE`

## <a name="apply-the-license-after-installation"></a>インストール後にライセンスを適用する
 ターゲット コンピューターにある storePID.exe ユーティリティをサイレント モードで使用して、インストールされているバージョンの Visual Studio をプロダクト キーでアクティブにすることができます。 StorePID.exe はユーティリティ プログラムで、Visual Studio で以下にインストールされます。 **\<ドライブ>:\\\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\StorePID.exe**

 System Center エージェントまたは管理者特権でのコマンド プロンプトのいずれかを使用することにより、昇格された特権で storePID.exe を実行します。その際、プロダクト キー (ダッシュを含む) と Microsoft 製品コード (MPC) を後ろに付けます。 プロダクト キーには必ずダッシュ (-) を含めます。

 `StorePID.exe [product key including the dashes] [MPC]`

 プロダクト キー「AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE」を指定して、MPC が 07060 の Visual Studio 2015 Enterprise をインストールするコマンド ラインの例を次に示します。

 `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\StorePID.exe AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 07060`

 次の表に、Visual Studio の各エディションの MPC コードを一覧します。

|Visual Studio エディション|MPC|
|---------------------------|---------|
|Visual Studio Enterprise 2015|07060|
|Visual Studio Professional 2015|07062|
|Visual Studio Test Professional 2015|07066|
|Visual Studio Ultimate 2013|06181|
|Visual Studio Premium 2013|06191|
|Visual Studio Professional 2013|06177|
|Visual Studio Test Professional 2013|06194|

プロダクト キーの取得方法の詳細については、「[How to: Locate the Visual Studio Product Key (方法: Visual Studio プロダクト キーを見つける)](../install/how-to-locate-the-visual-studio-product-key.md)」を参照してください。

StorePID.exe が正常にプロダクト キーを適用した場合は 0 を返します。 エラーが検出された場合は、1 ～ 6 の範囲の数値を返します。

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール](../install/install-visual-studio-2015.md)