 import java.util.Scanner;
import java.util.Timer;
import java.util.TimerTask;

class Quiz {
    private Question[] questions;
    private int currentQuestionIndex;
    private int score;

    public Quiz(Question[] questions) {
        this.questions = questions;
        this.currentQuestionIndex = 0;
        this.score = 0;
    }

    public void displayQuestion() {
        Question currentQuestion = questions[currentQuestionIndex];
        System.out.println("\nQuestion " + (currentQuestionIndex + 1) + ": " + currentQuestion.getQuestion());
        for (int i = 0; i < currentQuestion.getOptions().length; i++) {
            System.out.println((i + 1) + ". " + currentQuestion.getOptions()[i]);
        }
    }

    public int getUserChoice() {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            try {
                System.out.print("Enter your choice (1-" + questions[currentQuestionIndex].getOptions().length + "): ");
                int choice = Integer.parseInt(scanner.nextLine());
                if (choice >= 1 && choice <= questions[currentQuestionIndex].getOptions().length) {
                    return choice;
                } else {
                    System.out.println("Invalid choice. Please enter a number between 1 and " +
                            questions[currentQuestionIndex].getOptions().length + ".");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
    }

    public void checkAnswer(int userChoice) {
        if (userChoice == questions[currentQuestionIndex].getCorrectAnswer()) {
            System.out.println("Correct!\n");
            score++;
        } else {
            System.out.println("Incorrect. The correct answer is " +
                    questions[currentQuestionIndex].getCorrectAnswer() + ": " +
                    questions[currentQuestionIndex].getOptions()[questions[currentQuestionIndex].getCorrectAnswer() - 1] + "\n");
        }
    }

    public void runQuiz(int timeLimitPerQuestion) {
        System.out.println("Welcome to the Quiz!\n");

        Timer timer = new Timer();
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println("Time's up!\n");
                int userChoice = getUserChoice();
                checkAnswer(userChoice);

                currentQuestionIndex++;

                if (currentQuestionIndex == questions.length) {
                    displayResult();
                    timer.cancel();
                } else {
                    displayQuestion();
                }
            }
        }, 0, timeLimitPerQuestion * 1000);

        displayQuestion();
    }

    public void displayResult() {
        System.out.println("Quiz Completed!\n");
        System.out.println("Your Score: " + score + "/" + questions.length + "\n");
        System.out.println("Correct Answers:");
        for (int i = 0; i < questions.length; i++) {
            System.out.println((i + 1) + ". " + questions[i].getQuestion() + " - " +
                    questions[i].getOptions()[questions[i].getCorrectAnswer() - 1]);
        }
        System.out.println("\nThank you for taking the quiz!");
    }
}

class Question {
    private String question;
    private String[] options;
    private int correctAnswer;

    public Question(String question, String[] options, int correctAnswer) {
        this.question = question;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestion() {
        return question;
    }

    public String[] getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }
}

public class QuizApplication {
    public static void main(String[] args) {
        // Sample quiz questions
        Question[] quizQuestions = {
                new Question("What is the capital of France?", new String[]{"Berlin", "Paris", "London", "Rome"}, 2),
                new Question("Which planet is known as the Red Planet?", new String[]{"Mars", "Jupiter", "Venus", "Saturn"}, 1),
                // Add more questions as needed
        };

        // Create a Quiz object and run the quiz
        Quiz quiz = new Quiz(quizQuestions);
        quiz.runQuiz(10); // Set the time limit per question in seconds
    }
}
