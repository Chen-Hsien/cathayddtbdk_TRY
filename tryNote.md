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
