# Card-Matching-Game

import random
import time

   
ROWS = 4

visual_numbers = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16']
hidden_letters = ['G','D','B','F','H','B','C','D','A','A','E','E','F','H','G','C']



def shuffle():
    '''
    Randomly shuffles the letters of the variable hidden_letters.
    
    Return:
        Shuffled list of hidden_letters.
    '''  
    
    random.shuffle(hidden_letters)
    return hidden_letters



def displayboard(x):
    '''
    This function displays the rows and columns of the game.
    
    Args:
        x: The variable of visual_numbers.
    
    Return:
        A squared grid of the numbers.
    '''
    
    for i in range(0, len(x), ROWS):
        for val in x[i:i + ROWS]:
            print(val.ljust(3), end='')
        print()
 
 
 
def game_loop():
    '''
    This runs the game loop with various conditions.
    
    Return:
        The game algorithm/loop that takes a user input and runs the game.
    '''
    
    total_guesses = 0
    used_numbers = []
    starting_time = int(time.time())
    
    while visual_numbers != hidden_letters:
        
        user_input1, user_input2 = [int(x) for x in input('Guess two squares: ').split()]
        if user_input1 in used_numbers:
            print("Invalid number(s).")
        elif user_input2 in used_numbers:
            print("Invalid number(s).")
        elif (0 < user_input1 <= 16 and 0 < user_input2 <= 16) and user_input1 != user_input2:
            if hidden_letters[user_input1-1] != hidden_letters[user_input2-1]:
                flip_over = visual_numbers[:]
                flip_over[user_input1-1] = hidden_letters[user_input1-1]
                flip_over[user_input2-1] = hidden_letters[user_input2-1]
                displayboard(flip_over)
                time.sleep(2)
                print('\n' * 20)
                displayboard(visual_numbers)
                total_guesses += 1
            else:
                used_numbers.extend((user_input1, user_input2))
                visual_numbers[user_input1-1] = hidden_letters[user_input1-1]
                visual_numbers[user_input2-1] = hidden_letters[user_input2-1]
                print('\n' * 20)
                displayboard(visual_numbers)
                total_guesses += 1
        else:
            print("Invalid number(s).")
            
    ending_time = int(time.time())        
    print('\n' * 20)
    print("You win!")
    displayboard(visual_numbers)
    print("It took you " + str(total_guesses) + " guesses and " + str(ending_time - starting_time) + " seconds.")



def play_game():
    '''
    This brings in the board alongside the shuffle function to run the game.
    
    Return:
        The overall game system takes place now.
    '''
    
    shuffle()
    displayboard(visual_numbers)
    game_loop()
    
  
  
if __name__ == "__main__":
    play_game()
    
       

