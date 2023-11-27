# Hangman-Game
import random

def choose_word():
    words = ["python", "hangman", "cat", "lord", "dog", "male"]
    return random.choice(words)

def display(word, guessed_word):
    display = ""
    for letter in word:
        if letter in guessed_word:
            display += letter
        else:
            display += "_"
    return display  # Added return statement to return the display string

def hangman():
    MAX_TRY = 6  # Corrected variable name to follow Python convention
    incorrect_guess = 0
    guessed_letters = []
    secret_word = choose_word()
    
    print("Welcome to Hangman!")

    while incorrect_guess < MAX_TRY:
        print(display(secret_word, guessed_letters))
        guess = input("Please type in a letter to guess: ").lower()

        if guess.isalpha() and len(guess) == 1:  # Corrected the conditions
            guessed_letters.append(guess)
            if guess not in secret_word:
                incorrect_guess += 1

        if all(letter in guessed_letters for letter in secret_word):
            print("Congratulations! You won the game.")
            break

        print("Incorrect guesses:", incorrect_guess)

    else:
        print("Sorry, you ran out of guesses. The word was:", secret_word)

# Allow replay
while True:
    hangman()
    replay = input("Do you want to play again? (yes/no): ").lower()
    if replay != "yes":
        break

print("Thanks for playing Hangman!")
