---
title: メニュー コマンドにアイコンを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f4b71f981472451766f526cf62e975e571cf46da
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740156"
---
# <a name="add-icons-to-menu-commands"></a>メニュー コマンドにアイコンを追加する
コマンドは、メニューとツールバーの両方に表示できます。 ツールバーでは、コマンドはアイコンだけで表示されるのが一般的ですが(スペースを節約するために)、メニューでは通常、コマンドはアイコンとテキストの両方で表示されます。

 アイコンは幅 16 ピクセル、高さ 16 ピクセルで、8 ビットの色深度 (256 色) または 32 ビットの色深度 (トゥルー カラー) のいずれかです。 32 ビットカラーアイコンが推奨されます。 アイコンは通常、1 つのビットマップ内の単一の水平行に配置されますが、複数のビットマップを使用できます。 このビットマップは、ビットマップで使用できる個々のアイコンと共に *.vsct*ファイルで宣言されます。 詳細については[、Bitmaps 要素](../extensibility/bitmaps-element.md)のリファレンスを参照してください。

## <a name="add-an-icon-to-a-command"></a>コマンドにアイコンを追加する
 次の手順では、メニュー コマンドを使用して既存の VSPackage プロジェクトがあることを前提としています。 これを行う方法については、[メニュー コマンドを使用して拡張機能を作成するを](../extensibility/creating-an-extension-with-a-menu-command.md)参照してください。

1. 32 ビットの色深度のビットマップを作成します。 アイコンは常に 16 x 16 であるため、このビットマップは高さ 16 ピクセル、幅 16 ピクセルの倍数である必要があります。

     各アイコンは、1 行の間で、ビットマップ上に並んだ位置に配置されます。 アルファ チャネルを使用して、各アイコンの透明度の場所を示します。

     8 ビットの色深度を使用する場合は、透明度として`RGB(255,0,255)`マゼンタ、を使用します。 ただし、32 ビットのカラー アイコンが推奨されます。

2. アイコン ファイルを VSPackage プロジェクトの*リソース*ディレクトリにコピーします。 ソリューション**エクスプローラ**で、アイコンをプロジェクトに追加します。 (**リソース**を選択し、コンテキスト メニューで [**追加**] をクリックし、[**既存の項目**] をクリックして、アイコン ファイルを選択します。

3. エディターで *.vsct*ファイルを開きます。

4. 名前が`GuidSymbol` **testIcon**の要素を追加します。 GUID (**ツール** > **作成 GUID**) を作成し、[**レジストリ形式**] を選択`value`して [**コピー**] をクリックし、属性に貼り付けます。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. アイコンの`<IDSymbol>`を追加します。 属性`name`はアイコンの ID で、ストリップ上`value`の位置を示します (ある場合)。 アイコンが 1 つだけの場合は、1 を追加します。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. アイコンを`<Bitmap>``<Bitmaps>`含むビットマップを表す *.vsct*ファイルのセクションに を作成します。

    - 前の`guid`手順で作成した`<GuidSymbol>`要素の名前を値に設定します。

    - 値を`href`ビットマップ ファイルの相対パスに設定します (この場合**は\\リソース<\>アイコン ファイル名**)。

    - 前に`usedList`作成した ID シンボルに値を設定します。 この属性は、VSPackage で使用されるアイコンのコンマ区切りのリストを指定します。 リストにないアイコンは、フォームのコンパイルを除外します。

         ビットマップ ブロックは次のようになります。

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. 既存`<Button>`の要素で、前に`Icon`作成した GUID シンボルと IDSymbol の値を要素に設定します。 これらの値を持つ Button 要素の例を次に示します。

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

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [VSCT XML スキーマ リファレンス](../extensibility/vsct-xml-schema-reference.md)
