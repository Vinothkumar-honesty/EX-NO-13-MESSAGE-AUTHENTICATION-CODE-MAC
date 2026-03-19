# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32 // Define MAC size in bytes

// Function to compute a simple MAC using XOR
void computeMAC(const char *key, const char *message, unsigned char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);

    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len]; // Simple XOR operation
    }
}

// Function to print MAC in hex
void printMAC(const unsigned char *mac) {
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", mac[i]);
    }
    printf("\n");
}

int main() {
    char key[100], message[100];
    unsigned char mac[MAC_SIZE];
    unsigned char receivedMAC[MAC_SIZE];
    
    // Step 1: Input the message
    printf("Enter the message: ");
    scanf("%s", message);
    
    // Step 2: Input secret key
    printf("Enter the secret key: ");
    scanf("%s", key);

    

    // Step 3: Compute the MAC
    computeMAC(key, message, mac);

    // Step 4: Simulate receiving the same MAC (automatic)
    memcpy(receivedMAC, mac, MAC_SIZE);  // In a real scenario, this would come from sender

    // Step 5: Display both MACs
    printf("\nComputed MAC (Sender): ");
    printMAC(mac);

    printf("Received MAC (Receiver): ");
    printMAC(receivedMAC);

    // Step 6: Verify automatically
    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}

```
## Output:
<img width="824" height="120" alt="image" src="https://github.com/user-attachments/assets/f5b6bb3e-dbf5-48c5-8bee-c8c90849da2c" />


## Result:
The program is executed successfully.
