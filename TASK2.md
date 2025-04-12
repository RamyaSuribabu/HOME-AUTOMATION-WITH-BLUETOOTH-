#define LED_PIN 9  // LED connected to pin 9

void setup() {
    pinMode(LED_PIN, OUTPUT);  // Set LED pin as output
    Serial.begin(9600);        // Start Serial communication
    Serial.println("System Initialized. Type '1' to turn LED ON, '0' to turn LED OFF, and '2' to blink the LED.");
}

void loop() {
    if (Serial.available()) {      // Check if data is available in the Serial Monitor
        char command = Serial.read();  // Read the received command
        Serial.print("Command Received: ");
        Serial.println(command);

        // Handle LED Control
        if (command == '1') {
            digitalWrite(LED_PIN, HIGH);  // Turn LED ON
            Serial.println("LED ON");
        } 
        else if (command == '0') {
            digitalWrite(LED_PIN, LOW);   // Turn LED OFF
            Serial.println("LED OFF");
        } 
        else if (command == '2') {
            // Blink the LED
            Serial.println("Blinking LED...");
            for (int i = 0; i < 5; i++) {  // Blink 5 times
                digitalWrite(LED_PIN, HIGH);  // LED ON
                Serial.print("Blinking ON - Cycle ");
                Serial.println(i + 1);
                delay(500);                  // Wait for 500ms
                digitalWrite(LED_PIN, LOW);   // LED OFF
                Serial.print("Blinking OFF - Cycle ");
                Serial.println(i + 1);
                delay(500);                  // Wait for 500ms
            }
            Serial.println("Blinking Complete");
        } 
        else {
            Serial.println("Invalid Command");  // Handle unrecognized input
        }
    }
}
