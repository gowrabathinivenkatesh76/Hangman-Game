# Hangman-Game
It is just a normal randomized game on designing a text-based  game. The program selects a random word, and the player guesses one letter at a time to uncover the word. You can set a limit on the number of incorrect guesses allowed.

import random

# List of words to choose from
word_list = ['python', 'javascript', 'hangman', 'computer', 'programming', 'developer', 'algorithm']

# Function to select a random word from the list
def get_random_word():
    return random.choice(word_list)

# Function to display the current state of the word and guessed letters
def display_word(word, guessed_letters):
    display = ''.join([letter if letter in guessed_letters else '_' for letter in word])
    return display

# Function to play the Hangman game
def play_hangman():
    word = get_random_word()  # Select a random word
    guessed_letters = []  # List of guessed letters
    incorrect_guesses = 0  # Counter for incorrect guesses
    max_incorrect_guesses = 6  # Limit on incorrect guesses
    
    print("Welcome to Hangman!")
    print("Try to guess the word.")
    
    while incorrect_guesses < max_incorrect_guesses:
        # Display the current state of the word
        print(f"Word: {display_word(word, guessed_letters)}")
        print(f"Incorrect guesses remaining: {max_incorrect_guesses - incorrect_guesses}")
        print(f"Guessed letters: {', '.join(guessed_letters)}")
        
        # Get a valid letter guess from the player
        guess = input("Enter a letter: ").lower()
        
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a valid single letter.")
            continue
        
        if guess in guessed_letters:
            print(f"You've already guessed '{guess}'. Try again.")
            continue
        
        guessed_letters.append(guess)
        
        if guess in word:
            print(f"Good guess! '{guess}' is in the word.")
        else:
            incorrect_guesses += 1
            print(f"Oops! '{guess}' is not in the word.")
        
        # Check if the word has been fully guessed
        if all(letter in guessed_letters for letter in word):
            print(f"Congratulations! You've guessed the word: {word}")
            break
    else:
        print(f"Game Over! The word was: {word}")

# Run the game
if __name__ == "__main__":
    play_hangman()

