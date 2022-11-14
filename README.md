#### 2022/11/10.   
國泰數數發有開源一套聯盟鏈的部署工具～國泰有將其使用在產險區塊鏈，環球貿易區塊鏈等領域上，     
內部看起來有用上Hyperledger fabric,   J.P. Morgan Quorum，未來再繼續研究其底層的邏輯，今天先將它起起來看看服務長什麼樣子吧。  

#### 從原始碼安裝 (Install from Source).  

```bash
git clone https://github.com/cathayddt/bdk.git
cd bdk

//npm install
npm install --save --legacy-peer-deps

npm run build:console
```

當中因typescript相依套件版本衝突，改為使用npm install --save --legacy-peer-deps.  
忽略不同擴充套件因為相依的套件版本所造成的問題.  

```bash
npm run build:console

sudo chown -R 'UsrName' /xxx/xxx
```
這邊則是因資料夾路徑permission denied，把資料夾owner設為當前使用者即可.  
<img width="691" alt="image" src="https://user-images.githubusercontent.com/24216536/201607342-506a105e-daf2-4595-9c8c-78a89dc2d095.png">.  

後續就可以看到BDK跟你Hello了~~  
<img width="923" alt="截圖 2022-11-14 下午4 22 40" src="https://user-images.githubusercontent.com/24216536/201610689-dda22689-3c8b-4fd2-b02e-c1dd3b39e427.png">.  
再利用官方提供的指令來建立簡單的區塊鏈網路吧。 
```bash
  # create network
  bdk fabric network create --test-network
  # start orderer docker container (interactive mode)
  bdk fabric orderer up -i
  # start peer docker container (interactive mode)
  bdk fabric peer up -i
```
在對應order按下右鍵點亮為綠燈，在ENTER確認，就代表他以container起起來嚕。  
<img width="464" alt="image" src="https://user-images.githubusercontent.com/24216536/201617640-fd733901-a167-4c46-9138-f15c6c9b9453.png">   
<img width="685" alt="image" src="https://user-images.githubusercontent.com/24216536/201617575-4a018b59-59a9-4560-994f-eb5e2a0c698b.png">  
<img width="464" alt="image" src="https://user-images.githubusercontent.com/24216536/201619046-511ed947-3d22-4180-aa3f-0018ffdab87d.png">  
回到Docker裡面就可以看到對應名稱的節點出現在裡面惹。  
<img width="437" alt="image" src="https://user-images.githubusercontent.com/24216536/201619239-c20e8376-4a8d-4c40-ae7e-e1d04934c7ef.png">.  

初步建立國泰數數發區塊鏈網路，到這邊，後續會再研究裡面有提供怎麼樣的功能～








# Blockchain Deployment Kit

提供指令快速建立、管理、監控 blockchain，最大的特色是可以使用互動式的問答，讓使用者可以依續性的問答來完成指令所需要的指令，在每個 BDK 指令的後面，加入 `-i` 或是 `--interactive` 的參數，來使用互動式問答

BDK streamlines the normally complicated process of creating a blockchain with command-line tools and npm packages. Creating, managing, monitoring a blockchain network has never been easier. We support interactive prompts which can be triggered with `-i` or `--interactive` behind all cli commands

e.g.

```
bdk quorum network create -i
```
![bdk quorum network create -i](images/bdk-quorum-network-create.gif)

```bash
bdk fabric network create -i
```

![bdk fabric network create -i](images/bdk-fabric-network-create.gif)

## 版本 (Releases)

|      Latest      |      Stable      |
| ---------------- | ---------------- |
| [v2.0.0][v2.0.0] | [v1.0.4][v1.0.4] |

[v1.0.4]: https://github.com/cathayddt/bdk/releases/tag/v1.0.4

[更新內容 (Changelog)](CHANGELOG.md)

## 文件 (Documentation)

- 指令文件 CLI Documentation (Work in Progress)
- [Fabric 使用範例 (Examples)](docs/fabric/EXAMPLE.md)
- [Quorum 使用範例 (Examples)](docs/quorum/EXAMPLE.md)
- [開發指南 (Contributing)](CONTRIBUTING.md)
- [資安通報 (Security Issues)](SECURITY.md)

## 安裝流程 (Getting Started)

### 環境 (Prerequisites)

- [npm + nodejs](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) node v16, npm v8
- [docker](https://docs.docker.com/engine/install)
- [docker-compose](https://docs.docker.com/compose/install) >= 1.27
- eslint (vscode plugin, dev-only)

### 主程式安裝 (Installation)

#### 直接安裝 (Direct Install)

```bash
npm config set @cathayddt:registry=https://npm.pkg.github.com

# https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
npm config set //npm.pkg.github.com/:_authToken=[SET-YOUR-TOKEN]

npm install -g @cathayddt/bdk@latest

# 初始化 (initialize)
bdk fabric config init
```

#### 從原始碼安裝 (Install from Source)

```bash
git clone https://github.com/cathayddt/bdk.git
cd bdk

npm install

npm run build:console
```

## 設定 (Configuration)

### 設定自動完成 (Configure AutoComplete)

```bash
bdk completion
```

腳本 (script source is as follows)

```bash
###-begin-bdk-completions-###
#
# yargs command completion script
#
# Installation: bdk completion >> ~/.zshrc
#    or bdk completion >> ~/.zsh_profile on OSX.
#
_bdk_yargs_completions()
{
  local reply
  local si=$IFS
  IFS=$'
' reply=($(COMP_CWORD="$((CURRENT-1))" COMP_LINE="$BUFFER" COMP_POINT="$CURSOR" bdk --get-yargs-completions "${words[@]}"))
  IFS=$si
  _describe 'values' reply
}
compdef _bdk_yargs_completions bdk
###-end-bdk-completions-###
```

## Hello BDK

使用以下的指令，可以確認 BDK 已安裝完成並且可以開始操作使用

Use the following command to verify that BDK has completed installation and is now ready to be used.

```bash
bdk hello
```

如果指令已順利安裝，你會看到 `You have installed bdk successfully!!!` 

You will see `You have installed bdk successfully!!!` if the command line tool is installed successfully.

## 建立一個 Test Network (Create a test network)

使用以下指令，可以建立一個簡單的 Hyperledger Fabric 網路

Use the following command to create a simple Hyperledger Fabric Network.

```bash
  # create network
  bdk fabric network create --test-network
  # start orderer docker container (interactive mode)
  bdk fabric orderer up -i
  # start peer docker container (interactive mode)
  bdk fabric peer up -i
```

## LICENSE

[Apache2.0](LICENSE)
