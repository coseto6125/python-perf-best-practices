# Ruff 設定檔案查找順序（VS Code 未設定 `"ruff.configuration"`）

當 VS Code 未設定 `"ruff.configuration"` 時，Ruff 擴充功能會按以下順序查找設定檔案：

1.  **專案根目錄的 `ruff.toml`**
    *   格式：TOML，頂層鍵（如 `[lint]`、 `[format]`）。
    *   若存在，優先使用，停止查找。
2.  **專案根目錄的 `pyproject.toml`**
    *   格式：TOML，檢查 `[tool.ruff]` 區段。
    *   若存在且包含 `[tool.ruff]`，使用該設定，停止查找。
3.  **Ruff 預設設定**
    *   若無設定檔案，使用內建預設值：
        *   `line-length = 88`
        *   部分 lint 規則（如 `E`、`F`）
        *   雙引號、空格縮排等

## 設定檔案格式比較

Ruff 的設定可以存放在兩種主要格式的檔案中，它們的結構有所不同：

*   **`pyproject.toml`**:
    *   在此格式中，所有 Ruff 相關的設定都必須位於 `[tool.ruff]` 這個頂層區段之下。
    *   例如，linting 規則會定義在 `[tool.ruff.lint]` 區段，而程式碼格式化設定則在 `[tool.ruff.format]` 區段。
    *   您可以參考本專案中的範例檔案：[`pyproject.toml`](pyproject.toml)
*   **`ruff.toml`**:
    *   在此格式中，設定是直接定義在檔案的頂層區段。
    *   例如，linting 規則會直接定義在 `[lint]` 區段，而程式碼格式化設定則在 `[format]` 區段。
    *   您可以參考本專案中的範例檔案：[`ruff.toml`](ruff.toml)

選擇哪種格式取決於您的專案結構和偏好。如果您的專案已經使用 `pyproject.toml` 來管理其他工具（如 Poetry、Black、isort 等），將 Ruff 設定也整合進去會比較集中。如果您的專案較簡單，或者您偏好將 Ruff 設定獨立出來，則可以使用 `ruff.toml`。

Ruff 會優先查找 `ruff.toml`，然後才是 `pyproject.toml`（如上述查找順序所示）。

## 建議

為確保 VS Code 中的 Ruff 擴充功能使用您的自訂設定（例如 `line-length = 144`、`select = ["ALL"]` 等）：

*   將您的設定檔（`ruff.toml` 或 `pyproject.toml`）儲存至專案根目錄，或是一個可供 VS Code 存取的位置（如 `$HOME`）。
*   **建議做法**：在 VS Code 的 `settings.json` 中明確指定設定檔路徑，以避免混淆並確保一致性：

    ```json
    // 範例：如果您的設定檔是專案根目錄下的 pyproject.toml
    "ruff.configuration": "${workspaceFolder}/pyproject.toml"

    // 範例：如果您的設定檔是專案根目錄下的 ruff.toml
    // "ruff.configuration": "${workspaceFolder}/ruff.toml"

    // 範例：如果您的設定檔位於使用者家目錄 (例如 $HOME/.config/ruff/ruff.toml 或 $HOME/pyproject.toml)
    // "ruff.configuration": "$HOME/pyproject.toml"
    // "ruff.configuration": "$HOME/.config/ruff/ruff.toml"
    ```

    這樣可以確保 Ruff 擴充功能總是使用您指定的設定，而不依賴其內建的查找順序。
