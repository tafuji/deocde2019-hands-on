# Lab 1: Azure DevOps Pipeline による Xamarin アプリのビルド

## 0. Lab 1 で習得できること

このハンズオンでは、以下のことを学ぶことができます。

- Azure DevOps でチームプロジェクトを作成する方法
- Azure Repos からコードをクローンする方法
- Azure Repos にコードをプッシュする方法
- Azure Pipelines で Pipeline を作成する方法
- Azure Pipelines でアプリをビルドする方法

## 1. Azure DevOps でチームプロジェクトを作成する

ここでは、Azure DevOps 上に、チームで作業を行うためのチームプロジェクト（チームでソースコード、タスク、バグ、アプリのビルド、リリース作業などを行うための作業場所）を作成します。

### 1.1 Azure DevOps のサイトにアクセスします

以下のサイトで、Azure DevOps にサインインしてください。

- [Azure DevOps](https://dev.azure.com)

"Sign in to Azure DevOps" をクリックすると、Azure DevOps のサインインページに移動します。

![Sign in](./screenshots/SignInAzureDevOps.png)

### 1.2 Azure DevOps のサイトで、[Create Project] をクリックします

![Create Project](./screenshots/CreateTeamProject.png)

### 1.3 プロジェクト名などを入力します

|項目名|説明|例|
|----|----|----|
|Project name|チームプロジェクトの名前を入力します|XamarinDemo|
|Description|チームプロジェクトの説明を入力します|de:code ハンズオンサンプル|
|Visibility|チームプロジェクトを外部に公開するかどうかを指定します|Private を選択します|
|Version control|チームプロジェクトで利用する |Git を選択します|
|Work item process|プロセステンプレートを選択します|Agile を選択します|

![NewProject](./screenshots/CreateNewProject.png)

### 1.4 しばらく待つと、チームプロジェクトが作成されます

![CreatedTeamProject](./screenshots/ProjectHome.png)

## 2. Azure Repos からコードをクローンする

ここでは、「1. Azure DevOps でチームプロジェクトを作成する」で作成したチームプロジェクトにある、ソースコードのリポジトリをローカルの PC にクローンします。

### 2.1 リポジトリのページに移動します

![Repo](./screenshots/Repopage.png)

### 2.2 "add a .gitigonore:None" をクリックして、"Visual Studio" を選択し、"Initialize" ボタンを押します

![Select Git Ignore File Type ](./screenshots/SelectGitIgnoreType.png)

### 2.3 リポジトリが初期化されたことを確認してください

![Initialized Repository](./screenshots/InitializedRepository.png)

### 2.4 "Clone" をクリックします

![Clone](./screenshots/ClickCloneButton.png)

### 2.5 IDE の下にある "Clone in VS Code" の右側にあるボタンを押し、"Visual Studio" を選択します

![Clone](./screenshots/IDESelectVisualStudio.png)

### 2.6 Visual Studio を開きます

![Open Visual Studio](./screenshots/OpenMsVsSelector.png)

### 2.7 リポジトリをクローンするディレクトリを選択し、「複製」ボタンをクリックします

![Select your directory](./screenshots/ChooseRepoDirectory.png)

## 3. Azure Repos にコードをプッシュする

### 3.1 ソリューションを新規作成します

"ソリューション" で、"新規作成..." をクリックします。

![New Solution](./screenshots/CreateSolutionInTeamExploter.png)

### 3.2 プロジェクトのフィルタリングを行います

"プロジェクトタイプ" で、"モバイル" を選択して、"次へ" をクリックしてください。

![Choose project type](./screenshots/FilterProjectType.png)

### 3.3 Xamarin.Forms プロジェクトを選択します

"モバイル アプリ (Xamarin.Forms)" を選択して、"次へ" をクリックしてください。

![Select Xamarin.Forms project](./screenshots/SelectXamarinFormsProject.png)

### 3.4 プロジェクトの詳細を入力します

"プロジェクト名" に "SampleApp" と入力し、"作成" ボタンをクリックしてください。

![Input project name](./screenshots/ProjectConfiguration.png)

### 3.5 プロジェクトのテンプレートを選択します

|項目名|説明|
|----|----|
|テンプレートの選択|"マスター詳細" を選択します|
|プラットフォーム|"UWP" にチェックを入れる|
|モバイルバックエンド|チェックしない|

![Select project template](./screenshots/ChooseProjectTemplate.png)

### 3.6 アプリケーションの動作確認を行います

#### 3.6.1 スタートアッププロジェクトの設定

![set the uwp project as the startup project](./screenshots/SetStartupProjectInSolutionExplorer.png)

#### 3.6.2 プロジェクトのデバッグ

![Start Debugging project](./screenshots/DebugUWPProject.png)

#### 3.6.3 動作確認

![Start Debugging project](./screenshots/DebugApp.png)

### 3.6.7 テスト用証明書の作成とインポート

1. パッケージマニフェスト（Package.appmanifest）ファイルを開いて、"パッケージ化" タブを選択し、"証明書の選択" ボタンを押します

    ![Open Package Manifest](./screenshots/PackageManifest.png)

2. "証明書の選択" ウィンドウで、"テスト証明書" を選択します

    ![Select test cert](./screenshots/SelectCert.png)

4. そのまま "OK" ボタンを押します

    ![Create test cert](./screenshots/CreateTestCert.png)

5. "証明書の選択" ウィンドウで、"OK" をクリックします

    ![Confirm Cert](./screenshots/SelectCertResult.png)

6. "Package.appxmanifest" ファイルを保存してください

7. テスト証明書をソース管理に追加します。作成された pfx ファイルを右クリックし、"無視されたファイルをソース管理に追加" を選択します

    ![Add Source Repo](./screenshots/AddTestCertToRepo.png)

8. テスト証明書をローカルマシンにインストールします。作成したテスト証明書をエクスプローラー上でダブルクリックします

    ![Double click pfx file](./screenshots/PfxFileInExplorer.png)

9. 証明書のインポートウィザーが起動するので、"ローカルコンピュータ" を選択します

    ![LocalComputer](./screenshots/LocalComputer.png)

10. "次へ" をクリックします

    ![FileName](./screenshots/FileName.png)

11. "次へ" をクリックします

    ![NoPassword](./screenshots/NoPassword.png)

12. "証明書をすべて次のストアに配置する" をチェックして、"信頼されたルート証明機関" を選択して、"次へ" をクリックしてください

    ![TrustedRoot](./screenshots/TrustedRoot.png)

13. "完了" をクリックします

    ![Completed](./screenshots/Completed.png)

14. "OK" をクリックします

    ![Imported](./screenshots/Imported.png)

### 3.6.8 コードをリポジトリへ Push する

1. チームエクスプローラー上で、"変更" を選択します

    ![Select changes](./screenshots/ChangesInTeamExploter.png)

2. "変更" をすべて "ステージング済みの変更" に移動させます。"変更" の中に表示されている最上位のフォルダを右クリックして、コンテキストメニューで "ステージ" を選択してください。（ソリューションの保存ダイアログが表示された場合は、ソリューションを保存してください。）

    ![Stage](./screenshots/StageChanges.png)

3. ソースコードなどすべての成果物が、"ステージング済みの変更" に移動していることを確認し、"コメント" を入力して、"ステージング済みをコミット" ボタンを押します

    ![Commit](./screenshots/FirstCommit.png)

4. ローカルでのコミットが完了したら、"同期" のリンクをクリックします

    ![Sync](./screenshots/FirstSync.png)

5. 同期画面が表示されるので、"同期" のリンクをクリックします

    ![Push](./screenshots/FirstSyncExec.png)

6. Azure DevOps 上にコードが Push されます

    ![Push result](./screenshots/SyncExecuted.png)

## 4. Azure Pipelines でビルド定義を作成する

「3. Azure Repos にコードをプッシュする」で、チームプロジェクトにソースコードが登録されました。ここからは、作成したアプリケーションのビルドを行うために Azure DevOps の Pipeline にビルド定義を作成します。

### 4.1 Azure DevOps の Pipelines のページにアクセスします

![New Pipeline](./screenshots/Pipelines.png)

### 4.2 New Pipeline をクリックします

![New Pipeline](./screenshots/NewPipeline.png)

### 4.3 "Use Classic Editor" をクリック

![Classic Editor](./screenshots/UseClassicEditor.png)

### 4.4 リポジトリを選択して、"Continue" ボタンをクリックします

|項目名|説明|値|
|----|----|----|
|Select a source|ソースコードのリポジトリの種類を選択します|ここでは、"Azure Repos Git" を選択します|
|Team project|pipeline を作成するチームプロジェクトを選択します|作成したチームプロジェクトを選択します（ハンズオンの例では、"XamarinDemo" を選択します）|
|Repository|ソースコードのリポジトリ名を選択します|ハンズオンの例では、"XamarinDemo" を選択します|
|Default branch for manual and scheduled builds|Pipeline でビルドを行う既定のブランチを選択します|master|

![Select Repository](./screenshots/SelectYourRepo.png)

### 4.5 ビルド定義のテンプレートで、"Universal Windows Platform" を選択し、"Apply" ボタンを押します

![Select Build Template](./screenshots/SelectABuildTemplate.png)

### 4.6 ビルド定義が作成されたことを確認し、ビルド定義を保存します

ビルド定義が作成されたことを確認して、"Save & Queue" のタブをクリックして、"Save" をクリックします。

![Created build definition](./screenshots/CreatedBuildDefinition.png)

### 4.7 ビルド定義の保存

コメントを入力し、"Save" ボタンを押します。

![Select Pipeline](./screenshots/SaveBuildPipeline.png)

## 5. Azure Pipelines でアプリをビルドする

### 5.1 ビルドパイプラインで "Queue" ボタンをクリックします

![Queue Build](./screenshots/ClickQueue.png)

### 5.2 "BuildPlatform" の値を "x86" に変更して、"Queue" ボタンをクリックします

![Execute Build](./screenshots/ExecuteQueue.png)

"BuildPlatform" の値は、既定値でもビルドはできますが、ビルドに時間がかかります。今回は、ハンズオンを効率的に行うために、"x86" プラットフォームでビルドを行ってください。

### 5.3 ビルドが開始されたことを確認します

ビルドが開始されると、ビルド番号のリンクが表示されます。そのリンクをクリックします。

![Click build number](./screenshots/QueuedBuild.png)

リンクをクリックすると、ビルド中のタスク状況が表示されます。

![Click build number](./screenshots/ExecutingBuild.png)

### 5.4 Azure Pipeline 上でビルドが成功したことを確認してください

![Build Result](./screenshots/BuildResult.png)

以上で、ハンズオンの Lab 1 は終了です。
