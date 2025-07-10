# Hangman-Game
Create a simple text-based Hangman game whare the player guesses a word one letter at a time
import random

# Step 1: Predefined list of words
word_list = ["apple", "brain", "chair", "zebra", "grape"]

# Step 2: Randomly choose one word
secret_word = random.choice(word_list)
guessed_letters = []
incorrect_guesses = 0
max_guesses = 6

# Function to display current word progress
def display_word():
    display = ""
    for letter in secret_word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "
    return display.strip()

print("🎮 Welcome to Hangman!")
print("Guess the word, one letter at a time.")
print(f"You have {max_guesses} incorrect guesses allowed.\n")

# Step 3: Game loop
while incorrect_guesses < max_guesses:
    print("Word:", display_word())
    guess = input("Enter a letter: ").lower()

    if not guess.isalpha() or len(guess) != 1:
        print("Please enter a single alphabet letter.\n")
        continue

    if guess in guessed_letters:
        print("You already guessed that letter. Try another.\n")
        continue

    guessed_letters.append(guess)

    if guess in secret_word:
        print("✅ Good guess!\n")
    else:
        incorrect_guesses += 1
        print(f"❌ Wrong guess! You have {max_guesses - incorrect_guesses} tries left.\n")

    # Check if player has guessed all letters
    if all(letter in guessed_letters for letter in secret_word):
        print("🎉 Congratulations! You guessed the word:", secret_word)
        break
else:
    print("💀 Game over! The word was:", secret_word)
