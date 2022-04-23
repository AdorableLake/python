# Part1(2020.02.09)

## Target: Use _while_ loop to create a guessing game.

```python
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
## There is a little Guessing-Game writen by python. If you have some interests, try to play with it in your IDE!
