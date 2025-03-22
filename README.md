# Sample-Chatbot
Sample AI conversational project.

import tkinter as tk
from nltk.chat.util import Chat, reflections

# Define pairs of questions and answers
pairs = [
    [
        r"hey|hello?",
        ["I am a FAQ chatbot. You can call me FAQBot!"]
    ],
    [
        r"what are your opening hours?",
        ["We are open from 9 AM to 6 PM, Monday to Friday."]
    ],
    [
        r"how do I reset my password?",
        ["You can reset your password by visiting the 'Forgot Password' page."]
    ],
    [
        r"where are you located?",
        ["We are located at 123 Main Street, Cityville."]
    ],
    [
        r"how can I contact support?",
        ["You can contact support at support@example.com or call us at 123-456-7890."]
    ],
    [
        r"quit",
        ["Bye! Have a great day."]
    ]
]

# Create a chatbot instance
chatbot = Chat(pairs, reflections)

# Function to handle sending messages
def send_message():
    user_input = entry.get()  # Get user input from the entry widget
    response = chatbot.respond(user_input)  # Get chatbot response
    chat_log.config(state=tk.NORMAL)  # Enable the text widget to insert text
    chat_log.insert(tk.END, f"You: {user_input}\nFAQBot: {response}\n\n")  # Add conversation to the chat log
    chat_log.config(state=tk.DISABLED)  # Disable the text widget to prevent editing
    entry.delete(0, tk.END)  # Clear the entry widget


# Create the main application window
root = tk.Tk()
root.title("FAQ Chatbot")

# Create a text widget to display the chat log
chat_log = tk.Text(root, state=tk.DISABLED, wrap=tk.WORD, bg="yellow", fg="red", font=("Arial"
"Aptos", 12))
chat_log.pack(padx=10, pady=10, fill=tk.BOTH, expand=True)

# Add a scrollbar to the chat log
scrollbar = tk.Scrollbar(root)
scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
chat_log.config(yscrollcommand=scrollbar.set)
scrollbar.config(command=chat_log.yview)

# Display a welcome message
chat_log.config(state=tk.NORMAL)
chat_log.insert(tk.END, "FAQBot: Hi! I'm FAQBot. How can I help you today?\n\n")
chat_log.config(state=tk.DISABLED)

# Create an entry widget for user input
entry = tk.Entry(root, width=50, font=("Arial", 12))
entry.pack(padx=10, pady=10, fill=tk.X)

# Create a button to send the message
send_button = tk.Button(root, text="Send", command=send_message, bg="blue", fg="white", font=("Arial", 12))
send_button.pack(padx=10, pady=10)

# Start the application
root.mainloop()
# Start the conversation
print("Hi! I'm FAQBot. How can I help you today?")
while True:
    user_input = input("You: ")
    if user_input.lower() == "quit":
        print("FAQBot: Bye! Have a great day.")
        break
    response = chatbot.respond(user_input)
    print("FAQBot:", response)

