# Practica-3.1-Rafael-Moncayo-Palate

## Codi de la pràctica

```cpp 
#include <Arduino.h>
#include <WiFi.h>
#include <WebServer.h>
// SSID & Password
void handle_root();

extern String HTML;
const char* ssid = "MOVISTAR_B841"; // Enter your SSID here
const char* password = "C762A9CC017D67F5980"; //Enter your Password here
WebServer server(80);

// Object of WebServer(HTTP port, 80 is defult)
void setup() {

  Serial.begin(115200);
  Serial.println("Try Connecting to ");
  Serial.println(ssid);
  // Connect to your wi-fi modem
  WiFi.begin(ssid, password);
  // Check wi-fi is connected to wi-fi network
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected successfully");
  Serial.print("Got IP: ");
  Serial.println(WiFi.localIP()); //Show ESP32 IP on serial
  server.on("/", handle_root);
  server.begin();
  Serial.println("HTTP server started");
  delay(100);

}

void loop() {

server.handleClient();

}
// Handle root url (/)
void handle_root() {

  server.send(200, "text/html", HTML);

}
```
![alt text](https://github.com/RafaelEMonPal/Practica-3.1-Rafael-Moncayo-Palate/blob/main/Server%20succes.png)

______________________________________________________
```cpp
#include <Arduino.h>
#include <WiFi.h>
#include <WebServer.h>

// HTML & CSS contents which display on web server
String HTML = 
"<!DOCTYPE html> \
<html>\
<body>\
<h1> My Primera Pagina con ESP32 - Station Mode &#128221;</h1>\
<h5>Hello World<h1>\
</body>\
</html> ";
```
![alt text](https://github.com/RafaelEMonPal/Practica-3.1-Rafael-Moncayo-Palate/blob/main/Pag%20web.png)

## Explicació de la pràctica

En el principi del codi de la pràctica afegim la llibreria que ens proporciona la ESP per poder utilitzar el wifi. Comences amb a conexió wifi amb la teva xarxa amb un WiFi.begin(ssid,contrasenya). Després, amb el handleroot, assignes la ip local a una pagina web externa declarada com un String HTML on tindrem el diseny de la pagina web i amb el handleclient() comences la conexió amb el servidor. 
HTML no es el meu fort aixi que en la pagina web he canviat la emoticona i he escrit "Hello World" com a referencia a tots els tutorials de programació per a principiants.
