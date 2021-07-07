from tkinter import *
import math

# ---------------------------- CONSTANTS ------------------------------- #
PINK = "#e2979c"
RED = "#e7305b"
GREEN = "#9bdeac"
YELLOW = "#f7f5dd"
FONT_NAME = "Courier"
WORK_MIN = 20
SHORT_BREAK_MIN = 5
LONG_BREAK_MIN = 20
reps = 0
timer = None


# ---------------------------- TIMER RESET ------------------------------- #

# ---------------------------- TIMER MECHANISM ------------------------------- # 
def timer_start():
    global reps
    reps += 1
    long_break_sec = LONG_BREAK_MIN * 60
    short_break_sec = SHORT_BREAK_MIN * 60
    work_sec = WORK_MIN * 60

    if reps == 8:
        count_down(long_break_sec)
        timer_lable.config(text="BREAK_20M", fg=YELLOW)

    elif reps % 2 == 0:
        count_down(short_break_sec)
        timer_lable.config(text="BREAK_5M", fg=YELLOW)

    else:
        count_down(work_sec)
        timer_lable.config(text="WORK_25", fg=RED)


# ---------------------------- COUNTDOWN MECHANISM ------------------------------- #
def count_down(count):
    global timer
    min_text = math.floor(count / 60)
    if min_text < 10:
        min_text = f"0{min_text}"
    sec_text = count % 60
    # if sec_text == 0:
    #     sec_text = "00"

    if sec_text < 10:
        sec_text = f"0{sec_text}"
    canvas.itemconfig(timer_text, text=f"{min_text}:{sec_text}")
    if count > 0:
        timer = window.after(1000, count_down, count - 1)
    else:
        timer_start()
        marks = ""
        work_session = math.floor(reps / 2)
        for _ in range(work_session):
            marks += "✓"
        check_marks.config(text=marks)


# ---------------------------- UI SETUP ------------------------------- #

window = Tk()
window.title("pomodoro")
window.config(padx=50, pady=50, bg=GREEN)

canvas = Canvas(width=200, height=224, bg=GREEN, highlightthickness=0)
tomato_img = PhotoImage(file="tomato.png")
canvas.create_image(100, 112, image=tomato_img)
timer_text = canvas.create_text(100, 130, text="00:00", font=(FONT_NAME, 35, "bold"), fill="white")
canvas.grid(column=1, row=1)


def reset_clicked():
    window.after_cancel(timer)
    canvas.itemconfig(timer_text, text="00:00")
    timer_lable.config(text="Timer")
    check_marks.config(text="")
    global reps
    reps = 0


timer_lable = Label(text="Timer", font=(FONT_NAME, 45, "bold"), fg=PINK, bg=GREEN)
timer_lable.grid(column=1, row=0)

start_button = Button(text="Start", font=(FONT_NAME, 18, "bold"), command=timer_start)
start_button.grid(column=0, row=2)

reset_button = Button(text="Reset", font=(FONT_NAME, 18, "bold"), command=reset_clicked)
reset_button.grid(column=2, row=2)

check_marks = Label(font=(FONT_NAME, 22, "bold"), fg=YELLOW, bg=GREEN)
check_marks.grid(column=1, row=2)

window.mainloop()
