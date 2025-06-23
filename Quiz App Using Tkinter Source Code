import tkinter as tk
from tkinter import messagebox

# Sample questions (simulating loaded JSON/text file)
questions = [
    {"question": "What is 2 + 2?", "options": ["3", "4", "5", "6"], "answer": "4"},
    {"question": "What is the capital of France?", "options": ["Berlin", "Madrid", "Paris", "Rome"], "answer": "Paris"},
    {"question": "What is the largest planet?", "options": ["Earth", "Mars", "Jupiter", "Saturn"], "answer": "Jupiter"}
]

class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Quiz App")
        self.root.geometry("400x400")
        self.root.configure(bg="#e0f7fa")  # Light cyan background

        self.current_question = 0
        self.score = 0
        self.selected_option = tk.StringVar()

        # Title label
        self.title_label = tk.Label(root, text="Quiz App", font=("Arial", 16, "bold"), bg="#e0f7fa")
        self.title_label.pack(pady=10)

        # Question label
        self.question_label = tk.Label(root, text="", font=("Arial", 12), bg="#e0f7fa", wraplength=350)
        self.question_label.pack(pady=10)

        # Options (radio buttons)
        for i in range(4):
            rb = tk.Radiobutton(root, text="", variable=self.selected_option, value="", font=("Arial", 10), bg="#e0f7fa")
            rb.pack(anchor="w", padx=20)
            setattr(self, f"option_{i}", rb)

        # Navigation buttons
        self.prev_button = tk.Button(root, text="Previous", command=self.prev_question, bg="#b0bec5")
        self.prev_button.pack(side="left", padx=20, pady=10)

        self.next_button = tk.Button(root, text="Next", command=self.next_question, bg="#b0bec5")
        self.next_button.pack(side="right", padx=20, pady=10)

        self.load_question()

    def load_question(self):
        # Load the current question and options
        q = questions[self.current_question]
        self.question_label.config(text=f"Q{self.current_question + 1}: {q['question']}")
        self.selected_option.set("")  # Reset selection
        for i in range(4):
            getattr(self, f"option_{i}").config(text=q["options"][i], value=q["options"][i])
        self.prev_button.config(state="normal" if self.current_question > 0 else "disabled")

    def next_question(self):
        # Check answer
        if self.selected_option.get():
            if self.selected_option.get() == questions[self.current_question]["answer"]:
                self.score += 1

        self.current_question += 1
        if self.current_question < len(questions):
            self.load_question()
        else:
            self.show_score()

    def prev_question(self):
        self.current_question -= 1
        self.load_question()

    def show_score(self):
        # Determine message based on score
        if self.score == 1:
            message = "Good"
        elif self.score == 2:
            message = "Very Good"
        elif self.score == 3:
            message = "Excellent"
        else:
            message = "Keep Practicing"

        # Show score with message
        messagebox.showinfo("Quiz Finished", f"Your score: {self.score}/{len(questions)}\n{message}")
        self.root.destroy()  # Close the application

# Run the app
root = tk.Tk()
app = QuizApp(root)
root.mainloop()
