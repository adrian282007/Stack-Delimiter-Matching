# Stack-Delimiter-Matching
/* Description: Stack-based delimiter checker with full operation trace displayed.
Programmed by: [ADRIAN DAVE LUMANTA] [BSIT-2] [48143] [DATA STRUCTURE AND ALGORITHM]
Last Modified: 2026-10-16
Version: 1.1
Acknowledgements: DOLA AI
*/

import java.util.Scanner;
import java.util.Stack;

public class DelimiterCheckerWithTrace {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Input: ");
        String input = scanner.nextLine();
        scanner.close();

        Stack<Character> stack = new Stack<>();
        boolean isValid = true;
        String reason = "";

        System.out.println("\n--- Execution Trace ---");
        for (int i = 0; i < input.length(); i++) {
            char ch = input.charAt(i);

            if (ch == '(' || ch == '[' || ch == '{') {
                System.out.println("Read: " + ch);
                System.out.println("Operation: PUSH");
                stack.push(ch);
                System.out.println("Stack: " + stackDisplay(stack) + "\n");
            }
            else if (ch == ')' || ch == ']' || ch == '}') {
                System.out.println("Read: " + ch);

                if (stack.isEmpty()) {
                    System.out.println("Operation: ERROR — Stack empty!");
                    isValid = false;
                    reason = "Closing delimiter '" + ch + "' has no matching opening delimiter.";
                    System.out.println("Reason: " + reason + "\n");
                    break;
                }

                char top = stack.peek();
                System.out.println("Operation: PEEK → " + top);

                if ((ch == ')' && top == '(') ||
                    (ch == ']' && top == '[') ||
                    (ch == '}' && top == '{')) {
                    System.out.println("Operation: POP");
                    stack.pop();
                    System.out.println("Stack: " + stackDisplay(stack) + "\n");
                } else {
                    isValid = false;
                    reason = "Mismatched delimiters: expected closing for '" + top + "' but found '" + ch + "'.";
                    System.out.println("Operation: MISMATCH DETECTED");
                    System.out.println("Reason: " + reason + "\n");
                    break;
                }
            }
        }

        if (isValid && !stack.isEmpty()) {
            isValid = false;
            reason = "Unmatched opening delimiter(s) remain.";
            System.out.println("Final Check: Stack not empty → " + reason);
        }

        System.out.println("--- Result ---");
        System.out.println(isValid ? "Valid" : "Invalid — " + reason);
    }

    // Helper to format stack display
    private static String stackDisplay(Stack<Character> s) {
        if (s.isEmpty()) return "(empty)";
        StringBuilder sb = new StringBuilder();
        for (char c : s) sb.append(c).append(" ");
        return sb.toString().trim();
    }
}






/* Description: Stack-based program to check if parentheses, brackets, and braces are properly matched and nested.
Programmed by: [ADRIAN DAVE LUMANTA] [BSIT-2] [48143] [DATA STRUCTURE AND ALGORITHM]
Last Modified: 2026-10-16
Version: 1.0
Acknowledgements: DOLA AI
*/

import java.util.Scanner;
import java.util.Stack;

public class DelimiterChecker {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter sequence: ");
        String input = scanner.nextLine();
        scanner.close();

        Stack<Character> stack = new Stack<>();
        boolean isValid = true;
        String reason = "";

        for (int i = 0; i < input.length(); i++) {
            char ch = input.charAt(i);

            // Push opening delimiters
            if (ch == '(' || ch == '[' || ch == '{') {
                stack.push(ch);
            }
            // Process closing delimiters
            else if (ch == ')' || ch == ']' || ch == '}') {
                if (stack.isEmpty()) {
                    isValid = false;
                    reason = "Closing delimiter '" + ch + "' has no matching opening delimiter.";
                    break;
                }

                char top = stack.peek();
                if ((ch == ')' && top == '(') ||
                    (ch == ']' && top == '[') ||
                    (ch == '}' && top == '{')) {
                    stack.pop();
                } else {
                    isValid = false;
                    reason = "Mismatched delimiters: expected closing for '" + top + "' but found '" + ch + "'.";
                    break;
                }
            }
            // Ignore non-delimiter characters
        }

        // Final check for unmatched openings
        if (isValid && !stack.isEmpty()) {
            isValid = false;
            reason = "Unmatched opening delimiter(s) remain.";
        }

        // Result
        if (isValid) {
            System.out.println("Valid");
        } else {
            System.out.println("Invalid — " + reason);
        }
    }
}
