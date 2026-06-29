# Preparation Checklist — Quantum Teleportation Lab

Step-by-step checklist to prepare a **fresh Windows machine** to run Andrew
Glassner's Quantum Teleportation notebooks (SIGGRAPH 2026).

Work through it top to bottom. Each step has a checkbox, the exact command(s),
and what you should see when it worked.

> **All terminal commands run from a single working folder** that you set up in
> Step 3 (e.g. `C:\SiggraphQuantumClass`). That's the only absolute path you type —
> after that, keep using the **same PowerShell window** and every path below is
> written **relative to that folder**. Don't `cd` elsewhere unless a step says so.

> This checklist and `requirements.txt` live in the repo's **`setup/`** folder, so
> after cloning (Step 4) you'll find them at `Quantum-Teleportation\setup\`.

> The notebooks need: **qiskit**, **qiskit-aer**, **matplotlib**, **numpy**,
> **pylatexenc**, and **Jupyter**. (`time` is part of Python's standard library —
> nothing to install.)

---

## Step 1 — Install Python

- [ ] Download **Python 3.13** (3.11 or 3.12 also fine) from
      <https://www.python.org/downloads/windows/>
- [ ] Run the installer and **check "Add python.exe to PATH"** on the first screen
- [ ] Click *Install Now*
- [ ] Open a **new** PowerShell window and verify:
  ```powershell
  python --version
  pip --version
  ```
  ✅ Expect: `Python 3.13.x` and a pip version.

## Step 2 — Install Git

- [ ] If Git isn't installed, get it from <https://git-scm.com/download/win>
- [ ] Verify:
  ```powershell
  git --version
  ```
  ✅ Expect: a git version.

## Step 3 — Open a terminal in your working folder

- [ ] Pick (or create) one folder to hold everything, then `cd` into it. **This is
      the only absolute path you'll type** — every command after this runs from here.
  ```powershell
  cd "C:\SiggraphQuantumClass"
  ```
  (Create it first if it doesn't exist: `mkdir "C:\SiggraphQuantumClass"`.)
  ✅ From now on, keep using **this same PowerShell window**. All paths below are
  relative to this folder.

## Step 4 — Clone the project

- [ ] Clone the repo (downloads into a `Quantum-Teleportation` subfolder):
  ```powershell
  git clone https://github.com/blueberrymusic/Quantum-Teleportation.git
  ```
- [ ] Confirm the files are there:
  ```powershell
  ls Quantum-Teleportation
  ```
  ✅ Expect: `Intro-2026.ipynb`, `Teleport-Alice-2026.ipynb`,
  `Teleport-Bob-2026.ipynb`, the PDF, the PNG, and `README.md`.

## Step 5 — Create an isolated virtual environment

- [ ] Create and activate the venv (creates a `.venv` subfolder in your working
      folder):
  ```powershell
  python -m venv .venv
  .\.venv\Scripts\Activate.ps1
  ```
  ✅ Expect: your prompt now starts with **`(.venv)`**.
- [ ] **If activation is blocked** ("running scripts is disabled on this system"),
      run this once, then re-run the activate line:
  ```powershell
  Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
  ```

> To leave the venv later: `deactivate`. Each new PowerShell session, `cd` back to
> your working folder and re-run `.\.venv\Scripts\Activate.ps1`.

## Step 6 — Install the dependencies

- [ ] With `(.venv)` active:
  ```powershell
  python -m pip install --upgrade pip
  pip install -r Quantum-Teleportation\setup\requirements.txt
  ```
  (This is the slow step — it downloads qiskit + aer. Give it a few minutes.)
- [ ] Confirm the key packages installed:
  ```powershell
  pip show qiskit qiskit-aer
  ```
  ✅ Expect: `qiskit 2.4.2` and `qiskit-aer 0.17.2`.

## Step 7 — Register the venv as a Jupyter kernel

- [ ] With `(.venv)` active:
  ```powershell
  python -m ipykernel install --user --name quantum-teleport --display-name "Python (Quantum Teleport)"
  ```
  ✅ Expect: `Installed kernelspec quantum-teleport in ...`
- [ ] Verify it registered:
  ```powershell
  jupyter kernelspec list
  ```
  ✅ Expect: `quantum-teleport` appears in the list.

## Step 8 — Launch Jupyter and open the notebooks

- [ ] Enter the project subfolder and start the server:
  ```powershell
  cd Quantum-Teleportation
  jupyter notebook
  ```
  (Your browser opens automatically. If not, paste the `http://localhost:8888/...`
  URL printed in the terminal.)
- [ ] Open the notebooks in this order:
  1. `Intro-2026.ipynb`
  2. `Teleport-Alice-2026.ipynb`
  3. `Teleport-Bob-2026.ipynb`
- [ ] In each notebook, set the kernel:
      **Kernel → Change kernel → "Python (Quantum Teleport)"**
- [ ] Run cells with **Shift+Enter**.

> Keep the PowerShell window open while you work — it's the running server.
> To stop cleanly: return to the terminal and press **Ctrl+C** (then `cd ..` to go
> back to your working folder).

## Step 9 — Verify the environment (optional sanity check)

- [ ] With `(.venv)` active, run:
  ```powershell
  python -c "from qiskit import QuantumCircuit, transpile; from qiskit_aer import Aer; b=Aer.get_backend('aer_simulator'); qc=QuantumCircuit(2,2); qc.h(0); qc.cx(0,1); qc.measure([0,1],[0,1]); print(b.run(transpile(qc,b),shots=128).result().get_counts())"
  ```
  ✅ Expect: a result like `{'00': 64, '11': 64}` — that means every notebook
  import resolves and the simulator runs.

---

## Important: the notebooks are intentionally incomplete

Per the repo README, the notebooks have **blank spots where you write your own
code** — that's the whole point of the lab. A cell may raise an error until you
fill in the missing piece. This checklist guarantees the **environment** is
correct; completing the **exercises** is up to you. The full explanation (and
Chapter 7 of Glassner's book) is in
`Combined-Quantum-Teleportation-Notes-Glassner.pdf`.

---

## Quick reference — confirmed working versions (Windows 11, 2026-06-28)

| Component   | Version |
|-------------|---------|
| Python      | 3.13.5  |
| qiskit      | 2.4.2   |
| qiskit-aer  | 0.17.2  |
| matplotlib  | 3.11.0  |
| numpy       | 2.4.6   |
| notebook    | 7.5.7   |
| ipykernel   | 7.3.0   |

These are pinned in `requirements.txt` in this same folder.
