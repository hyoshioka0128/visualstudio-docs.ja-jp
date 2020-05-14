---
title: グリフ管理 (ソース管理 VS パッケージ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9db1b4542eae293e39cda674fac3eb984aa77d3e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708316"
---
# <a name="glyph-control-source-control-vspackage"></a>グリフ管理 (ソース管理 VSPackage)
ソース管理 VSPackages で使用できる深い統合の一部は、ソース管理下の項目の状態を示すために独自のグリフを表示する機能です。

## <a name="levels-of-glyph-control"></a>グリフ コントロールのレベル
 状態グリフは、**たとえばソリューション エクスプローラ**や**クラス ビュー**などで表示されたときの項目の現在の状態を示すアイコンです。 ソース管理 VSPackage は、グリフコントロールの 2 つのレベルを実行できます。 このオプションを使用すると、IDE で提供される定義済みのグリフセットにグリフの選択[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を制限したり、表示するグリフのカスタムセットを定義したりできます。

### <a name="default-set-of-glyphs"></a>グリフのデフォルトセット
 **ソリューション エクスプローラ**の項目に関連付けられている状態グリフを決定するために、プロジェクトは、 を使用してソース管理から状態<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A>グリフを要求します。 ソース管理 VSPackage は、IDE によって提供される定義済みのグリフに限定されたグリフの選択を維持することを決定する場合があります。 この場合、VSPackage は*vsshell.idl*で定義されているグリフ列挙を表す値の配列を返します。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>」を参照してください。 これは、チェックインされたグリフの南京錠やチェック アウトグリフのチェック マークなど、IDE によって設定された定義済みのグリフのセットです。

### <a name="custom-set-of-glyphs"></a>グリフのカスタムセット
 ソース 管理 VSPackage は、独自のグリフを使用して、インストール時に一意の外観と感触を得ることができます。 新しいソース管理 VSPackage がアクティブな場合は、以前のソース 管理の VSPackage がまだ読み込まれているが非アクティブな場合でも、独自のグリフを使用して開始できる必要があります。 このモードでは、ソース管理 VSPackage は、既存のアイコンを使用して、選択[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]した場合に一貫性のある外観を維持できます。

 この<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>サービスは、VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>がオプションで実装でき、IDE によって求められるインターフェイスをサポートします。 IDE が要求を行うと[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、現在登録されているソース管理 VSPackage からこのインターフェイスを取得しようとします。 インターフェイスが登録済み VSPackage に存在する場合、IDE のカスタム グリフの要求は成功します。それ以外の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]場合、IDE はデフォルトのグリフセットを使用します。

 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A>メソッドは、さまざまな[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理状態を示すイメージの一覧を取得するために使用されます。 ソース管理 VSPackage は、IDE にカスタム グリフのイメージ リストへのハンドルを返します。 IDE はこの時点でイメージリストのコピーを作成し、後で表示するグリフを選択するために使用します。 新しいインターフェイスがサポートされていない場合、または`IVsSccGlyphs::GetCustomGlyphList`メソッドが`E_NOTIMPL`戻る場合、IDE は、 によって[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供される既定のグリフの一覧からグリフを取得します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
