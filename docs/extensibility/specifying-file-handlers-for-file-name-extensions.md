---
title: ファイル名拡張子のファイル ハンドラを指定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af195aea09c91696843c6be42c20053bb8c095a2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699754"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>ファイル名拡張子のファイル ハンドラーを指定する
特定のファイル拡張子を持つファイルを処理するアプリケーションを決定する方法はいくつかあります。 OpenWithList 動詞と OpenWithProgids 動詞は、ファイル拡張子のレジストリ エントリの下にファイル ハンドラーを指定する 2 つの方法です。

## <a name="openwithlist-verb"></a>動詞を開く
 Windows エクスプローラでファイルを右クリックすると、[**開く**] コマンドが表示されます。 1 つの拡張機能に複数の製品が関連付けられている場合は、[**ファイルを開く**] サブメニューが表示されます。

 HKEY_CLASSES_ROOTでファイル拡張子の OpenWithList キーを設定して、拡張機能を開く別のアプリケーションを登録できます。 ファイル拡張子のこのキーの下に表示されているアプリケーションは、[**プログラムを開く**プログラム] ダイアログ ボックスの **[推奨プログラム**] の下に表示されます。 次の例は、.vcproj ファイル拡張子を開くために登録されたアプリケーションを示しています。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> アプリケーションを指定するキーは、HKEY_CLASSES_ROOT\アプリケーションの下の一覧から取得されます。

 OpenWithList キーを追加すると、別のアプリケーションが拡張機能の所有権を取得した場合でも、アプリケーションがファイル拡張子をサポートすることを宣言します。 これは、将来のバージョンのアプリケーションまたは別のアプリケーションである可能性があります。

## <a name="openwithprogids"></a>オープンウィズプログイド
 プログラム識別子 (ProgID) は、アプリケーションまたは COM オブジェクトのバージョンを識別する ClassID のわかりやすいバージョンです。 すべての共同作成可能オブジェクトは、独自の ProgID を持つ必要があります。 たとえば、VisualStudio.DTE.7.1 は、VisualStudio.DTE.10.0 が起動している間に Visual [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]Studio .NET 2003 を起動します。 プロジェクトの種類またはプロジェクト項目の種類の所有者は、ファイル拡張子のバージョン固有の ProgID を作成する必要があります。 これらの ProgID は、複数の ProgID が同じアプリケーションを起動する可能性があるという点で冗長である可能性があります。 詳細については、「[ファイル名拡張子の動詞の登録](../extensibility/registering-verbs-for-file-name-extensions.md)」を参照してください。

 バージョン対応ファイル ProgID には、他のベンダーからの登録との重複を避けるために、次の命名規則を使用します。

|[ファイル拡張子]|バージョン付きのプログ ID|
|--------------------|----------------------|
|拡張子|Productname。 拡張.バージョンメジャー.バージョンマイナー|

 バージョン対応の ProgID を値として \OpenWithProgids キー\\*\<>HKEY_CLASSES_ROOT拡張子*に追加することで、特定のファイル拡張子を開くことができるさまざまなアプリケーションを登録できます。 このレジストリ キーには、ファイル拡張子に関連付けられた代替 ProgID の一覧が含まれています。 リストされた ProgID に関連付けられているアプリケーションが、[_製品名_**で開く**] サブメニューに表示されます。 キー`OpenWithList`と`OpenWithProgids`キーの両方で同じアプリケーションが指定されている場合、オペレーティング システムは重複をマージします。

> [!NOTE]
> この`OpenWithProgids`キーは Windows XP でのみサポートされています。 他のオペレーティング システムではこのキーが無視されるため、ファイル ハンドラーの唯一の登録として使用しないでください。 このキーを使用して、Windows XP のユーザー エクスペリエンスを向上させます。

 型の値として目的の ProgID を追加REG_NONE。 次のコードは、ファイル拡張子 (.*ext)。*

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 ファイル拡張子の既定値として指定された ProgID は、既定のファイル ハンドラーです。 以前のバージョンに付属していたファイル拡張子や、他のアプリケーションが引き継がることができる[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ファイル拡張子の ProgID を変更する場合は、ファイル`OpenWithProgids`拡張子のキーを登録し、サポートしている古い ProgID と共にリストに新しい ProgID を指定する必要があります。 次に例を示します。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 古い ProgID に関連付けられた動詞がある場合、これらの動詞はショートカット メニューの *[製品名***で開く**] にも表示されます。

## <a name="see-also"></a>関連項目
- [ファイル名拡張子について](../extensibility/about-file-name-extensions.md)
- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)
