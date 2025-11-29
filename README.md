# ♟️ Shredder-iPhone Game Analyzer  
### Analyze complete chess games from the iPhone Shredder app using Stockfish & Jupyter

If you play regularly with **Shredder on iPhone**, you may have experienced a limitation:  
➡️ **you cannot analyze a full game with an engine afterwards.**

This project provides a clean, reproducible solution:  
paste the Shredder move list into the notebook, and obtain:

- full **move-by-move evaluation**  
- **best moves** and **blunders**  
- **mate-in-N detection** (with full forced lines)  
- **beautiful evaluation graphics** (normal scale + Symlog)  
- Stockfish version, metadata, players, ELO, etc.

---

## 📸 Extracting the Game from Shredder

1. Finish your game  
2. Tap **Save / Notation**  
3. Copy only the **moves section** (not the title/header)

<img width="260" height="560" alt="game" src="https://github.com/user-attachments/assets/36191f9e-4c9b-4de1-afca-acb28d3bffb5" />

<img width="260" height="560" alt="notation" src="https://github.com/user-attachments/assets/309cbbd1-f781-4e74-a2f3-98671b577d52" />

Then paste the moves into the Jupyter notebook (cell **#2**, variable `moves_str`).

---

## 📘 Notebook Structure

| Cell | Purpose | what to do ? |
|------|---------|-----------------------|
| **1** | System & module initialization | just run the cell |
| **2** | Paste your Shredder game → `moves_str` | **Put your moves here** (then run the cell) |
| **3** | Game metadata (players, ELO, date…) for final graphics |data for the graphics (run the cell if you change something)|
| **4** | Engine thinking time per move (e.g., `X_secondes = 5`) |**as you like : from 0.1 to ... 5 is great** You can test 60 if you have a coffee break (run the cell) |
| **5** | Cleans notation, runs analysis, produces logs + graphics | (run the cell !) |

A good move is trying with just 0.5 to see ... then for a greater and deeper analyzis, put ... 5 to 60 or ... more...

Time per move:  
- `5` seconds → already very good  
- `0.2` seconds → fast preview  
- `60` seconds →→ deep analysis
- `200` seconds → very very very deep analysis (great for 1 position for example)

---

## 📊 What the Notebook Produces

### 1️⃣ **Full Move-by-Move Analysis**

Each line contains:

- the move number  
- the move played  
- Stockfish evaluation  
- the **best move**  
- evaluation *after* best move

Example:

```
16. b2b3                [+39]            a7a5 (best: f7f5)   [+76]
17. f2f3 (best: g5e3)   [+46]            c8c7 (best: c8a8)   [+17]
18. e2d2 (best: c1c2)   [-17]            f8a8 (best: c5c4)   [-31]
19. d2e2 (best: c1c2)   [-47]            f7f6 (best: a5a4)   [+6]
20. g5e3                [+6]             a5a4 (best: a8c8)   [+2]
```


Explanation of line 18:

- **White move**: `e2-d2`  
- **Best move** was `c1-c2`  
- **Evaluation**: `-47` centipawns (= Black slightly better)

Line 20 (`g5-e3`) shows a case where the played move **was** the best move 😊  

### 2️⃣ Mate-in-N Detection

If a forced mate appears, the notebook prints:

```

45. h4h5 (best: h1h2)   [#-10]   g6h5   [#-9]

```

Meaning:

- White blundered: best was `h1-h2`
- The position is **mate in 10** for Black  
- After Black's reply, it becomes **mate in 9**

You also get the **full forced mate line**:

```

45-Black, #-9:
Mate via: Kh2 Qxg1+ Kxg1 Rxc1+ Kh2 Rh1+ Kxh1 c1=Q+ Kh2 Bc5 Ra1 Qxa1 d6 Qg1+ Kh3 Qh1+ Kg3 Qh4#

45-White, #-10:
Mate via: Kxh5 Kh2 Qxg1+ Kxg1 Rxc1+ Kh2 Rh1+ Kxh1 c1=Q+ Kh2 Bc5 Ra1 Qxa1 d6 Qg1+ Kh3 Qh1+ Kg3 Qh4#

```

---

## 🧮 Final Graphs

A final graphic is generated with:

- evaluation curve  
- symlog scale beyond ±1200  
- thresholds displayed for:
  - ±100 (1 pawn)  
  - ±300 (knight/bishop)  
  - ±500 (rook)  
  - ±700  
- mate-in-N indicators (green), vertically stacked

Example:

<img width="1355" height="758" alt="game-shredder-VPD" src="https://github.com/user-attachments/assets/0df9614a-67f0-4a4b-84f3-7afeabd412cd" />

Notes:

- The horizontal axis uses **half-moves (ply)**  
  - so graphic move 12/13 = “6-White / 6-Black”  
- The Stockfish version is shown (e.g., **Stockfish 14.1**)

---

## 🛠 Requirements

- Python 3  
- `python-chess`  
- `matplotlib`  
- Stockfish installed (path auto-detected)  

---

## 💬 Questions / Feedback

Comments are welcome.  
You can contact me by email:

```

vincent   pinte   at   gmail   com

```

(Just remove spaces and assemble intelligently — you play chess, so you're smart enough 😉)

---

## ⚠️ Compatibility

The notebook processes **Shredder iPhone notation**.

Other notations may work, but are **not guaranteed**.

---

## ✔️ Enjoy!

If this helps you improve your game, analyze your styles, or revisit old matches, feel free to star the project ⭐ or open issues/pull-requests.

Happy analyzing!
```

