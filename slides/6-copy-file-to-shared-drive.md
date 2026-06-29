# 6 — Send Alice's file to the shared drive (S:)

After you run **Teleport-Alice**, the notebook prints a filename like
`qb_state_483912.txt`. This file holds the quantum state to send to Bob.

Open a **new** PowerShell window (the first one is busy running Jupyter) and copy
the file to the shared drive:

```powershell
Copy-Item "C:\labs\quantum-folder\qb_state_483912.txt" "S:\"
```

Also tell Bob the **filename** and the two measured bits (`bit_ms`, `bit_ma`).

*(Or simply drag the file into the `S:` drive in File Explorer.)*
