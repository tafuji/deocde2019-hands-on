# Lab 1: Azure DevOps Pipeline で Xamarin アプリケーションをビルドする

## ここで学習すること

ここでは、以下のことを学習します。

- Azure DevOps の Pipeline を利用して、Xamarin アプリケーションのビルドを行う

## 目次

- Azure DevOps でチームプロジェクトを作成する
- プロジェクトの作成
- コードをプッシュする
- Azure Pipeline の作成

## 1. Azure DevOps でチームプロジェクトを作成する

1. Azure DevOps のサイトにアクセスします

2. Azure DevOps のサイトで、[Create Project] をクリックします

    ![Create Project](./screenshots/CreateTeamProject.png)

3. プロジェクト名などを入力します

    ![NewProject](./screenshots/CreateNewProject.png)

    |項目名|説明|例|
    |----|----|----|
    |Project name|チームプロジェクトの名前を入力します|XamarinDemo|
    |Description|チームプロジェクトの説明を入力します|de:code ハンズオンサンプル|
    |Visibility|チームプロジェクトを外部に公開するかどうかを指定します|Private を選択します|
    |Version control|チームプロジェクトで利用する |Git を選択します|
    |Work item process|プロセステンプレートを選択します|Agile を選択します|

4. しばらく待つと、チームプロジェクトが作成されます

    ![CreatedTeamProject](./screenshots/ProjectHome.png)

## 2. リポジトリにソースコードを Push する

1. リポジトリをクローンします
   1. 「Clone in Visual Studio」をクリックします

        ![Clone to your computer](./screenshots/CloneToYourComputer.png)

   2. リポジトリをクローンするディレクトリを選択し、「複製」ボタンをクリックします

        ![Select your directory](./screenshots/ChooseRepoDirectory.png)

   3. ソリューションを新規作成します

2. Xamarin アプリケーションを作成します
   1. プロジェクトを新規作成します

        ![New Solution](./screenshots/CreateSolutionInTeamExploter.png)

   2. プロジェクトのフィルタリング

        ![Choose project type](./screenshots/FilterProjectType.png)

   3. Xamarin.Forms プロジェクトを選択

        ![Select Xamarin.Forms project](./screenshots/SelectXamarinFormsProject.png)

   4. プロジェクトの詳細を入力

        ![Input project name](./screenshots/ProjectConfiguration.png)

   5. プロジェクトのテンプレートを選択

        ![Select project template](./screenshots/ChooseProjectTemplate.png)

3. アプリケーションの動作確認
   1. スタートアッププロジェクトの設定

        ![set the uwp project as the startup project](./screenshots/SetStartupProjectInSolutionExplorer.png)

   2. プロジェクトのデバッグ

        ![set the uwp project as the startup project](./screenshots/DebugUWPProject.png)

   3. 動作確認


4. コードをリポジトリへ Push する



## 3. Azure Pipeline の作成

## 4. Azure Pipeline でアプリケーションをビルドする

