# MY-FIRST-WEBSITE
FIRST WEBSITE
 dustdensity = 0.5;
 String dataString = "";
 dataString += dtostrf(voltage, 9, 4, s);
 dataString += ",";
 dataString += dtostrf(dustdensity, 5, 2, s);
 dataString += ",";
 dataString += dtostrf(ppmpercf, 8, 0, s);
 i=0;
 ppm=0;
 Serial.println(dataString);
 sendData(dataString);
 Serial.println(dataString);
 delay(1000);
 }
 // store the state of the connection for next time through
 // the loop:
 lastConnected = client.connected();
 }

// this method makes a HTTP connection to the server:
 void sendData(String thisData) {
 // if there's a successful connection:
 if (client.connect("www.pachube.com", 80)) {
 Serial.println("connecting...");
 // send the HTTP PUT request.
 // fill in your feed address here:
 client.print("PUT /api/YOUR_FEED_HERE.csv HTTP/1.1\n");
 client.print("Host: www.pachube.com\n");
 // fill in your Pachube API key here:
 client.print("X-PachubeApiKey: YOUR_KEY_HERE\n");
 client.print("Content-Length: ");
 client.println(thisData.length(), DEC);
// last pieces of the HTTP PUT request:
client.print("Content-Type: text/csv\n");
client.println("Connection: close\n");

// here's the actual content of the PUT request:
client.println(thisData);

// note the time that the connection was made:
lastConnectionTime = millis();


}
 else {
 // if you couldn't make a connection:
 Serial.println("connection failed");
 }
 }
