
# 第三方 Python 庫推薦

## 第三方庫概覽

| 第三方庫                   | GitHub 連結                                                      | 簡述                                                                                                     |
| -------------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **CalamineWorkbook** | [tafia/calamine](https://github.com/tafia/calamine)                 | 讀取 Excel 類型檔案（支援 xls、xlsx、xlsm、xlsb、xla、xlam、ods，不包含 csv，因為 csv 與純文字差異不大） |
| **msgpack**          | [msgpack/msgpack-python](https://github.com/msgpack/msgpack-python) | 高效的二進制序列化格式，功能比 orjson 更廣泛，效能與 orjson 相當                                         |
| **orjson**           | [ijl/orjson](https://github.com/ijl/orjson)                         | 高效的 JSON 序列化/反序列化庫，專注於速度                                                                |
| **datatable**        | [h2oai/datatable](https://github.com/h2oai/datatable)               | 高效的資料表處理庫，專為大規模資料分析設計                                                               |
| **comrak**           | [lmmx/comrak](https://github.com/lmmx/comrak)                       | 將 Markdown 轉換為 HTML                                                                                  |
| **lxml**             | [lxml/lxml](https://github.com/lxml/lxml)                           | 高效的 HTML/XML 解析庫                                                                                   |
| **html2text_rs**     | [deedy5/html2text_rs](https://github.com/deedy5/html2text_rs)       | 將 HTML 轉換為 Markdown                                                                                  |
| **cython**           | [cython/cython](https://github.com/cython/cython)                   | 將 Python 程式碼編譯為 C 擴充模組（.pyd），用於高效運算                                                  |

## 語言結構與轉換成本

| 第三方庫                   | 庫原始語言結構                                           | 轉換成本/提示/差異 |
| -------------------------- | -------------------------------------------------------- | ------------------ |
| **CalamineWorkbook** | 純 Rust，透過 PyO3 提供 Python 介面                      |                    |
| **msgpack**          | C（核心序列化邏輯），透過 C 擴充模組與 Python 整合       |                    |
| **orjson**           | Rust，透過 PyO3 提供 Python 介面                         |                    |
| **datatable**        | C++（核心邏輯），透過 Python C 擴充模組封裝              |                    |
| **comrak**           | Rust，透過 PyO3 提供 Python 介面                         |                    |
| **lxml**             | C（基於 libxml2 和 libxslt），透過 Python C 擴充模組封裝 |                    |
| **html2text_rs**     | Rust，透過 PyO3 提供 Python 介面                         |                    |
| **cython**           | Python（編譯器部分）與 C（生成程式碼），輸出 C 擴充模組  | 補充說明           |

- **CalamineWorkbook**：適合處理各種試算表格式，特別是 Excel 和 OpenDocument，但不支援 csv（csv 通常用 Python 內建的 `csv` 模組處理）。其 Rust 實現提供高效能。
- **msgpack 和 orjson**：兩者都是高效序列化工具，msgpack 基於 C，支援跨語言序列化；or
