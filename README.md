


🚀 Gradio × Stable Diffusion V1.4 影像生成互動系統
本專案提供了一個輕量、直觀且即時的網頁互動介面（WebUI），讓使用者輸入文字提示詞（Prompt）後，即可透過預訓練的大型擴散模型 Stable Diffusion v1-4 自動生成相對應的高品質影像。本系統整合了 Hugging Face 的 diffusers 庫與 Gradio 框架，非常適合用於生成式 AI 教學、快速原型開發與影像生成實驗。

✨ 核心功能與特色
文字生成影像（Text-to-Image）： 輸入任意英文敘述，系統即可在數秒內將抽象文字轉化為具體視覺圖像。

網頁互動介面（Gradio WebUI）： 無需具備前端開發經驗，透過簡易的 Python 程式碼即可快速建構出美觀、直觀的輸入與輸出欄位。

一鍵外鏈分享（Public Share）： 啟動後將自動產生一組具時效性的公網連結（Gradio Share Link），方便遠端測試或與團隊即時展示成果。

硬體加速優化： 程式碼原生支援並要求 NVIDIA CUDA GPU 環境，採用 torch.float16（半精度浮點數）進行模型載入，大幅降低顯示記憶體（VRAM）佔用並加速推論。

🛠️ 環境架構與技術棧
核心語言： Python 3

前端介面： Gradio（用於建構 WebUI）

擴散模型底層： Hugging Face Diffusers & Accelerate

後端基底： PyTorch (支援 CUDA 加速)

預訓練模型： CompVis/stable-diffusion-v1-4

📖 程式碼執行流程說明
本專案主要由四個核心區塊組成，依序執行即可啟動服務：

環境部署（Installation）：
透過 pip 工具自動下載並安裝系統所需的依賴套件：

Bash
!pip install gradio diffusers accelerate
模型載入與 GPU 配置（Model Initialization）：
從 Hugging Face Hub 載入經典的 Stable Diffusion v1-4 權重。為了優化運算效能，特別將數據型態宣告為 torch.float16，並將整個推論管線（Pipeline）指派至 cuda 裝置進行硬體加速。

核心推論函式（Core Inference Function）：
定義 gen_image(prompt) 函式，接收使用者輸入的文字，調用 Pipeline 進行反向擴散去噪，最後回傳解碼完成的影像物件。

網頁端點啟動（Interface Launch）：
使用 gr.Interface 綁定輸入（文字框）、輸出（圖片框）與推論邏輯。執行 launch(share=True, debug=True) 後，系統會在本地端與公網同時建立連線，並開啟除錯模式以便即時追蹤推論狀態。

⚠️ 注意事項
執行環境： 本專案必須在配置有 NVIDIA GPU（如 Google Colab 的 T4/L4 或獨立顯示卡）的環境下執行。若在純 CPU 環境下執行，將會引發 CUDA 錯誤。

首次載入： 第一次執行模型初始化時，系統需要從雲端下載數 GB 的模型權重檔案，耗時較長屬正常現象。
