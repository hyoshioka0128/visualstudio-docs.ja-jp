---
title: Windows インストーラー展開の拡張機能を準備する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0084cfc6c08db1c1d15013362a186fec175b4ee4
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012218"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Windows インストーラー展開の拡張機能を準備する
Windows インストーラーパッケージ (MSI) を使用して VSIX パッケージを配置することはできません。 ただし、MSI の展開用に VSIX パッケージのコンテンツを抽出することはできます。 このドキュメントでは、既定の出力がセットアッププロジェクトに含める VSIX パッケージであるプロジェクトを準備する方法について説明します。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラー配置用の拡張機能プロジェクトを準備する
 セットアッププロジェクトに追加する前に、新しい拡張機能プロジェクトでこれらの手順を実行します。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラー配置用の拡張機能プロジェクトを準備するには

1. VSPackage、MEF コンポーネント、エディターの表示要素、または VSIX マニフェストを含むその他の機能拡張プロジェクトの種類を作成します。

2. コードエディターで VSIX マニフェストを開きます。

3. `InstalledByMsi`VSIX マニフェストの要素をに設定 `true` します。 VSIX マニフェストの詳細については、「 [vsix 拡張機能スキーマ2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)」を参照してください。

     これにより、VSIX インストーラーはコンポーネントをインストールしようとしません。

4. **ソリューションエクスプローラー**でプロジェクトを右クリックし、[**プロパティ**] をクリックします。

5. [ **VSIX** ] タブを選択します。

6. [ **VSIX コンテンツを次の場所にコピーする** ] チェックボックスをオンにし、セットアッププロジェクトがファイルを取得するパスを入力します。

## <a name="extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出する
 ソースファイルがない場合に既存の VSIX パッケージの内容をセットアッププロジェクトに追加するには、次の手順を実行します。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出するには

1. の名前を変更*します。**ファイル名 .vsix*から*filename.zip*への拡張子を含む vsix ファイル。

2. *.Zip*ファイルの内容をディレクトリにコピーします。

3. ディレクトリから *[Content_types] .xml* ファイルを削除します。

4. 前の手順で示したように、VSIX マニフェストを編集します。

5. 残りのファイルをセットアッププロジェクトに追加します。

## <a name="see-also"></a>関連項目
- [Visual Studio インストーラーの配置](/previous-versions/2kt85ked(v=vs.120))
- [チュートリアル: カスタム動作の作成](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))