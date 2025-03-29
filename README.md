# 客服機器人 RAG Demo：以好味小姐為例

本專案展示一個結合 LLM（GPT-3.5-turbo）與 RAG（Retrieval-Augmented Generation）的簡易客服機器人，模擬「好味小姐」寵物用品電商的問答系統。使用者可輸入自然語言問題，系統將從文件庫中檢索最相關資料，再搭配 LLM 生成回答。

---

## 🔧 技術架構

- **語言模型**：OpenAI GPT-3.5-turbo  
- **向量資料庫**：使用 [FAISS](https://github.com/facebookresearch/faiss) 建立向量索引  
- **向量化模型**：[`shibing624/text2vec-base-chinese`](https://huggingface.co/shibing624/text2vec-base-chinese)，專為中文語意理解訓練的 sentence embedding 模型  
- **開發語言**：Python

---

## 📁 文件庫內容

文件內容模擬好味小姐的常見 FAQ，包括：

- 會員制度  
- 訂單與配送  
- 退換貨政策  
- 國際運送等

---

## 🚀 實作流程

1. **準備文件庫**  
   將 FAQ 整理成純文字檔 [`faq.txt`](https://github.com/yhkung025/2-1playcode/blob/main/faq.txt)，每筆資料為一問一答結構，格式如下：
   
   Q: 註冊會員需要填哪些資料？ A: 註冊時請完整填寫資料，務必填寫電子郵件及手機，以確保能收到會員資訊與優惠，否則可能導致系統無法辨識，將無法補發相關優惠。\
   Q: 如果沒填正確資料會怎樣？ A: 若註冊時未正確填寫電子郵件與手機，可能導致系統判讀失敗，將不協助補發相關優惠。

3. **文件向量化與索引**  
   使用 `text2vec-base-chinese` 將每筆問答轉換為向量，並存入 FAISS。

4. **檢索與問答流程**  
   - 使用者輸入自然語言問題  
   - 系統計算問題的向量表示，並查詢 FAISS 找出最相關的文件  
   - 取出文件內容，構成 Prompt 給 GPT-3.5-turbo  
   - 回傳由 LLM 生成的回答

---

## 🧪 使用方式

```bash
# 安裝必要套件
pip install -r requirements.txt

# 執行主程式
python 2_1_LLM_RAG.ipynb
