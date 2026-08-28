# 1st-program
"""Rakhi Quest - a tiny festive game made for a beloved sister.

Run with: python gift.py
"""

import random
import tkinter as tk
from tkinter import messagebox


WIDTH = 760
HEIGHT = 560
GAME_TIME = 30


class RakhiQuest:
    def __init__(self, root):
        self.root = root
        self.root.title("Rakhi Quest - A Gift for My Sister")
        self.root.resizable(False, False)
        self.root.configure(bg="#fff3e8")

        self.score = 0
        self.time_left = GAME_TIME
        self.playing = False
        self.player_x = WIDTH // 2
        self.items = []
        self.after_ids = []

        self._build_header()
        self.canvas = tk.Canvas(
            root, width=WIDTH, height=HEIGHT, bg="#261342",
            highlightthickness=0
        )
        self.canvas.pack(padx=14, pady=(0, 14))
        self._draw_background()

        self.root.bind("<Left>", lambda _: self.move(-35))
        self.root.bind("<Right>", lambda _: self.move(35))
        self.root.bind("a", lambda _: self.move(-35))
        self.root.bind("d", lambda _: self.move(35))
        self.root.bind("<space>", lambda _: self.start_game())

    def _build_header(self):
        header = tk.Frame(self.root, bg="#fff3e8")
        header.pack(fill="x", padx=18, pady=(14, 8))
        tk.Label(
            header, text="RAKHI QUEST", font=("Segoe UI", 22, "bold"),
            fg="#8e2457", bg="#fff3e8"
        ).pack(side="left")
        self.score_label = tk.Label(
            header, text="Score: 0", font=("Segoe UI", 12, "bold"),
            fg="#d45d32", bg="#fff3e8"
        )
        self.score_label.pack(side="right", padx=(20, 0))
        self.timer_label = tk.Label(
            header, text="Time: 30", font=("Segoe UI", 12, "bold"),
            fg="#d45d32", bg="#fff3e8"
        )
        self.timer_label.pack(side="right")

    def _draw_background(self):
        self.canvas.create_text(
            WIDTH // 2, 36, text="Catch the love, leave the worries!",
            fill="#ffd166", font=("Segoe UI", 18, "bold")
        )
        self.canvas.create_text(
            WIDTH // 2, 68, text="Move with ← → or A / D  •  Press SPACE to start",
            fill="#e8c7f5", font=("Segoe UI", 11)
        )
        for x, y, color in [
            (45, 40, "#f94144"), (710, 42, "#f9c74f"),
            (90, 470, "#90be6d"), (675, 465, "#f9844a"),
        ]:
            self.canvas.create_oval(x - 10, y - 10, x + 10, y + 10,
                                    fill=color, outline="")
            self.canvas.create_oval(x - 4, y - 17, x + 4, y + 17,
                                    fill=color, outline="")
            self.canvas.create_oval(x - 17, y - 4, x + 17, y + 4,
                                    fill=color, outline="")

        self.player = self.canvas.create_oval(
            self.player_x - 46, HEIGHT - 70, self.player_x + 46, HEIGHT - 32,
            fill="#ffb703", outline="#ffd166", width=3
        )
        self.canvas.create_text(
            self.player_x, HEIGHT - 51, text="♡  SIS  ♡",
            fill="#7b1e4d", font=("Segoe UI", 12, "bold"), tags="player_text"
        )
        self.start_button = self.canvas.create_rectangle(
            WIDTH // 2 - 92, HEIGHT // 2 - 30, WIDTH // 2 + 92, HEIGHT // 2 + 30,
            fill="#e63972", outline="#ffb3c6", width=3, tags="start"
        )
        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2, text="START GAME",
            fill="white", font=("Segoe UI", 16, "bold"), tags="start"
        )
        self.canvas.tag_bind("start", "<Button-1>", lambda _: self.start_game())

    def move(self, amount):
        if not self.playing:
            return
        self.player_x = max(55, min(WIDTH - 55, self.player_x + amount))
        self.canvas.coords(self.player, self.player_x - 46, HEIGHT - 70,
                           self.player_x + 46, HEIGHT - 32)
        self.canvas.coords("player_text", self.player_x, HEIGHT - 51)

    def start_game(self):
        if self.playing:
            return
        self.playing = True
        self.score = 0
        self.time_left = GAME_TIME
        self.player_x = WIDTH // 2
        self.items = []
        self.canvas.delete("item")
        self.canvas.delete("start")
        self._update_labels()
        self._spawn_item()
        self._animate()
        self._tick()

    def _spawn_item(self):
        if not self.playing:
            return
        x = random.randint(35, WIDTH - 35)
        kind = random.choice(["heart", "heart", "rakhi", "gift", "oops"])
        colors = {"heart": "#ff4d6d", "rakhi": "#ffd166",
                  "gift": "#06d6a0", "oops": "#9b5de5"}
        symbols = {"heart": "♥", "rakhi": "✦", "gift": "🎁", "oops": "☁"}
        item = self.canvas.create_text(
            x, 95, text=symbols[kind], fill=colors[kind],
            font=("Segoe UI Symbol", 28), tags="item"
        )
        self.items.append((item, kind))
        self.after_ids.append(self.root.after(650, self._spawn_item))

    def _tick(self):
        if not self.playing:
            return
        self.time_left -= 1
        self._update_labels()
        if self.time_left <= 0:
            self.finish_game()
            return
        self.after_ids.append(self.root.after(1000, self._tick))

    def _animate(self):
        if not self.playing:
            return
        for item, kind in self.items[:]:
            self.canvas.move(item, 0, 5)
            coords = self.canvas.coords(item)
            if not coords:
                self.items.remove((item, kind))
                continue
            x, y = coords
            if y >= HEIGHT - 55:
                if abs(x - self.player_x) < 62:
                    self.score += 2 if kind != "oops" else -1
                    self.score = max(0, self.score)
                    self._update_labels()
                self.canvas.delete(item)
                self.items.remove((item, kind))
            elif y > HEIGHT:
                self.canvas.delete(item)
                self.items.remove((item, kind))
        self.after_ids.append(self.root.after(45, self._animate))

    def _update_labels(self):
        self.score_label.config(text=f"Score: {self.score}")
        self.timer_label.config(text=f"Time: {self.time_left}")

    def finish_game(self):
        self.playing = False
        for after_id in self.after_ids:
            self.root.after_cancel(after_id)
        self.after_ids.clear()
        self.canvas.delete("item")
        messagebox.showinfo(
            "Happy Raksha Bandhan!",
            f"You collected {self.score} love points!\n\n"
            "Dear Sis, you make every day brighter.\n"
            "Happy Rakhi! I am lucky to have you. ♥"
        )
        self.canvas.create_rectangle(
            WIDTH // 2 - 125, HEIGHT // 2 - 30, WIDTH // 2 + 125, HEIGHT // 2 + 30,
            fill="#e63972", outline="#ffb3c6", width=3, tags="start"
        )
        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2, text="PLAY AGAIN",
            fill="white", font=("Segoe UI", 16, "bold"), tags="start"
        )
        self.canvas.tag_bind("start", "<Button-1>", lambda _: self.start_game())


if __name__ == "__main__":
    app = tk.Tk()
    game = RakhiQuest(app)
    app.mainloop()