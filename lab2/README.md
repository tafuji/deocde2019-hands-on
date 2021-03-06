# Lab 2 Azure DevOps と Visual Studio App Center によるアプリのテスト配布

## ここで学習すること

Lab 1 の作業で、アプリケーションを Azure DevOps 上でビルドすることができるようになりました。 Lab 2 では、Visual Studio App Center を使って、ビルドしたアプリケーションをテストチームに配布する方法を学びます。

具体的には、以下のことを学びます。

- Visual Studio App Center にアプリを作成する方法
- Azure DevOps Pipeline のビルド定義に Visual Studio App Center との連携の設定を行う方法
- Azure DevOps でビルドを実行し、作成されたアプリケーションを App Center にデプロイする方法
- Visual Studio App Center から配布されたアプリケーションをインストールして実行する方法

## 1. Visual Studio App Center にアプリを作成する

アプリケーションをテスト配布するために、Visual Studio App Center 上にアプリケーションを作成します。

### 1. Web ブラウザから以下の URL を開きます

- [https://appcenter.ms/apps](https://appcenter.ms/apps)

### 2. "Add new" ボタンをクリックし、"Add new app" を選択します

![Add new app](./screenshots/AddNewApp.png)

### 3. アプリ名等を入力して、"Add new app" ボタンを押します

![Input app name](./screenshots/AddNewAppName.png)

|項目名|説明|例|
|----|----|----|
|App name|アプリケーション名を入力します|XamarinDemo|
|Release Type|アプリケーションのリリースの種類を選択します。|ここでは、テスターに配布するシナリオを想定して、"Beta" を選択します|
|OS|アプリケーションのオペレーティングシステムを選択します|"Windows" を選択します|
|Platform|アプリケーションのプラットフォームを選択します|"UWP" を選択します|
|Icon|アプリケーションのアイコンを設定します|ハンズオンでは、なにも設定しません|

### 4. App Center にアプリケーションが作成されます

![Input app name](./screenshots/AppCenterAppHome.png)

## 2. Azure DevOps Pipeline のビルドと Visual Studio App Center の連携の設定を行う

Azure DevOps 上に作成したビルド定義の中に、Visual Studio App Center を連携する設定を追加します。これにより、Azure DevOps 上でビルドされたアプリケーションが、Visual Studio App Center に配置され、Visual Studio App Center から、テストチームにアプリケーションが配布されるようになります。

### 1. API Token の取得

1. Visual Studio App Center のページで、ユーザーのアイコンをクリックし、"Account Settings" をクリックします

    ![Account Settings](./screenshots/AccountSettings.png)

2. "API Tokens" をクリックし、"New API token" をクリックします

    ![API Tokens](./screenshots/APITokens.png)

3. "Description" に Token の名前などを入力し、"Access" で "Full Access" を選択して、"Add new API token" をクリックします

    ![New API Tokens](./screenshots/NewAPIToken.png)

4. 作成されたトークンをメモ帳などに張り付けておきます。

    ![Token](./screenshots/APIToken.png)

### 2. Azure Pipeline のビルド定義の編集

1. Azure DevOps でビルド定義を開き、"Edit" をクリックします

    ![Build definition](./screenshots/AzureDevOpsBuildDefinition.png)

2. 取り消し線が引かれている "Deploy to Visual Studio ..." という名前のタスクを右クリックし、"Enable selected task(s)" をクリックします

    ![Enable task](./screenshots/EnableSelectedTask.png)

3. "App Center service connection" の欄の "New" をクリックします

    ![New service connection](./screenshots/AppCenterServiceConnection.png)

4. "Connection name" に接続名（任意）を入力し、"API Token" に先ほどコピーした Visual Studio App Center の API Token を張り付けます

    ![Add service connection](./screenshots/AddConnection.png)

5. "App slug" を入力します。入力形式は、Visual Studio App Center の {username}/{app_identifier} となります。
   - username, app_identifiler は、App Center に作成したアプリケーションの URL を見るとわかります

        ![App Center Url](./screenshots/AppSlugFromUrl.png)

   - App slug を Azure DevOps のビルド定義に入力します

        ![Azure DevOps App slug](./screenshots/AzureDevOpsAppSlug.png)

6. "Binary file path" （アプリケーションをビルドした結果作成されるバイナリファイルのパス）を指定します。ここでは、以下の値を入力します。

    ```shell
    $(Build.ArtifactStagingDirectory)\AppxPackages\**\*.appxbundle
    ```

    ![Binary file path](./screenshots/BinaryFilePath.png)

7. "Release notes" を入力します。この例では、"テストリリース" と入力しています。

    ![Release notes](./screenshots/ReleaseNotes.png)

8. ビルド定義を保存します

    ![Save](./screenshots/SaveBuildDefinition.png)

    コメントを入力して、"Save" をクリックします

    ![Save Comment](./screenshots/SaveComment.png)

## 3. ビルドを実行

Lab 1 で紹介したやり方で、ビルドを実行し、しばらく待つと、App Center へのデプロイタスクが成功していることが確認できます。

![Build result of deploy](./screenshots/BuildResultDeployToAppCenter.png)

## 4. App Center のリリースを確認 / メールからリンクを開いて UWP をインストール

### 1. App Center にデプロイされたかを確認する

App Center をブラウザで開き、"Distribute の中の ""Release" をクリックすると。Azure DevOps でビルドされたバイナリがデプロイされていることが確認できます。

![App Center release binary](./screenshots/AppCenterReleaseBinary.png)

### 2. アプリケーションが配布されたかを確認する

App Center にアプリケーションが配布されると、App Center のアカウントのメールアドレスにメールが送信されます。

![App Center Outlook](./screenshots/AppCenterOutlook.png)

"Install" のリンクをクリックすると、アプリケーションをダウンロードし、インストールすることができます。

![Download](./screenshots/DownloadBinary.png)

ダウンロードした "appxbundle" ファイルをダブルクリックしてください。

![Double Click](./screenshots/DoubleClick.png)

インストーラーが起動するので、"インストール" ボタンをクリックして、アプリをインストールしてください。

![Install](./screenshots/Installer.png)

- 注意事項

    すでにインストールされていますというメッセージが表示された場合は、スタートメニューで "SampleApp.UWP"
    をアンインストールした後に、"appxbundle" ファイルをダブルクリックして、アプリをインストールしてください。

    ![Already Installed](./screenshots/AlreadyInstalled.png)

    ![Uninstall](./screenshots/UnInstallApp.png)

以上で、Lab 2 は終了です。