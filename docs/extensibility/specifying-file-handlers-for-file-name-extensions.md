---
title: ファイル名拡張子のファイルハンドラーの指定 |Microsoft Docs
description: OpenWithList と Openwithlist を使用して、Visual Studio SDK でファイル拡張子を処理するアプリケーションを特定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d897cb9bb4697a687bd06eeb02c779e133090e33
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99848098"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>ファイル名拡張子のファイル ハンドラーを指定する
特定のファイル拡張子を持つファイルを処理するアプリケーションを特定するには、いくつかの方法があります。 OpenWithList と Openwithlist 動詞は、ファイル拡張子のレジストリエントリの下にファイルハンドラーを指定する2つの方法があります。

## <a name="openwithlist-verb"></a>OpenWithList 動詞
 エクスプローラーでファイルを右クリックすると、[ **開く** ] コマンドが表示されます。 複数の製品が拡張機能に関連付けられている場合は、 **[ファイルを開くアプリケーションの** 作成] サブメニューが表示されます。

 HKEY_CLASSES_ROOT でファイル拡張子の OpenWithList キーを設定することによって、拡張機能を開くさまざまなアプリケーションを登録できます。 このキーの下に一覧表示されるファイル拡張子のアプリケーションは、[プログラムから **開く**] ダイアログボックスの [**推奨プログラム**] 見出しの下に表示されます。 次の例は、.vcproj ファイル拡張子を開くために登録されているアプリケーションを示しています。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> アプリケーションを指定するキーは、HKEY_CLASSES_ROOT\Applications の下の一覧にあります。

 OpenWithList キーを追加することにより、別のアプリケーションが拡張機能の所有権を取得した場合でも、アプリケーションでファイル拡張子がサポートされるように宣言します。 これは、アプリケーションまたは別のアプリケーションの将来のバージョンである可能性があります。

## <a name="openwithprogids"></a>OpenWithProgIDs
 プログラム識別子 (Progid) は、アプリケーションまたは COM オブジェクトのバージョンを識別する、Classid のフレンドリバージョンです。 すべての共同作成可能なオブジェクトには、独自の ProgID が必要です。 たとえば、VisualStudio は、VisualStudio の開始時に Visual Studio .NET 2003 を起動します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトの種類またはプロジェクト項目の種類の所有者は、ファイル拡張子のバージョン固有の ProgID を作成する必要があります。 これらの progid は、複数の ProgID が同じアプリケーションを起動する可能性があるため、冗長である場合があります。 詳細については、「 [ファイル名拡張子に対する動詞の登録](../extensibility/registering-verbs-for-file-name-extensions.md)」を参照してください。

 他のベンダーからの登録と重複しないように、バージョン管理されたファイルの Progid には次の名前付け規則を使用します。

|[ファイル拡張子]|バージョン付きの ProgID|
|--------------------|----------------------|
|. 拡張子|同様. 拡張子. versionMajor. Versionmajor|

 バージョン管理された Progid を値として HKEY_CLASSES_ROOT \\ \ openwithprogid キーに追加することで、特定のファイル拡張子を開くことができるさまざまなアプリケーションを登録でき *\<extension>* ます。 このレジストリキーには、ファイル拡張子に関連付けられている別の Progid の一覧が含まれています。 表示されている Progid に関連付けられているアプリケーションは、[_製品名_ を指定し **て開く**] サブメニューに表示されます。 との両方のキーに同じアプリケーションが指定されている場合、 `OpenWithList` `OpenWithProgids` オペレーティングシステムは重複部分をマージします。

> [!NOTE]
> この `OpenWithProgids` キーは、WINDOWS XP でのみサポートされています。 このキーは他のオペレーティングシステムでは無視されるため、ファイルハンドラーの唯一の登録として使用しないでください。 Windows XP でのユーザーエクスペリエンスを向上させるには、このキーを使用します。

 REG_NONE 型の値として、必要な Progid を追加します。 次のコードは、ファイル拡張子 () の Progid を登録する例を示しています。*ext*)。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 ファイル拡張子の既定値として指定された ProgID が既定のファイルハンドラーです。 以前のバージョンのまたは他のアプリケーションで使用できるファイル拡張子の ProgID を変更する場合は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、 `OpenWithProgids` ファイル拡張子のキーを登録し、サポートする古い progid と共に一覧で新しい progid を指定する必要があります。 次に例を示します。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 古い ProgID に動詞が関連付けられている場合は、ショートカットメニューの [*製品名* を指定し **て開く**] にも、これらの動詞が表示されます。

## <a name="see-also"></a>関連項目
- [ファイル名拡張子について](../extensibility/about-file-name-extensions.md)
- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)
