# Speaking Clock 語音報時程式

這是一個使用 Azure Cognitive Services Speech Services 的語音報時應用程式。它可以接受語音輸入並用語音回應目前時間。

## 專案結構

```
speaking-clock/
│  speaking-clock.csproj    # 專案設定檔
│  Program.cs              # 主程式碼
│  appsettings.json       # 設定檔(包含 Azure 金鑰)
```

## 主要功能

這個應用程式提供以下功能：
- 語音識別：接受「What time is it?」的語音輸入
- 英文語音回應：用英文報讀當前時間
- 中文語音回應：用中文報讀當前時間

## 程式碼說明

### Program 類別

主要類別，包含所有程式邏輯。

#### 全域變數
- `speechConfig`: Speech Services 的設定物件

#### Main 方法
```csharp
static async Task Main(string[] args)
```
主程式進入點，負責:
1. 設定控制台編碼為 Unicode
2. 讀取設定檔獲取 Azure 認證
3. 設定 Speech Services
4. 處理語音命令
5. 根據命令回應時間

#### TranscribeCommand 方法
```csharp
static async Task<string> TranscribeCommand()
```
負責語音辨識:
1. 播放提示音效
2. 設定音訊輸入
3. 辨識語音
4. 回傳辨識結果

#### TellTime 方法
```csharp
static async Task TellTime()
```
用英文報時:
1. 取得當前時間
2. 設定英文語音(使用 en-GB-RyanNeural 語音)
3. 轉換時間為語音
4. 輸出至喇叭與控制台

#### MyMessage 方法
```csharp
static async Task MyMessage()
```
用中文報時:
1. 取得當前時間
2. 設定中文語音(使用 zh-TW-HsiaoChenNeural 語音)
3. 轉換時間為語音
4. 輸出至喇叭與控制台

## 設定說明

在 appsettings.json 中需要設定:
- CognitiveServiceKey: Azure Speech Services 的金鑰
- CognitiveServiceRegion: 服務區域(如 eastus)

## 使用的 Azure 服務

- Azure Cognitive Services Speech Services
  - 語音辨識(Speech-to-Text)
  - 語音合成(Text-to-Speech)

## 使用的語音模型

- 英文語音: en-GB-RyanNeural
- 中文語音: zh-TW-HsiaoChenNeural

## 錯誤處理

程式包含基本的錯誤處理:
- 檢查語音辨識結果
- 處理服務取消狀況
- 檢查語音合成結果

## 系統需求

- .NET 8.0
- Azure Speech Services 訂閱
- 麥克風和喇叭
