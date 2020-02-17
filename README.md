# python

Hi, guys. Here are my python practise notes.
And I will share my practices in next days.

print("click to 简体中文")

# Part1(2020.02.09)
``` python
# Use while loop to create guessing game
secret_word = "westlake"
running = True
guess = ""
guess_count = 0
guess_limit = 3
out_of_guesses = False

print("Hello, my Friend!")
while running:
    if guess_count < guess_limit and not out_of_guesses:
        guess = input("Enter Your Guess: ")
        guess_count += 1
        if guess == secret_word:
           print("Congratulation!")
           running = False
        elif guess == "west":
           print("Wow, you get part of it!")
        elif guess == "lake":
           print("Wow, you get part of it!")
        elif guess == "lakewest":
           print("It seems that you got a wrong direction!")
        else:
           print("Hm, there is happened to get some trouble with you.\nDo it again!")
    else:
        out_of_guesses = True
        running = False

if out_of_guesses and not running:
    print("YOU ARE OUT OF TIMES!")
else:
    print("YOU DID NOT BAD!")

print("Game Over!")
```
There is a little Guessing-Game writen by python. 
If you guys have some interests, try to play with it in your IDE!
