# radar-system-project
# 📡 Radar System Project with ESP32 and ESP8266

Welcome to the Radar System Project! This project uses an ESP32 and an ESP8266 to create a radar system that can detect objects and display the radar data on a web interface. 🎯

## 🚀 Project Overview

This project consists of the following components:
- **ESP32**: Hosts the web server and controls the servo motor.
- **ESP8266**: Controls the servo motor and connects to the Wi-Fi network.
- **Servo Motor**: Rotates to scan the area.
- **Ultrasonic Sensor**: Detects objects in the scanning area.
- **Web Interface**: Displays the radar data.

## 🛠️ Components

- ESP32
- ESP8266
- Servo Motor
- Ultrasonic Sensor
- Breadboard
- Jumper Wires
- 240 Ohm Resistor
- 
ESP32 code
#include <WiFi.h>
#include <ESPAsyncWebServer.h>
#include <Servo.h>

// Network credentials
const char* ssid = "your_SSID";
const char* password = "your_PASSWORD";

// Create AsyncWebServer object on port 80
AsyncWebServer server(80);

// Define Servo motor
Servo myservo;
const int servoPin = 13;

// Define Ultrasonic Sensor pins
const int trigPin = 5;
const int echoPin = 18;

// Variables for calculating distance
long duration;
int distance;

// Variable to store HTML content
String html = "";

// Function to measure distance
int measureDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  return duration * 0.034 / 2;
}

// Function to generate HTML content
String generateHTML(int angle, int distance) {
  String html = "<html><head><title>Radar</title></head><body>";
  html += "<h1>Radar Data</h1>";
  html += "<p>Angle: " + String(angle) + " degrees</p>";
  html += "<p>Distance: " + String(distance) + " cm</p>";
  html += "<button onclick=\"location.href='/set?angle=15'\">Set Angle to 15</button>";
  html += "<button onclick=\"location.href='/set?angle=125'\">Set Angle to 125</button>";
  html += "</body></html>";
  return html;
}

void setup() {
  // Initialize Serial Monitor
  Serial.begin(115200);

  // Initialize Servo motor
  myservo.attach(servoPin);

  // Initialize Ultrasonic Sensor
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");

  // Serve HTML page
  server.on("/", HTTP_GET, [](AsyncWebServerRequest *request){
    int angle = myservo.read();
    int distance = measureDistance();
    String html = generateHTML(angle, distance);
    request->send(200, "text/html", html);
  });

  // Handle setting angle
  server.on("/set", HTTP_GET, [](AsyncWebServerRequest *request){
    if (request->hasParam("angle")) {
      String angleStr = request->getParam("angle")->value();
      int angle = angleStr.toInt();
      myservo.write(angle);
    }
    request->redirect("/");
  });

  // Start server
  server.begin();
}

void loop() {
  // Measure distance
  distance = measureDistance();
  delay(1000);
}

ESP8266
The ESP8266 is responsible for:

Connecting to the Wi-Fi network.
Controlling the servo motor.

Copy code
// ESP8266 main.ino
#include <ESP8266WiFi.h>
#include <Servo.h>
#include <ESP8266WiFi.h>
#include <Servo.h>

// Network credentials
const char* ssid = "your_SSID";
const char* password = "your_PASSWORD";

// Define Servo motor
Servo myservo;
const int servoPin = D4;

// Variables for storing data
WiFiServer server(80);
String header;

void setup() {
  // Initialize Serial Monitor
  Serial.begin(115200);

  // Initialize Servo motor
  myservo.attach(servoPin);

  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");
  Serial.println(WiFi.localIP());

  // Start server
  server.begin();
}

void loop() {
  WiFiClient client = server.available();
  if (client) {
    String currentLine = "";
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        header += c;
        if (c == '\n') {
          if (currentLine.length() == 0) {
            if (header.indexOf("GET /15") >= 0) {
              myservo.write(15);
            } else if (header.indexOf("GET /125") >= 0) {
              myservo.write(125);
            }
            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println();
            client.println("<html><body><h1>Servo Control</h1>");
            client.println("<p><a href=\"/15\">Set to 15 degrees</a></p>");
            client.println("<p><a href=\"/125\">Set to 125 degrees</a></p>");
            client.println("</body></html>");
            break;
          } else {
            currentLine = "";
          }
        } else if (c != '\r') {
          currentLine += c;
        }
      }
    }
    header = "";
    client.stop();
  }
}


📷 Schematic

🌐 Web Interface
The web interface allows you to view the radar data and control the servo motor. Here's an example of what it looks like:


📦 Getting Started
Clone the repository:

Copy code
git clone https://github.com/Probityrajdeep/radar-system-project
Open the code in your preferred IDE (e.g., Arduino IDE).

Upload the code to the ESP32 and ESP8266.

Connect the components as per the schematic.

Access the web interface via the IP address provided by the ESP32.

🔧 Troubleshooting
If you encounter any issues, check the following:

Ensure all connections are secure.
Verify the Wi-Fi credentials.
Check the serial monitor for any error messages.
🎉 Conclusion
Enjoy building and using your radar system! If you have any questions or suggestions, feel free to open an issue or submit a pull request.

Made with ❤️ by Rajdeep

Copy code

### Steps to Create and Upload to GitHub

1. Create a new repository on GitHub with a name like `radar-system-project`.

2. Clone the repository to your local machine:
    ```sh
    https://github.com/Probityrajdeep/radar-system-project
        ```

3. Navigate to the repository directory:
    ```sh
    cd radar-system-project
    ```

4. Create the project structure:
    ```sh
    mkdir -p code/ESP32 code/ESP8266 images
    ```

5. Add your code files (`main.ino` for both ESP32 and ESP8266) to the respective directories.

6. Add any images (schematic, radar example) to the `images` directory.

7. Create the `README.md` file with the content provided above.

8. Add all files to the repository and commit the changes:
    ```sh
    git add .
    git commit -m "Initial commit"
    ```

9. Push the changes to GitHub:
    ```sh
    git push origin main
    ```

This will create a well-organized GitHub repository with an attractive README file for your radar system proje
