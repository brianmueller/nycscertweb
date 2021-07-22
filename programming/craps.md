# Craps pre-work

## Context
Prior to starting the program, we were given preliminary Java assignments to complete so that we would all be on the same page. In fact, as a part of the application, we were allowed to use assignments from the pre-work to demonstrate our prior knowledge. Being someone who loves Java as well as the game of Craps, I chose this assignment.

## Task
The task was to create a virtual simulation of the dice game of Craps. There were a number of methods to write:
* A `main` method to actually run the game. The input was a total number of rounds to play, printing out the results.
* A `roll` method that simply returned a random number from a die.
* A `shoot` method that was generalized to any configuration of dice size/number, which is great if I want to extend this program.
* A `round` method. This was the heart of the program, where all the rules of Craps are observed using two dice:
  * If a shooter rolls 7 or 11, they win!
  * If a shooter rolls 2, 3, or 12, they lose.
  * If a shooter rolls any of the remaining values (4, 5, 6, 8, 9, 10), that is their "point". If they roll their point, they win. If they roll 7, they "crap" out.

## Process
As one can observe from the rules above, this program was going to involve plenty of `if` statements. Writing that wasn't too difficult. But because of so many blocks nested within each other, it was important to be intentional about indentations, and keep track of my `{}`s.

Perhaps my favorite part of the task was getting to use a `do{} while(condition)` loop. Essentially, a `while(condition){}` loop has no guarantee of running, as the `condition` could be false before the body even runs. However, once a shooter reaches their "point", I knew that they would have to roll _at least_ once. Hence, I planned the following pseudocode:
```
// once the point is established
do{
    // roll the dice
    // if point
        // win
    // else
        // craps
} while( /* dice is not point or craps */)
```
I did end up having to write `System.out.println("Shooter rolled " + diceVal);` twice: once before the loop, and once inside. I'm not sure if there is a more efficient way to do this.

## Challenges
Since I've been teaching Java for a few years, this task was much more fun than it was difficult. It took some time to get the programming I wanted using the right spacing (`System.out.println()`s and `\n`s).

One thing I'm wondering is if there is a way to avoid having to write `return ""` after a branch of conditionals where you _know_ that all possibilities will `return` something ("win" or "lose").

## Result
My final code can be found [here](https://github.com/hunter-teacher-cert/work_csci70900-brianmueller/blob/master/pre/8/Craps.java)

## Next Steps
As Craps is typically a betting game, it would be kind of fun to add a betting functionality to this game and see what the results would be if the user bet a certain amount on the Pass line each round.

---

[Home](../index.md) 