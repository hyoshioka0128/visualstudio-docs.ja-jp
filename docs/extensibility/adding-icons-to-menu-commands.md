---
title: メニューコマンドにアイコンを追加する |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のメニューとツールバーの両方に表示されるコマンドにアイコンを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 01f159b9f07cd0d530039e0d5707cf38d51610ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097591"
---
# <a name="add-icons-to-menu-commands"></a>メニューコマンドにアイコンを追加する
コマンドは、メニューとツールバーの両方に表示できます。 ツールバーでは、コマンドがアイコンだけで表示されるのが一般的です (領域を節約するため)。メニュー上では、通常、コマンドにはアイコンとテキストの両方が表示されます。

 アイコンは幅16ピクセル、高さ16ピクセル、8ビットの色深度 (256 色) または32ビットの色深度 (true color) のいずれかになります。 32ビットカラーアイコンが優先されます。 アイコンは通常、1つのビットマップ内の1つの水平行に配置されますが、複数のビットマップが許可されます。 このビットマップは、 *vsct* ファイルで、ビットマップで使用可能な個々のアイコンと共に宣言されます。 詳細については、「 [ビットマップ要素](../extensibility/bitmaps-element.md) のリファレンス」を参照してください。

## <a name="add-an-icon-to-a-command"></a>コマンドにアイコンを追加する
 次の手順では、既存の VSPackage プロジェクトにメニューコマンドがあることを前提としています。 これを行う方法については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

1. 32ビットの色深度でビットマップを作成します。 アイコンは常に 16 x 16 であるため、このビットマップの高さは16ピクセル、幅16ピクセルにする必要があります。

     各アイコンは、1行に隣接するビットマップの横に配置されます。 各アイコンの透明度を示すには、アルファチャネルを使用します。

     8ビットの色深度を使用する場合は、 `RGB(255,0,255)` 透明度としてマゼンタを使用します。 ただし、32ビットのカラーアイコンを使用することをお勧めします。

2. アイコンファイルを VSPackage プロジェクトの *Resources* ディレクトリにコピーします。 **ソリューションエクスプローラー** で、プロジェクトにアイコンを追加します。 ([ **リソース**] を選択し、コンテキストメニューの [ **追加**]、[ **既存の項目**] の順にクリックして、アイコンファイルを選択します)。

3. エディターで、 *vsct* ファイルを開きます。

4. `GuidSymbol` **Testicon** という名前の要素を追加します。 Guid を作成し  >  ます ([ツール] [**guid の作成**] を選択し、[**レジストリ形式**] を選択して [**コピー**] をクリックします)。次に、属性に貼り付け `value` ます。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. `<IDSymbol>`アイコンのを追加します。 `name`属性はアイコンの ID で、は `value` ストリップ上での位置を示します (存在する場合)。 アイコンが1つしかない場合は、1を追加します。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. `<Bitmap>` `<Bitmaps>` *. Vsct* ファイルのセクションにを作成し、アイコンを含むビットマップを表します。

    - `guid`値を、前の手順で作成した要素の名前に設定し `<GuidSymbol>` ます。

    - `href`この値は、ビットマップファイルの相対パス (この場合は **リソース \\<アイコンファイル名 \>**) に設定します。

    - 前の手順で作成した `usedList` IDSymbol に値を設定します。 この属性は、VSPackage で使用するアイコンのコンマ区切りリストを指定します。 リストにないアイコンは、フォームのコンパイルを除外します。

         Bitmap ブロックは次のようになります。

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. 既存の要素で、要素を、前に作成した `<Button>` `Icon` Guidsymbol と idsymbol の値に設定します。 これらの値を持つ Button 要素の例を次に示します。

    ```xml
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />
        <Icon guid="testIcon" id="testIcon1" />
        <Strings>
            <ButtonText>My Command name</ButtonText>
        </Strings>
    </Button>
    ```

8. アイコンをテストします。 プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスで、コマンドを見つけます。 追加したアイコンが表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [VSCT XML スキーマリファレンス](../extensibility/vsct-xml-schema-reference.md)
