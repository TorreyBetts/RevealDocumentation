---
pagination_next: web/authentication
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Google Drive データ ソースの追加

:::danger 重大な変更

現在、Reveal SDK は、Reveal SDK core パッケージからデータ ソースを分離する過程にあります。プロジェクトの継続的な機能を確保するために、プロジェクトに追加のパッケージをインストールすることが必要になる場合があります。詳細については、[サポートされるデータ ソース](web/datasources.md#サポートされるデータ-ソース) トピックを参照してください。

:::

**手順 1** - `RevealView.onDataSourcesRequested` イベントのイベント ハンドラーを追加します。

```js
var revealView = new $.ig.RevealView("#revealView");
revealView.onDataSourcesRequested = (callback) => {
    //add code here
    callback(new $.ig.RevealDataSources([], [], false));
};
```

**手順 2** - `RevealView.onDataSourcesRequested` イベント ハンドラーで、[RVGoogleDriveDataSource](https://help.revealbi.io/api/javascript/latest/classes/rvgoogledrivedatasource.html) オブジェクトの新しいインスタンスを作成します。`Title` プロパティと `Subtitle` プロパティを、Google ドライブに対応する値に設定します。`RVGoogleDriveDataSource` オブジェクトを作成したら、それをデータ ソース コレクションに追加します。

```js
revealView.onDataSourcesRequested = (callback) => {
    var googleDrive = new $.ig.RVGoogleDriveDataSource();
    googleDrive.title = "My Google Drive";
    googleDrive.subtitle = "Google Drive";

    callback(new $.ig.RevealDataSources([googleDrive], [], false));
};
```

アプリケーションが実行されたら、新しい可視化を作成すると、新しく作成された Google ドライブ データ ソースが [データ ソースの選択] ダイアログに表示されます。

![](images/google-drive-data-source.jpg)

:::note

`RVGoogleDriveDataSource` は、Reveal SDK に登録された認証プロバイダーに基づいてフォルダーとファイルを読み込みます。Google ドライブは `RVBearerTokenDataSourceCredential` を使用して認証します。詳細については、「[認証](../authentication.md#ベアラー-トークン認証)」トピックを参照してください。

:::

:::info コードの取得

このサンプルのソース コードは、[GitHub](https://github.com/RevealBi/sdk-samples-javascript/tree/main/DataSources/GoogleDrive-ServiceAccount) にあります。

:::