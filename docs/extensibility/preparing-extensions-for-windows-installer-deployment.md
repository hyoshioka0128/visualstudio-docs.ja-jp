---
title: Windows インストーラの展開用の拡張機能を準備する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8636dfbbad06192e5edbb61a9a784f64b8f3f14f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702022"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Windows インストーラの展開用の拡張機能を準備する
Windows インストーラー パッケージ (MSI) を使用して VSIX パッケージを展開することはできません。 ただし、MSI 展開用の VSIX パッケージの内容を抽出できます。 このドキュメントでは、既定の出力がセットアップ プロジェクトに含める VSIX パッケージであるプロジェクトを準備する方法を示します。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーの展開用の拡張プロジェクトを準備する
 セットアップ プロジェクトに追加する前に、新しい拡張プロジェクトに対してこれらの手順を実行します。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーの展開用の拡張機能プロジェクトを準備するには

1. VsPackage、MEF コンポーネント、エディター表示要素、または VSIX マニフェストを含むその他の機能拡張プロジェクトの種類を作成します。

2. コード エディターで VSIX マニフェストを開きます。

3. VSIX`InstalledByMsi`マニフェストの要素を に`true`設定します。 VSIX マニフェストの詳細については[、VSIX 拡張スキーマ 2.0 のリファレンスを参照](../extensibility/vsix-extension-schema-2-0-reference.md)してください。

     これにより、VSIX インストーラーがコンポーネントをインストールすることを防ぎます。

4. **ソリューション エクスプローラ**でプロジェクトを右クリックし、[**プロパティ**] をクリックします。

5. **[VSIX]** タブを選択します。

6. **[VSIX コンテンツを次の場所にコピー**する] というラベルの付いたチェック ボックスをオンにし、セットアップ プロジェクトがファイルを取得するパスを入力します。

## <a name="extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出する
 ソース ファイルがない場合に、既存の VSIX パッケージのコンテンツをセットアップ プロジェクトに追加するには、次の手順を実行します。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出するには

1. の名前を変更*します。**ファイル名.vsix からファイル名.zip*までの拡張子を含む VSIX*ファイル*。

2. *zip*ファイルの内容をディレクトリにコピーします。

3. ディレクトリから *[Content_types].xml*ファイルを削除します。

4. 前の手順に示すように、VSIX マニフェストを編集します。

5. 残りのファイルをセットアップ プロジェクトに追加します。

## <a name="see-also"></a>関連項目
- [インストーラーの配置](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)
- [チュートリアル: カスタム アクションを作成する](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))
