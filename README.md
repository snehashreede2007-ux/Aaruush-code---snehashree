import random

# Number Guessing Game
# The computer randomly chooses a number between 1 and 100.
# The player has to guess the number, receiving hints after each guess.
# The game tracks wins and allows unlimited attempts per round.

def display_welcome():
    print("Welcome to the Number Guessing Game!")
    print("=======================================")
    print("I'm thinking of a number between 1 and 100.")
    print("Try to guess it in as few attempts as possible!")
    print("Type 'quit' at any time during guessing to exit the game.")
    print("=======================================\n")

def get_valid_guess():
    while True:
        guess =input("Enter your guess (1-100): ")
        
        if guess.lower() == 'quit':
            return None
            
        try:
            guess= int(guess)
            if 1 <= guess<= 100:
                return guess
            else:
                print("Please enter a number between 1 and 100.")
        except ValueError:
            print("Invalid input! Please enter a number or 'quit' to exit.")

def play_game():
    secret_number = random.randint(1,100)
    attempts = 0
    
    print("\nNew game started! Guess the number between 1 and 100.")
    print("You have unlimited attempts!")
    
    while True:
        attempts += 1
        guess = get_valid_guess()
        
        if guess is None:
            print("\nGame cancelled. The number was",secret_number)
            return False, attempts
            
        if guess == secret_number:
            print("\nCongratulations! You guessed the number",secret_number," !")
            print("It took you",attempts," attempts.")
            
            if attempts == 1:
                print("Perfect guess! You're a mind reader!")
            elif attempts <= 5 and attempts>1:
                print("Excellent! You're really good at this!")
            elif attempts <= 10 and attempts>5:
                print("Good job! That was pretty quick!")
            else:
                print("Persistence pays off! Well done!")
                
            return True, attempts
            
        elif guess < secret_number:
            difference = secret_number - guess
            if difference <= 5:
                print("Very close! Just a bit higher...")
            elif difference <= 15 and difference>5:
                print("Getting warmer! Try a higher number.")
            else:
                print("Too low! Try a higher number.")
        else:
            difference = guess - secret_number
            if difference <= 5:
                print("Very close! Just a bit lower...")
            elif difference <= 15 and difference>5:
                print("Getting warmer! Try a lower number.")
            else:
                print("Too high! Try a lower number.")

def display_stats(wins, losses, total_attempts, games_played, best_score):
    print("\nGame Statistics:")
    print("===================")
    print("Total games played: ",games_played)
    print("Wins: ",wins)
    print("Losses: ",losses)
    
    if games_played > 0:
        win_percentage = (wins / games_played) * 100
        avg_attempts = total_attempts / games_played
        print("Win percentage: ",win_percentage,"%")
        print("Average attempts per game: ",avg_attempts)
        
        if best_score is not None:
            print("Best score (fewest attempts): ",best_score)
    
    print("==========================================\n")

def main_menu():
    wins = 0
    losses = 0
    total_attempts = 0
    games_played = 0
    best_score = 0
    
    while True:
        display_welcome()
        display_stats(wins, losses, total_attempts, games_played, best_score)
        
        print("Menu Options:")
        print("1. Play Game")
        print("2. View Instructions")
        print("3. Reset Statistics")
        print("4. Quit")
        
        choice =input("\nEnter your choice (1-4): ")
        
        if int(choice) == 1:
            result, attempts = play_game()
            games_played += 1
            total_attempts += attempts
            
            if result:
                wins += 1
                if best_score==0 or attempts < best_score:
                    best_score = attempts
                    print(" New best score!")
            else:
                losses += 1
                
            input("\nPress Enter to continue...")
            
        elif int(choice) == 2:
            print("\nGame Instructions:")
            print("====================")
            print("• I'll think of a random number between 1 and 100")
            print("• You have to guess what number I'm thinking of")
            print("• I'll tell you if your guess is too high or too low")
            print("• Try to guess it in as few attempts as possible")
            print("• You have unlimited attempts - take your time!")
            print("• Type 'quit' during guessing to exit the current game")
            print("• The game tracks your best score (fewest attempts)")
            print("====================\n")
            input("Press Enter to return to menu...")
            
        elif int(choice) == 3:
            wins = 0
            losses = 0
            total_attempts = 0
            games_played = 0
            best_score = 0
            print("\nStatistics have been reset!")
            input("Press Enter to continue...")
            
        elif int(choice) == 4:
            print("\nThank you for playing! Goodbye!")
            break
            
        else:
            print("\nInvalid choice! Please enter 1, 2, 3, or 4.")
            input("Press Enter to continue...")

if __name__ == "__main__":
    main_menu()
