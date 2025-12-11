# CodSoft-internship
import java.util.Random;
import java.util.Scanner;

public class NumberGame {
    
    // Constants for game settings
    private static final int MIN_RANGE = 1;
    private static final int MAX_RANGE = 100;
    private static final int MAX_ATTEMPTS = 7; // Limited attempts
    
    // Variable to track rounds won
    private static int roundsWon = 0;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("--- Welcome to the Number Guessing Game! ---");

        boolean playAgain = true;
        
        // 6. Add the option for multiple rounds
        while (playAgain) {
            playRound(scanner);
            
            System.out.println("\n-------------------------------------------");
            System.out.println("Rounds Won: " + roundsWon);
            System.out.print("Do you want to play another round? (yes/no): ");
            String playChoice = scanner.next().toLowerCase();
            
            // Check if the user wants to continue playing
            if (!playChoice.equals("yes")) {
                playAgain = false;
            }
        }
        
        System.out.println("\nThank you for playing! Final Score: " + roundsWon + " round(s) won.");
        scanner.close();
    }

    /**
     * Executes one full round of the number guessing game.
     */
    private static void playRound(Scanner scanner) {
        // 1. Generate a random number within a specified range
        Random random = new Random();
        int targetNumber = random.nextInt(MAX_RANGE - MIN_RANGE + 1) + MIN_RANGE;
        
        int attempts = 0;
        boolean guessedCorrectly = false;
        
        System.out.println("\n--- Starting New Round ---");
        System.out.println("I have generated a number between " + MIN_RANGE + " and " + MAX_RANGE + ".");
        System.out.println("You have " + MAX_ATTEMPTS + " attempts to guess it.");

        // Loop until the number is guessed or attempts run out
        // 4. Repeat steps 2 and 3
        while (attempts < MAX_ATTEMPTS && !guessedCorrectly) {
            // 5. Limit the number of attempts
            System.out.print("\nAttempt " + (attempts + 1) + "/" + MAX_ATTEMPTS + ". Enter your guess: ");
            
            // 2. Prompt the user to enter their guess
            if (scanner.hasNextInt()) {
                int userGuess = scanner.nextInt();
                attempts++; // Increment attempts after a valid guess
                
                // 3. Compare the user's guess and provide feedback
                if (userGuess == targetNumber) {
                    System.out.println("🎉 CONGRATULATIONS! You guessed the number in " + attempts + " attempts.");
                    roundsWon++;
                    guessedCorrectly = true;
                } else if (userGuess < targetNumber) {
                    System.out.println("Too low. Try again!");
                } else { // userGuess > targetNumber
                    System.out.println("Too high. Try again!");
                }
            } else {
                System.out.println("Invalid input. Please enter a number.");
                scanner.next(); // Consume the invalid input to prevent an infinite loop
            }
        }

        // If the user did not guess correctly after all attempts
        if (!guessedCorrectly) {
            System.out.println("\n😔 You ran out of attempts!");
            System.out.println("The correct number was: " + targetNumber);
        }
        
        // 7. Display the user's score (attempts taken)
        if (guessedCorrectly) {
            System.out.println("Score for this round: " + (MAX_ATTEMPTS - attempts + 1) + " point(s) (lower attempts = higher score).");
        }
    }
}
