# PUSH-BUTTON-COUNTER
 import java.util.Scanner;

public class PushButtonCounter {
    static final int debounceDelay = 50; // milliseconds
    static int buttonState = 0;
    static int lastButtonState = 0;
    static int count = 0;
    static long lastDebounceTime = 0;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Simulated Push Button Counter. Type 'press' to simulate a button press. Type 'exit' to quit.");

        while (true) {
            String input = scanner.nextLine();

            if (input.equalsIgnoreCase("exit")) break;

            // Simulate digitalRead
            int reading = input.equalsIgnoreCase("press") ? 1 : 0;

            long currentTime = System.currentTimeMillis();

            if (reading != lastButtonState) {
                lastDebounceTime = currentTime;
            }

            if ((currentTime - lastDebounceTime) > debounceDelay) {
                if (reading != buttonState) {
                    buttonState = reading;

                    if (buttonState == 1) {
                        count++;
                        System.out.println("Button Pressed Count: " + count);
                    }
                }
            }

            lastButtonState = reading;
        }

        scanner.close();
    }
}
