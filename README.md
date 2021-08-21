# ConcertBot
It is a line chatbot written in Google Apps Script (Javascript) with Google sheet as its backend. It features that it works properly without the Google Apps Script editor.

## Table of Contents
<details open>
<summary><b>(click to expand or hide)</b></summary>
<!-- MarkdownTOC -->

1. [Setup the environment](#setup-the-environment)
    1. [Notice](#notice)
    1. [Node.js and NPM](#node-js-and-npm)
    1. [Visual Studio Code (optional)](#visual-studio-code)
    1. [Clasp](#clasp)
    1. [Git](#git)
1. [Working with Both Clasp and Git in VS Code](#working-with-both-clasp-and-git-in-vs-code)
    1. [Preparations](#preparations)
    1. [Editing and uploading the codes to Github and Google](#editing-and-uploading-the-codes-to-github-and-google)
    1. [Deploy on Google](#deploy-on-google)
    
    
<!-- /MarkdownTOC -->
</details>

---
<a id="setup-the-environment"></a>
## Setup the environment
<a id="notice"></a>
### Notice:
* All the following commands are run in a command prompt (terminal) in the working directory of the project in a **single** line per block. In detail, ...
    1. [Open a command prompt in Windows](https://www.businessinsider.com/how-to-open-command-prompt)
    1. Open the File Explorer and copy the path of the working directory.
    1. Enter there by the following command (replace `<dir>` with the copied path):  
    `cd <dir>`

<a id="node-js-and-npm"></a>
### Node.js and NPM
* Functionalities: Run clasp.
* Installation instructions: https://phoenixnap.com/kb/install-node-js-npm-on-windows

<a id="visual-studio-code"></a>
### Visual Studio Code (optional)
* Functionalities: Editing codes off line
* Installation instructions:
    * Download and install VS Code from [its official website](https://code.visualstudio.com/).
    * Make the following `jsconfig.json` file in the root of the working directory to use IntelliSense to reference stuffs among different files.
        ```json
        {
            "compilerOptions": {
            "module": "commonjs",
            "allowSyntheticDefaultImports": true,
            },
        }
        ```
    * Setup Google-apps-script word-completion in VS Code ([Ref.](https://yagisanatode.com/2019/04/01/working-with-google-apps-script-in-visual-studio-code-using-clasp/)):
        * Create a folder to store codes
        * Run the command  
        `npm install @types/google-apps-script`

<a id="clasp"></a>
### Clasp
* Functionalities: Update the changes of codes on a computer to Google.
* Installation instructions ([Ref.](https://developers.google.com/apps-script/guides/clasp)): 
    * Run the command:  
        `npm install @google/clasp -g`
    
    * Install inquirer if you want. (It is not necessary)  
        `npm install inquirer`

<a id="git"></a>
### Git
* Functionalities: Version contorl and collaboration
* Installation instructions: Download from [its official website](https://git-scm.com/downloads) and install it.
---

<a id="working-with-both-clasp-and-git-in-vs-code"></a>
## Working with Both Clasp and Git in VS Code

<a id="preparations"></a>
### Preparations
1. Sign up on [Github](https://github.com/).
1. [Create a repository](https://docs.github.com/en/get-started/quickstart/create-a-repo) and copy the repo path (hyperlink) as `<path>`.
1. Clone the repo to the working directory with the commands ([Ref.](https://stackoverflow.com/a/18999726)).  
    `git init`

    `git remote add origin <path>`

    `git fetch`

    `git checkout -t origin/master`
    
    Note: `-t` will set the upstream branch for you, if that is what you want, and it usually is.
1. Change the default editor of git to VS Code locally. ([Ref.](https://stackoverflow.com/a/36427485))  
    `git config core.editor "code --wait"`
1. Google sheet and project
    1. Create a Google sheet
    1. Create a Google apps script project with "tool" -> "script editor" in the toolbar  
    1. Login to Google with clasp
        `clasp login`
    1. Download the project to the `src` folder under the working directory with the command. (Note that `<script ID>` can be found in the project settings)  
        `clasp clone <script ID> --rootDir ./src`

1. Deploy on Google with the following instructions in the **legacy** editor (Why lagacy: [#1](/../../issues/1))
    1. Switch to the legacy editor by entering the script editor and click the “Use legacy editor” on the upper-right corner.
    1. Click “publish” on the toolbar
    1. Project version: New
    1. Description: Initial deployment
    1. Execute the app as: Me
    1. Who has access to the app: Anyone , even anonymous

<a id="editing-and-uploading-the-codes-to-github-and-google"></a>
### Editing and uploading the codes to Github and Google
1. Edit…
1. Upload to Github  (Why git before clasp: [#3](/../../issues/3)) ([More commands](https://docs.google.com/document/d/1c-OrQLbNHiUpPAVxULZvyaGUupKESsC5f1XQFVBI12A))  
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
1. Get the `<deployment ID>`. It is followed by `“@1 - Initial deployment”` from the the result of the command. (Why you should get: [#2](/../../issues/2))  
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
