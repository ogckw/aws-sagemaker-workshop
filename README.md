# AWS SageMaker工作坊 
AWS SageMaker是一個全受管的機器學習服務。從監督式學習到非監督式學習，從決策樹到深度學習，資料科學家可以都輕鬆的將自己的分析流程及演算法實現在上面，並可以使用AWS最佳化過的演算法來進行分析。特色為貼近目前開發者的生態體系，例如：使用Jupyter Notebook開發、可以使用Docker客製化環境、整合SDK可以跨語言使用提供其他團隊使用，目前提供AWS Cli、.NET、C++、Go、Java、JavaScript、PHP、Python、Ruby等SDK。

Created by Hans (github: https://github.com/ogckw)
 
## SageMaker元件說明

### SageMaker架構

  ![sagearch](images/ironman-architecture.png)

* S3 Bucket
  
  提供SageMaker儲存及讀取訓練資料、存放模型

* Container Registry

  提供程式碼執行環境的image


* Notebook Instance
  
  用於資料科學家互動式分析服務，可以使用資料科學家常使用的`Jupyter Notebook`分析並分享給合作團隊。

* ML Training Service

  用於訓練及分析資料運算服務，可以利用分散式演算法來進行分散式運算，不用管理叢集的基礎設施，讓資料科學家只用專注在算法上而不是管理叢集。

* ML Hosting Service

  用於最終提供預測或分類算演法結果服務，不用管理叢集的基礎設施，可以輕鬆的整合任何語言呼叫演算法使用，就像在使用習慣語言中的SDK一樣。

# Workshop 流程教學指引

## 預先要求
* AWS帳號並有Admin權限
* 能連上網路且足夠順暢的電腦
* 瀏覽器為Chrome或Firefox
* 基礎的IAM、EC2、S3知識


## Module0 Prepare Environment 約10分鐘
準備基礎環境



1. 登入AWS

   本Lab可選擇的Region如下列，請確保接下來開的服務都在同個Region，這邊範例使用`US East (N. Virginia)`

   1. US East (N. Virginia)
   2. US East (Ohio)
   3. US West (Oregon)
   4. EU (Ireland) 
   
   確認自己所在的Region為US East (N. Virginia)

   ![login](images/sagemaker01.png)


2. 建立S3 Bucket提供之後進行Module使用

   ![creates3](images/sagemaker02.png)

   ![creates3](images/sagemaker03.png)

   輸入S3 名稱及區域
   
   Bucket Name: `請填入想要的名稱`
   
   這邊的範例使用`hans-work-201804`
   
   注意! S3 bucket名稱為全球唯一，重覆的名稱會無法建立，所以請勿照抄範例，請自己想一個適合的名稱

   Region: `US East (N. Virginia)`

   ![creates3](images/sagemaker04.png)　

   一直選Next直到建立好bucket

   ![creates3](images/sagemaker05.png)

   ![creates3](images/sagemaker06.png)

   ![creates3](images/sagemaker07.png)

   ![creates3](images/sagemaker08.png)

## Module1 Introduction to Notebook Instance 15分鐘
建立一個資料科學家探索資料用機器並探索資料

1. 建立Notebook Instance

   選擇服務SageMaker

   ![createsagemaker](images/sagemaker09.png)
   
   建立Notebook Instance

   ![createsagemaker](images/sagemaker10.png)

   設定Notebook Instance規格

   Notebook instance name: `請填入想要的名稱`

   Notebook instance type: `請選擇想要的型號`

   建議instance type選擇`ml.t2.medium`或`ml.m4.xlarge`

   ![createsagemaker](images/sagemaker11.png)

   設定Notebook所使用的IAM Role權限
   
   ![createsagemaker](images/sagemaker12.png)

   填入剛剛建立的S3 bucket名稱後建立Role

   ![createsagemaker](images/sagemaker13.png)

   建立成功畫面並確認VPC - optional選擇No VPC後選擇Create  notebook instance

   ![createsagemaker](images/sagemaker14.png)

   會出現建立中的畫面

   ![createsagemaker](images/sagemaker15.png)

   建立完成看到InService後點選Open

   ![createsagemaker](images/sagemaker16.png)

   瀏覽器會跳出新的視窗，恭喜你！成功建立第一個資料科學家所使用的環境

   ![createsagemaker](images/sagemaker17.png)
   
2. 探索資料
   
   選擇New建立新的資料夾並改名為`video-game-sales`

   ![createsagemaker](images/sagemaker18.png)

   ![createsagemaker](images/sagemaker19.png)

   ![createsagemaker](images/sagemaker20.png)

   點選進入新建的資料夾並上傳檔案`cht-video-game-sales-xgboost.ipynb`

   ![createsagemaker](images/sagemaker21.png)

   ![createsagemaker](images/sagemaker22.png)

   ![createsagemaker](images/sagemaker23.png)

   進入Notebook開始開發

   ![createsagemaker](images/sagemaker24.png)

   簡易介紹Jupyter Notebook使用方式，`Jupyter Notebook`是一個資料科學家常使用的開發工具，舉例來說，剛剛上傳的`cht-video-game-sales-xgboost.ipynb`為一個Notebook，一個Notebook又由一個個Cell組成程式碼來達到與資料分析跟互動。
   紅框框起來的部分是編輯程式碼及執行的地方，稱為Cell，
   透過滑鼠左建點擊選取想要的Cell
   使用`Shift + Enter`來執行該個Cell內的程式碼

   ![createsagemaker](images/sagemaker25.png)

   或選`Run`也可以執行該Cell的程式碼

   ![createsagemaker](images/sagemaker-running-cell.png)

   執行中的Cell會顯示左側框框(In[ ])會顯示`*`號
   
   ![createsagemaker](images/sagemaker26.png)
   
   修改S3 Bucket成自己剛剛建立的Bucket名稱

   ![createsagemaker](images/sagemaker-s3-bucket.png)

   接下來可以照著Notebook上的指示開發

   請注意!!! 本程式碼腳本會上下互相依賴，請務必照順序執行Cell，請勿隨意重新整理網頁，如果重新整理網頁之前執行的內容會消失


## Module2 Introduction to ML Training Service 約15分鐘
建立一個資料科學家運算跟分析機器

1. 建立ML Training Service Instance

   設定要訓練的工作，例如要用什麼機器，在哪個Region

   ![createsagemaker](images/sagemaker27.png)

   ![createsagemaker](images/sagemaker27-1.png)

   XGBoost演算法要輸出模型的位置以及超參數等設定

   ![createsagemaker](images/sagemaker27-2.png)


   開始訓練，這邊準備的範例約需要訓練6-10分鐘

   ![createsagemaker](images/sagemaker28.png)

   
2. 監控訓練狀態

   可以回到AWS的Console看到UI介面上的設定

   ![createsagemaker](images/sagemaker29.png)

   訓練的狀態

   ![createsagemaker](images/sagemaker30.png)

   CloudWatch會紀錄訓練的log

   ![createsagemaker](images/sagemaker31.png)

## Module3 Introduction to ML Hosting Service 約15分鐘
建立一個機器學習提供預測或分群服務使用

1. 建立ML Hosting Service Instance

   指定模型

   ![createsagemaker](images/sagemaker32.png)

   設定EC2規格

   ![createsagemaker](images/sagemaker33.png)

   建立服務的Endpoint約需要8-10分鐘

   ![createsagemaker](images/sagemaker34.png)

2. 開始評估模型

   ![createsagemaker](images/sagemaker35.png)


   建立混淆矩陣 (Confusion Matrix)

   ![createsagemaker](images/sagemaker36.png)

   計算預測的準確率

   ![createsagemaker](images/sagemaker37.png)


## Clean Up
清除你的環境避免額外的收費

1. 清除ML Hosting Service (清除Endpoints)

   ![createsagemaker](images/sagemaker38.png)

2. 清除Endpoint Configuration

   ![createsagemaker](images/sagemaker39.png)

3. 清除Models

   ![createsagemaker](images/sagemaker40.png)

4. 清除Notebook
    
   先停止

   ![createsagemaker](images/sagemaker41.png)

   確認停止後刪除

   ![createsagemaker](images/sagemaker42.png)

5. 清除S3
   
   搜尋剛剛建立的S3 Bucket並選擇刪除

   ![createsagemaker](images/sagemaker43.png)

   填入想要刪除的S3 Buckcet名稱後按確認

   ![createsagemaker](images/sagemaker44.png)
   

6. 清除IAM
   
   ![createsagemaker](images/sagemaker47.png)

   ![createsagemaker](images/sagemaker48.png)

   ![createsagemaker](images/sagemaker49.png)

   
   

