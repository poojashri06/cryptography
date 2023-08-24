#include <stdio.h>
#include <string.h>

void receivePacket(const char* packet) {
    printf("Received packet: %s\n", packet);
    
    if (strstr(packet, "PASSWORD") != NULL) {
        printf("Intrusion detected: Password pattern found!\n");
    }
}

int main() {
    
    receivePacket("Some normal data here.");
    receivePacket("Another packet without PASSWORD.");
    receivePacket("This packet contains the PASSWORD.");

    return 0;
}
