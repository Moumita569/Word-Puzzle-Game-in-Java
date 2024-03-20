#Word-Puzzle-Game-in-Java

package projectoop;

import java.util.HashSet;
import java.util.Scanner;

public class WordPuzzleGame2 {
    private int count;
    private boolean passfirstround;

    public WordPuzzleGame2() {
        count = 0;
        passfirstround = false;
    }

    public void gamerules() {
        System.out.println("Round 1."
                + "\nRules:"
                + "\n***Guess a word by processing from the Wordtable's Alphabet."
                + "\n***There are three levels - Round 1 & Round 2."
                + "\n***In Round 1,The word must be contained with three characters."
                + "\n***Remember, you can guess three different words only three times."
                + "\n***you can use one letter four times."
                + "\n***Every correct word = 10 points, wrong word = -2 points");
    }
    public void firstround() {
        Scanner sc = new Scanner(System.in);
        String[][] wordTable = {
                {"F", "O", "J"},
                {"W", "A", "R"},
                {"N", "M", "A"}
        };
        printWordTable(wordTable);
        String[] correctWords = {"OWN", "JAM", "JAR", "FAR", "WAR", "MAN", "FAN", "RAW", "JAW", "RAN"};
        int wrongGuess = 0;
        int guessLimit = 0;
        HashSet<String> guessedWords = new HashSet<>();
        boolean gameOver = false;
        passfirstround = false;

        while (!gameOver) {
            System.out.print("Enter your guess: ");
            String guessingWord = sc.nextLine();
            boolean correctGuess = false;

            if (guessedWords.contains(guessingWord.toUpperCase())) {
                System.out.println("You have already guessed that word. Try a different one:");
                continue;
            }

            for (String correctWord : correctWords) {
                if (guessingWord.equalsIgnoreCase(correctWord)) {
                    correctGuess = true;
                    break;
                }
            }

            if (correctGuess) {
                guessLimit++;
                count += 10;
                System.out.println("You got " + count + " points");
            } else {
                System.out.println("Wrong guess.");
                count -= 2;
                wrongGuess++;
                if (wrongGuess >= 3) {
                    System.out.println("Game over");
                    gameOver = true;
                    break;
                }
            }

            guessedWords.add(guessingWord.toUpperCase());

            if (wrongGuess >= 3) {
                System.out.println("Game over");
                gameOver = true;
            } else if (guessLimit >= 3) {
                passfirstround = true;
                break;
            }
        }

        if (!passfirstround) {
            System.out.println("You did not win the first round. So, you cannot play the next round.");
        }
    }

    public void gamerules2() {
        System.out.println("\nRound 2"
                + "\n***Rules:"
                + "\n***Guess a word by processing from the Wordtable's Alphabet."
                + "\n***In Round 2,The word must be contained with minimum five characters."
                + "\n***you have to guess two different words in this round."
                + "\n***you can use one letter only four times."
                + "\n***Every correct word = 10 points, wrong word = -2 points");
    }


    public void secondround() {
        Scanner sc = new Scanner(System.in);
        String[][] wordTable2 = {
                {"E", "G", "I"},
                {"P", "P", "L"},
                {"T", "R", "A"}
        };
        printWordTable(wordTable2);
        String[] correctWords = {"APPLE", "TIGER", "TRAPPER"};
        int guessLimit = 0;
        HashSet<String> guessedWords = new HashSet<>();
        boolean gameOver = false;

        while (guessLimit < 2 && !gameOver) {
            System.out.print("Enter your guess: ");
            String guessingWord = sc.nextLine();
            boolean correctGuess = false;

            if (guessedWords.contains(guessingWord.toUpperCase())) {
                System.out.println("You have already guessed that word. Try a different one:");
                continue;
            }

            for (String correctWord : correctWords) {
                if (guessingWord.equalsIgnoreCase(correctWord)) {
                    correctGuess = true;
                    break;
                }
            }

            if (correctGuess) {
                guessLimit++;
                count += 10;
                System.out.println("You got " + count + " points");
            } else {
                System.out.println("Wrong guess.");
                count -= 2;
            }

            guessedWords.add(guessingWord.toUpperCase());

            if (guessLimit > 2) {
                System.out.println("Game over.");
                gameOver = true;
            }
        }
    }

    public void startGame() {
        gamerules();
        firstround();

        if (passfirstround) {
            if (count > 20)
                System.out.println("***Wow!!You have Unlocked 2 (**) Star"
                        + "\nFor gaining 5(*****) Star, you have to get 50 points in the next round. Now, Continue....");
            gamerules2();
            secondround();
            if (count == 50) {
                System.out.println("Congratulations. You have unlocked all (*****) stars."
                        + "\nWinner!!!!");
            }
        }
        System.out.println("Final Score: " + count);
    }

    private void printWordTable(String[][] wordTable) {
        System.out.println("\nHere is your puzzle. Now think and solve.");
        for (String[] row : wordTable) {
            for (String cell : row) {
                System.out.print(cell + "\t");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        WordPuzzleGame2 game = new WordPuzzleGame2();
        game.startGame();
    }
}
