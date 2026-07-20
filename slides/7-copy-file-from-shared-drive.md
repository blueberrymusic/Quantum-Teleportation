# 7 — Bring the file from the shared drive (S:) to your folder

On the machine running **Teleport-Bob**, copy the file Alice shared from `S:`
into your local project folder:

```powershell
Copy-Item "Z:\Non-NV Labs\Quantum\qb_state_483912.txt" "C:\labs\quantum\"
```

Then in Bob's notebook set the filename so it can load the state:

```python
filename = 'qb_state_483912.txt'
```

*(Or simply drag the file from `S:` into your project folder in File Explorer.)*
