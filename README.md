# Linebot Sameple
It is a LINE chatbot written in Google Apps Script (Javascript) with Google sheet as its backend. It features that it works properly without the Google Apps Script editor.

## Table of Contents
<details open>
<summary><b>(click to expand or hide)</b></summary>
<!-- MarkdownTOC -->

1. [Set up the environment](#set-up-the-environment)
    1. [Notice](#notice)
    1. [Node.js and NPM](#node-js-and-npm)
    1. [Visual Studio Code (optional)](#visual-studio-code)
    1. [Clasp](#clasp)
    1. [Git](#git)
1. [Working with Both Clasp and Git in VS Code](#working-with-both-clasp-and-git-in-vs-code)
    1. [Preparations](#preparations)
    1. [Editing and uploading the codes to Github and Google](#editing-and-uploading-the-codes-to-github-and-google)
    1. [Deploy on Google](#deploy-on-google)
1. [Link LINE and Google Sheet](#link-line-and-google-sheet)
1. [Link to LINE Notify](#link-to-line-notify)
1. [Debug](#debug)
    
    
<!-- /MarkdownTOC -->
</details>

---
<a id="set-up-the-environment"></a>

## Set up the environment

<a id="notice"></a>

### Notice:
* All the commands in this file are run in a command prompt (terminal) in the working directory of the project in a **single** line per command block. To enter into the working directory, you have to
    1. [Open a command prompt in Windows](https://www.businessinsider.com/how-to-open-command-prompt)
    1. Open the File Explorer and copy the path of the working directory.
    1. Enter there by the following command (replace `<dir>` with the copied path):  
    `cd <dir>`
    1. Tips: If you clone this repo, you can just double-click the `enterCurrentDirectory.bat` in the file explorer of the Windows.
* After the first time of the setup, this section can be skipped for the projects in the future.

<a id="node-js-and-npm"></a>

### Node.js and NPM
* Functionalities: Run clasp.
* Installation instructions: https://phoenixnap.com/kb/install-node-js-npm-on-windows

<a id="visual-studio-code"></a>

### Visual Studio Code (optional)
* Functionalities: Editing codes off line
* Installation instructions:
    * Download and install VS Code from [its official website](https://code.visualstudio.com/).
    * Make the following `jsconfig.json` file in the root of the working directory to use IntelliSense to reference stuffs among different files. (This step can be skipped if you clone this repo.)
        ```json
        {
            "compilerOptions": {
            "module": "commonjs",
            "allowSyntheticDefaultImports": true,
            },
        }
        ```
    * Setup Google-apps-script word-completion in VS Code ([Ref.](https://yagisanatode.com/2019/04/01/working-with-google-apps-script-in-visual-studio-code-using-clasp/)):
        * Run the command. 
        `npm install @types/google-apps-script -g`

<a id="clasp"></a>

### Clasp
* Functionalities: Update the changes of codes on a computer to Google.
* Installation instructions ([Ref.](https://developers.google.com/apps-script/guides/clasp)): 
    * Run the command:  
        `npm install @google/clasp -g`  
    * Note: It is recommended to install clasp globally with the `-g` flag as the above. As a result, there will not be duplicated 170MB files in multiple projects.
    
    * Install inquirer if you want. (It is not necessary)  
        `npm install inquirer -g`
* Note: Clasp cannot be run in PowerShell.

<a id="git"></a>

### Git
* Functionalities: Version contorl and collaboration
* Installation instructions: Download from [its official website](https://git-scm.com/downloads) and install it.
---

<a id="working-with-both-clasp-and-git-in-vs-code"></a>

## Working with Both Clasp and Git in VS Code

<a id="preparations"></a>

### Preparations
1. Set up things of Github  
    1. Sign up on [Github](https://github.com/).
    1. Create an **empty** folder locally as the working directory.
    1. Clone the repo to the working directory with the commands ([Ref.1](https://stackoverflow.com/questions/29368837/copy-a-git-repo-without-history) [Ref.2](https://www.cyberciti.biz/faq/how-to-remove-non-empty-directory-in-linux/)). If the folder is not empty, try [the commands on stack overflow](https://stackoverflow.com/questions/5377960/git-whats-the-best-practice-to-git-clone-into-an-existing-folder/13852329#13852329).  
    `git clone https://github.com/Rays314/LinebotSample`
    1. Remove the commit history in the original repository.  
        `rm -rf .git` (in Linux)  
        `rmdir .git /S /Q` (in Windows)  
    1. Remove the readme file in the original repository. (You may want to have a link to [this file](https://github.com/Rays314/LinebotSample/blob/master/README.md) in your readme file to help people set things up.)  
        `rm README.md` (in Linux)  
        `del README.md` (in Windows)
    1. [Create a new repository](https://docs.github.com/en/get-started/quickstart/create-a-repo) and copy the repo path (hyperlink) as `<path>`.
    1. Create the first commit to the new repository.  
        `git remote add origin <path>`  
        `git add .`  
        `git commit -m "Initial Commit"`  
        `git push -u origin master`

1. Change the default editor of git to VS Code locally. ([Ref.](https://stackoverflow.com/a/36427485))  
    `git config core.editor "code --wait"`

1. Google sheet and project
    1. Create a Google sheet.
    1. Create a Google apps script project with "Extensions" -> "Apps script" in the toolbar.
    1. Login to Google with clasp.  
        `clasp login`
    1. Link to the project and download a removable `code.js` file to the `src` folder under the working directory with the command. (Note that `<script ID>` can be found in the project settings.)  
        `clasp clone <script ID> --rootDir ./src`

1. Deploy on Google with the following instructions in the **classic** editor (Why classic: [#1](/../../issues/1))
    1. Switch to the classic editor by entering the script editor and click the “Use classic editor” on the upper-right corner.
    1. Click “Publish” on the toolbar and then "Deploy as web app..."
    1. Project version: New
    1. Description: Initial deployment
    1. Execute the app as: Me
    1. Who has access to the app: Anyone , even anonymous

<a id="editing-and-uploading-the-codes-to-github-and-google"></a>

### Editing and uploading the codes to Github and Google
1. Edit files.
1. Upload to Github  (Why git before clasp: [#3](/../../issues/3))  
    `git add .`  
    `git commit`  
    `git push`
1. Upload to Google  
    `clasp push`
1. Note: The above-mentioned commands can be automated by
    1. `ctrl + shift + `\` (backtick) to open an integrated terminal in VS Code
    1. Run the batch file  
        `batch\push.bat`

        by typing `b<tab>\p<tab><enter>`

<a id="deploy-on-google"></a>

### Deploy on Google
1. Get the `<deployment ID>`. It is followed by `“@1 - Initial deployment”` from the the result of the command. (Why you should get it: [#2](/../../issues/2))  
    `clasp deployments`
1. Deploy on Google  
    `clasp deploy -d <description> -i <deployment ID>`

    Or equivalently, ([Ref.](https://github.com/google/clasp))  
    `clasp deploy --description <description> --deploymentId <deployment ID>`
1. Note: The above-mentioned commands can be automated by
    1. (Do it once) Get the `<deployment ID>` and replace the two `"deployment ID"` in `batch\deploy.bat`. Save the file.
    1. `ctrl + shift + `\` (backtick) to open an integrated terminal in VS Code
    1. Run the batch file. (Replace `<description>` by the **double-quoted** (surrounded by ") **ASCII** description of the version to be deployed.)  
        `batch\deploy.bat <description>`  
        by typing `b<tab>\d<tab> <description><enter>`

<a id="link-line-and-google-sheet"></a>

## Link LINE and Google Sheet
Reference tutorial: https://youtu.be/vS00zQ75xRg
1. Login to [LINE developers](https://developers.line.biz/). Follow the instructions on it to create an account.
1. Create a new provider (by clicking the green icon and follow it).
1. Create a messaging API channel.
1. Switch from the "Basic settings" tab to the "Messaging API" tab.
1. In the "LINE Official Account features" section, in the row of "Allow bot to join group chats", click the "Edit" button to switch to "LINE Official Account Manager". In the section of "Toggle features", in the row of "Group and multi-person chats", switch to "Allow account to join groups and multi-person chats".
1. In the section of "Account details", copy the "Basic ID" (with the @ sign). Add the bot as friend in the LINE platform. It should be able to echo a message now. Otherwise, go to the [debug](#debug) section.
1. In the side bar, switch from "Account settings" to "Response settings". Disable "Greeting message", disable "Auto-response" and enable "Webhooks"
1. Go back to the LINE Developers. In the bottom of the Messaging API tab, issue the channel access token and copy it.
1. Duplicate the `SettingsTemplate.js` file in the `src` folder and rename the duplicated one into `Settings.js`.
1. Paste the channel access token to the `Settings.js` file. It will be like the followig sample but with a longer token.
    ```javascript
    const CHANNEL_ACCESS_TOKEN = 'jhgfdj149qdagy1j/sdhnaf=';
    ```
1. In the section of "Webhook settings", edit the URL as follows. (Note that the project should have been publish on Google as a web app with the [above instructions of preparations](#preparations). And the `<deploy ID>` can be found with [those of deploying on Google](#deploy-on-google).)  
    `https://script.google.com/macros/s/<deploy ID>/exec`
1. Toggle the below option into green to use webhhook.
1. Deploy a new version with the [above instructions of deploying on Google](#deploy-on-google).

---
<a id="link-to-line-notify"></a>

## Link to LINE Notify
1. Login to [LINE Notify](https://notify-bot.line.me/).
1. In [my registered services](https://notify-bot.line.me/my/services/) page, add a service by filling all blanks. Notice that the "Service URL" and "Callback URL" should be as follows.  
    `https://script.google.com/macros/s/<deploy ID>/exec`
1. Verify your identify with the mail in your mailbox that you just filled in.
1. Click the icon of the registered service. Copy the client ID and the client secret to the `Settings.js` file. It should be like the following sample.
    ```javascript
    const LINENOTIFY = {
        CLIENTID: 'f5JSD2JkQWI18a',
        CLIENTSECRET: '4FS3FDJsuU1USi49SA53',
    };
    ```
1. Deploy a new version with the [above instructions of deploying on Google](#deploy-on-google).
1. Add the bot to a group and send a message of exactly `連動`. Click the icon that

<a id="debug"></a>

## Debug
When the bot does not react properly. Follow the instructions below to debug.
1. Open the Google sheet linked to this project and check for the `Exe log` and the `Fetch log` tabs.
1. Use `clasp open` command to open the Apps Script editor. (Or in the tool bar of the Google sheet, click "Extensions" -> "Apps script".) Swtich to the execution tab to check the function that emits an exception.
1. Save and deploy a new version to Google.
1. Insert `logImmediately` function to some potential function to log the info to the `Exe log` sheet.
1. Follow the function-call stack and check for the newest added codes.
