import tkinter as tk
from tkinter import messagebox
import random

class GuessTheNumberGame:
    def _init_(self, master):
        self.master = master
        self.master.title("Guess the Number Game")
        self.master.geometry("400x200")  # Set the initial size of the window

        # Set the background color to pink
        self.master.configure(bg='pink')

        self.secret_number = random.randint(1, 100)
        self.attempts = 0

        self.create_widgets()

    def create_widgets(self):
        # Set the font size to 16
        label_font = ("Helvetica", 16)

        self.label = tk.Label(self.master, text="Welcome to Guess the Number!", font=label_font, bg='pink')
        self.label.pack()

        self.instructions = tk.Label(self.master, text="I have selected a number between 1 and 100. Can you guess it?",
                                     font=label_font, bg='pink')
        self.instructions.pack()

        entry_font = ("Helvetica", 14)
        self.guess_entry = tk.Entry(self.master, font=entry_font)
        self.guess_entry.pack()

        button_font = ("Helvetica", 12)
        self.guess_button = tk.Button(self.master, text="Submit Guess", command=self.check_guess, font=button_font)
        self.guess_button.pack()

    def check_guess(self):
        try:
            guess = int(self.guess_entry.get())
            self.attempts += 1

            if guess == self.secret_number:
                messagebox.showinfo("Congratulations", f"You guessed the number in {self.attempts} attempts. 🎉")

                # Display dancing man in a larger font
                dancing_font = ("Helvetica", 36)
                dancing_label = tk.Label(self.master, text="🕺", font=dancing_font, bg='pink')
                dancing_label.pack()

                self.master.update()  # Force the update to display the dancing man

                self.master.after(3000, self.reset_game)  # Close the GUI after 3 seconds

            elif guess < self.secret_number:
                messagebox.showinfo("Incorrect Guess", "Too low. Try again.")
            else:
                messagebox.showinfo("Incorrect Guess", "Too high. Try again.")

        except ValueError:
            messagebox.showerror("Invalid Input", "Please enter a valid number.")

    def reset_game(self):
        self.master.destroy()

def main():
    root = tk.Tk()
    game = GuessTheNumberGame(root)
    root.mainloop()

if _name_ == "_main_":
    main()
