#include <stdio.h>
#include <string.h>

int main() {
    char str[100];
    int i;

    // Taking input from user
    printf("Enter a string: ");
    scanf("%s", str);

    // XOR each character with 0
    for(i = 0; str[i] != '\0'; i++) {
        str[i] = str[i] ^ 0;
    }

    // Display result
    printf("Result after XOR with 0: %s\n", str);

    return 0;
}


-----------------------------------


Enter a string: world
Result after XOR with 0: world





#include <stdio.h>

int main() {
    char *str = "World";   // char pointer string

    printf("Original String: %s\n", str);
    printf("After XOR with 0: ");

    for (int i = 0; str[i] != '\0'; i++) {
        char result = str[i] ^ 0;   // XOR with 0
        printf("%c", result);
    }

    return 0;
}
-------------------------------------------------------------
week 2

#include <stdio.h>

int main() {
    char str[100];
    int i;

    printf("Enter a string: ");
    scanf("%s", str);

    printf("\nOriginal String     : %s\n", str);

    printf("After AND with 127 : ");
    for(i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] & 127);
    }

    printf("\nAfter OR with 127  : ");
    for(i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] | 127);
    }

    printf("\nAfter XOR with 127 : ");
    for(i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] ^ 127);
    }

    return 0;
}



#include <stdio.h>

int main() {
    char *str = "World";   // char pointer

    printf("Original String     : %s\n", str);

    printf("After AND with 127 : ");
    for(int i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] & 127);
    }

    printf("\nAfter OR with 127  : ");
    for(int i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] | 127);
    }

    printf("\nAfter XOR with 127 : ");
    for(int i = 0; str[i] != '\0'; i++) {
        printf("%d ", str[i] ^ 127);
    }

    return 0;
}
__________________________________________


Enter a string: world

Original String     : world
After AND with 127 : 119 111 114 108 100 
After OR with 127  : 127 127 127 127 127 
After XOR with 127 : 8 16 13 19 27 
---------------------------------------------
week 3
import java.util.*;

public class CaesarCipher {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String text = sc.nextLine();

        System.out.print("Enter shift key: ");
        int key = sc.nextInt();

        String encrypt = "", decrypt = "";

        // Encryption
        for (int i = 0; i < text.length(); i++) {
            char ch = text.charAt(i);

            if (Character.isLetter(ch)) {
                char base = Character.isUpperCase(ch) ? 'A' : 'a';
                encrypt += (char) ((ch - base + key) % 26 + base);
            } else {
                encrypt += ch;
            }
        }

        // Decryption
        for (int i = 0; i < encrypt.length(); i++) {
            char ch = encrypt.charAt(i);

            if (Character.isLetter(ch)) {
                char base = Character.isUpperCase(ch) ? 'A' : 'a';
                decrypt += (char) ((ch - base - key + 26) % 26 + base);
            } else {
                decrypt += ch;
            }
        }

        System.out.println("Encrypted Text: " + encrypt);
        System.out.println("Decrypted Text: " + decrypt);
    }
}


__________________________________________________________________


Enter text: hello
Enter shift key: 3
Encrypted Text: khoor
Decrypted Text: hello
---------------------------------
import java.util.*;

public class SubstitutionCipher {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter plain text: ");
        String text = sc.nextLine().toUpperCase();

        System.out.print("Enter 26-letter substitution key: ");
        String key = sc.nextLine().toUpperCase();

        String alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String encrypt = "", decrypt = "";

        // Encryption
        for (char ch : text.toCharArray()) {
            if (Character.isLetter(ch)) {
                int index = alphabet.indexOf(ch);
                encrypt += key.charAt(index);
            } else {
                encrypt += ch;
            }
        }

        // Decryption
        for (char ch : encrypt.toCharArray()) {
            if (Character.isLetter(ch)) {
                int index = key.indexOf(ch);
                decrypt += alphabet.charAt(index);
            } else {
                decrypt += ch;
            }
        }

        System.out.println("Encrypted Text: " + encrypt);
        System.out.println("Decrypted Text: " + decrypt);
    }
}

____________________________________________________________


Enter plain text: world
Enter 26-letter substitution key: qwertyuiopasdfghjklzxcvbnm
Encrypted Text: VGKSR
Decrypted Text: WORLD
------------------------------------------------------
import java.util.*;

public class HillCipherEasy {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Input text
        System.out.print("Enter text: ");
        String text = sc.nextLine().replaceAll(" ", "").toUpperCase();

        // Padding if odd length
        if (text.length() % 2 != 0)
            text += "X";

        // Input key matrix
        int[][] key = new int[2][2];
        System.out.println("Enter 4 values of 2x2 key matrix:");
        for (int i = 0; i < 2; i++)
            for (int j = 0; j < 2; j++)
                key[i][j] = sc.nextInt();

        // Find determinant
        int det = key[0][0]*key[1][1] - key[0][1]*key[1][0];
        det = (det % 26 + 26) % 26;

        // Find modular inverse of determinant
        int invDet = -1;
        for (int i = 1; i < 26; i++) {
            if ((det * i) % 26 == 1) {
                invDet = i;
                break;
            }
        }

        if (invDet == -1) {
            System.out.println("Invalid key! No modular inverse.");
            return;
        }

        // Inverse matrix
        int[][] inv = new int[2][2];
        inv[0][0] = key[1][1];
        inv[1][1] = key[0][0];
        inv[0][1] = -key[0][1];
        inv[1][0] = -key[1][0];

        for (int i = 0; i < 2; i++)
            for (int j = 0; j < 2; j++) {
                inv[i][j] = (inv[i][j] * invDet) % 26;
                if (inv[i][j] < 0)
                    inv[i][j] += 26;
            }

        String enc = "", dec = "";

        // Encryption
        for (int i = 0; i < text.length(); i += 2) {
            int a = text.charAt(i) - 'A';
            int b = text.charAt(i+1) - 'A';

            int x = (key[0][0]*a + key[0][1]*b) % 26;
            int y = (key[1][0]*a + key[1][1]*b) % 26;u

            enc += (char)(x + 'A');
            enc += (char)(y + 'A');
        }

        // Decryption
        for (int i = 0; i < enc.length(); i += 2) {
            int a = enc.charAt(i) - 'A';
            int b = enc.charAt(i+1) - 'A';

            int x = (inv[0][0]*a + inv[0][1]*b) % 26;
            int y = (inv[1][0]*a + inv[1][1]*b) % 26;

            dec += (char)(x + 'A');
            dec += (char)(y + 'A');
        }

        // Output
        System.out.println("Encrypted Text: " + enc);
        System.out.println("Decrypted Text: " + dec);
    }
}
-------------------------------------------------------
week 4
import java.util.*;
import java.util.Base64;
import java.io.ByteArrayOutputStream;

public class SimpleDESFinal{
    
    static int F(int r, int k) {
        return (r ^ k) % 256;
    }

    static int[] generateKeys(String keyStr) {
        int baseKey = 0;

        for (int i = 0; i < 8; i++) {
            baseKey += keyStr.charAt(i);
        }

        int[] keys = new int[16];
        for (int i = 0; i < 16; i++) {
            keys[i] = baseKey + i;
        }

        return keys;
    }

    static int[] encrypt(int L, int R, int[] keys) {
        for (int i = 0; i < 16; i++) {
            int temp = R;
            R = L ^ F(R, keys[i]);
            L = temp;
        }
        return new int[]{L, R};
    }

    static int[] decrypt(int L, int R, int[] keys) {
        for (int i = 15; i >= 0; i--) {
            int temp = L;
            L = R ^ F(L, keys[i]);
            R = temp;
        }
        return new int[]{L, R};
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String text = sc.nextLine();

        System.out.print("Enter 8-character key: ");
        String keyStr = sc.nextLine();

        if (keyStr.length() != 8) {
            System.out.println("Key must be exactly 8 characters!");
            return;
        }

        int[] keys = generateKeys(keyStr);

        if (text.length() % 2 != 0)
            text += "X";

        ByteArrayOutputStream encryptedBytes = new ByteArrayOutputStream();
        String decrypted = "";

        for (int i = 0; i < text.length(); i += 2) {

            int L = text.charAt(i);
            int R = text.charAt(i + 1);

            int[] enc = encrypt(L, R, keys);

            encryptedBytes.write(enc[0] & 0xFF);
            encryptedBytes.write(enc[1] & 0xFF);

            int[] dec = decrypt(enc[0], enc[1], keys);

            decrypted += (char) dec[0];
            decrypted += (char) dec[1];
        }

        String encryptedText = Base64.getEncoder()
                .encodeToString(encryptedBytes.toByteArray());

        if (decrypted.endsWith("X"))
            decrypted = decrypted.substring(0, decrypted.length() - 1);

        System.out.println("Encrypted Text: " + encryptedText);
        System.out.println("Decrypted Text: " + decrypted);
    }
}

___________________________________________________________________

Enter text: hellos
Enter 8-character key: qwertyui
Encrypted Text: bppnl3iL
Decrypted Text: hellos
-------------------------------------------------------------------
week 5
import java.util.*;

public class SimpleBlowfish {

    static int[] P = new int[18];
    static int[] S = new int[256];

    // Initialize P-array and S-box using key
    static void init(String key) {

        int k = 0;

        for (char ch : key.toCharArray()) {
            k += ch;
        }

        for (int i = 0; i < 18; i++) {
            P[i] = k ^ (i + 1);
        }

        for (int i = 0; i < 256; i++) {
            S[i] = (k + i) ^ 0x5A;
        }
    }

    // F-function
    static int F(int x) {

        int a = (x >> 8) & 0xFF;
        int b = x & 0xFF;

        return (S[a] + S[b]) ^ 7;
    }

    // Encryption
    static int[] encrypt(int L, int R) {

        for (int i = 0; i < 16; i++) {

            L = L ^ P[i];

            R = R ^ F(L);

            // Swap
            int temp = L;
            L = R;
            R = temp;
        }

        // Undo final swap
        int temp = L;
        L = R;
        R = temp;

        R = R ^ P[16];
        L = L ^ P[17];

        return new int[]{L, R};
    }

    // Decryption
    static int[] decrypt(int L, int R) {

        for (int i = 17; i > 1; i--) {

            L = L ^ P[i];

            R = R ^ F(L);

            // Swap
            int temp = L;
            L = R;
            R = temp;
        }

        // Undo final swap
        int temp = L;
        L = R;
        R = temp;

        R = R ^ P[1];
        L = L ^ P[0];

        return new int[]{L, R};
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter plaintext: ");
        String text = sc.nextLine().toUpperCase().replaceAll(" ", "");;

        

        System.out.print("Enter key: ");
        String key = sc.nextLine();

        // Initialize using key
        init(key);

        // Padding
        if (text.length() % 2 != 0) {
            text += "X";
        }

        String encryptedText = "";
        String decryptedText = "";

        // Process 2 characters at a time
        for (int i = 0; i < text.length(); i += 2) {

            int L = text.charAt(i);
            int R = text.charAt(i + 1);

            // Encrypt
            int[] enc = encrypt(L, R);

            // Store encrypted text
            encryptedText +=
                    Integer.toHexString(enc[0]) + " ";

            encryptedText +=
                    Integer.toHexString(enc[1]) + " ";

            // Decrypt
            int[] dec = decrypt(enc[0], enc[1]);

            decryptedText +=
                    (char)(dec[0] & 0xFF);

            decryptedText +=
                    (char)(dec[1] & 0xFF);
        }

        System.out.println("\nEncrypted Text: "
                + encryptedText);

        System.out.println("Decrypted Text: "
                + decryptedText);

        sc.close();
    }
}
-----------------------------------------------------------
week6
import java.util.*;

public class SimpleAESFinal {

    static int[][] state = new int[4][4];

    // ---------------- SubBytes ----------------
    static int sub(int x) {
        return (x * 5 + 3) % 26;
    }

    // ---------------- Inverse SubBytes ----------------
    static int invSub(int x) {
        return (21 * (x - 3 + 26)) % 26;
    }

    // ---------------- ShiftRows ----------------
    static void shiftRows() {

        for (int i = 1; i < 4; i++) {

            int[] temp = state[i].clone();

            for (int j = 0; j < 4; j++) {

                state[i][j] = temp[(j + i) % 4];
            }
        }
    }

    // ---------------- Inverse ShiftRows ----------------
    static void invShiftRows() {

        for (int i = 1; i < 4; i++) {

            int[] temp = state[i].clone();

            for (int j = 0; j < 4; j++) {

                state[i][(j + i) % 4] = temp[j];
            }
        }
    }

    // ---------------- AddRoundKey ----------------
    static void addKey(int[][] key) {

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                state[i][j] =
                        (state[i][j] + key[i][j]) % 26;
            }
        }
    }

    // ---------------- Reverse AddRoundKey ----------------
    static void subKey(int[][] key) {

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                state[i][j] =
                        (state[i][j] - key[i][j] + 26) % 26;
            }
        }
    }

    // ---------------- Load Plaintext ----------------
    static void load(String text) {

        int k = 0;

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                state[i][j] =
                        text.charAt(k++) - 'A';
            }
        }
    }

    // ---------------- Convert Matrix to Text ----------------
    static String getText() {

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                sb.append((char)
                        (state[i][j] + 'A'));
            }
        }

        return sb.toString();
    }

    // ---------------- Generate Key Matrix ----------------
    static int[][] getKey(String keyText) {

        int[][] key = new int[4][4];

        int k = 0;

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                key[i][j] =
                        keyText.charAt(k++) - 'A';
            }
        }

        return key;
    }

    // ---------------- Encryption ----------------
    static String encrypt(String text, int[][] key) {

        load(text);

        // Initial AddRoundKey
        addKey(key);

        // 9 Main Rounds
        for (int r = 0; r < 9; r++) {

            // SubBytes
            for (int i = 0; i < 4; i++) {

                for (int j = 0; j < 4; j++) {

                    state[i][j] =
                            sub(state[i][j]);
                }
            }

            // ShiftRows
            shiftRows();

            // AddRoundKey
            addKey(key);
        }

        // Final Round
        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                state[i][j] =
                        sub(state[i][j]);
            }
        }

        shiftRows();

        addKey(key);

        return getText();
    }

    // ---------------- Decryption ----------------
    static String decrypt(String text, int[][] key) {

        load(text);

        // Reverse Final Round
        subKey(key);

        invShiftRows();

        for (int i = 0; i < 4; i++) {

            for (int j = 0; j < 4; j++) {

                state[i][j] =
                        invSub(state[i][j]);
            }
        }

        // Reverse 9 Main Rounds
        for (int r = 0; r < 9; r++) {

            subKey(key);

            invShiftRows();

            for (int i = 0; i < 4; i++) {

                for (int j = 0; j < 4; j++) {

                    state[i][j] =
                            invSub(state[i][j]);
                }
            }
        }

        // Reverse Initial AddRoundKey
        subKey(key);

        return getText();
    }

    // ---------------- Main Function ----------------
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter 16-letter plaintext : ");
        String text =
                sc.nextLine().toUpperCase();

        System.out.print("Enter 16-letter key       : ");
        String keyText =
                sc.nextLine().toUpperCase();

        // Validation
        if (text.length() != 16 ||
                keyText.length() != 16) {

            System.out.println(
                    "Input and key must be exactly 16 letters.");

            return;
        }

      

        int[][] key = getKey(keyText);

        // Encryption
        String encrypted =
                encrypt(text, key);

        System.out.println(
                "\nEncrypted Text : " + encrypted);

        // Decryption
        String decrypted =
                decrypt(encrypted, key);

        System.out.println(
                "Decrypted Text : " + decrypted);

        sc.close();
    }
}
--------------------------------------------------
week7

"C:\Program Files\Java\jdk-21\bin\keytool.exe" -genseckey -alias myblowfishkey -keyalg Blowfish -keysize 128 -storetype JCEKS -keystore mykeystore.jks -storepass password -keypass password

import javax.crypto.Cipher;
import javax.crypto.SecretKey;
import java.security.KeyStore;
import java.io.FileInputStream;
import java.util.Base64;
import java.util.Scanner;

public class blow {

    public static void main(String[] args) throws Exception {

        // Scanner for user input
        Scanner sc = new Scanner(System.in);

        // Take text input from user
        System.out.print("Enter text to encrypt: ");
        String text = sc.nextLine();

        // Load keystore
        KeyStore ks = KeyStore.getInstance("JCEKS");

        FileInputStream fis =
                new FileInputStream("mykeystore.jks");

        ks.load(fis, "password".toCharArray());

        // Get secret key
        SecretKey key = (SecretKey)
                ks.getKey(
                        "myblowfishkey",
                        "password".toCharArray()
                );

        // Check key
        if (key == null) {

            System.out.println(
                    "Key not found. Check alias/password."
            );

            return;
        }

        // Create Blowfish Cipher
        Cipher cipher =
                Cipher.getInstance(
                        "Blowfish/ECB/PKCS5Padding"
                );

        // Encryption
        cipher.init(Cipher.ENCRYPT_MODE, key);

        byte[] encryptedBytes =
                cipher.doFinal(text.getBytes());

        String encrypted =
                Base64.getEncoder()
                        .encodeToString(encryptedBytes);

        // Decryption
        cipher.init(Cipher.DECRYPT_MODE, key);

        byte[] decryptedBytes =
                cipher.doFinal(
                        Base64.getDecoder()
                                .decode(encrypted)
                );

        String decrypted =
                new String(decryptedBytes);

        // Output
        System.out.println("\nOriginal Text : " + text);

        System.out.println(
                "Encrypted Text: " + encrypted
        );

        System.out.println(
                "Decrypted Text: " + decrypted
        );

        sc.close();
    }
}


week 8

import java.util.*;

public class RSA {

    // Find GCD
    static int gcd(int a, int b) {

        while (b != 0) {

            int temp = b;
            b = a % b;
            a = temp;
        }

        return a;
    }

    // Find modular inverse
    static int modInverse(int e, int phi) {

        for (int d = 1; d < phi; d++) {

            if ((d * e) % phi == 1) {
                return d;
            }
        }

        return 1;
    }

    // Power function
    static long power(long base, long exp, long mod) {

        long result = 1;

        while (exp > 0) {

            result = (result * base) % mod;
            exp--;
        }

        return result;
    }

    // Prime check
    static boolean isPrime(int n) {

        if (n < 2)
            return false;

        for (int i = 2; i <= n / 2; i++) {

            if (n % i == 0)
                return false;
        }

        return true;
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // Input prime numbers
        System.out.print("Enter prime number p: ");
        int p = sc.nextInt();

        System.out.print("Enter prime number q: ");
        int q = sc.nextInt();

        // Validate primes
        if (!isPrime(p) || !isPrime(q)) {

            System.out.println(
                    "Please enter prime numbers only.");

            return;
        }

        // Compute n
        int n = p * q;

        // Compute phi
        int phi = (p - 1) * (q - 1);

        // Choose e
        int e;

        for (e = 2; e < phi; e++) {

            if (gcd(e, phi) == 1) {
                break;
            }
        }

        // Compute d
        int d = modInverse(e, phi);

        // Display keys
        System.out.println(
                "\nPublic Key (e,n): (" + e + "," + n + ")");

        System.out.println(
                "Private Key (d,n): (" + d + "," + n + ")");

        // Input message
        System.out.print(
                "\nEnter message number: ");

        int message = sc.nextInt();

        // Message validation
        if (message >= n) {

            System.out.println(
                    "Message must be less than " + n);

            return;
        }

        // Encryption
        long encrypted = power(message, e, n);

        System.out.println(
                "Encrypted Message: " + encrypted);

        // Decryption
        long decrypted = power(encrypted, d, n);

        System.out.println(
                "Decrypted Message: " + decrypted);

        sc.close();
    }
}


week 9

<!DOCTYPE html>
<html>
<head>
    <title>Diffie-Hellman Key Exchange</title>

    <style>
        body{
            font-family: Arial;
            margin: 40px;
        }

        input{
            margin: 5px;
            padding: 5px;
            width: 200px;
        }

        button{
            padding: 8px 15px;
            margin-top: 10px;
        }

        #result{
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>

<body>

<h2>Diffie-Hellman Key Exchange</h2>

<label>Prime Number (P):</label><br>
<input type="number" id="p"><br>

<label>Primitive Root (G):</label><br>
<input type="number" id="g"><br>

<label>Alice Private Key:</label><br>
<input type="number" id="a"><br>

<label>Bob Private Key:</label><br>
<input type="number" id="b"><br>

<button onclick="exchange()">Generate Shared Key</button>

<div id="result"></div>

<script>

    // Fast Modular Exponentiation
    function power(base, exp, mod){

        let result = 1;

        while(exp > 0){

            if(exp % 2 === 1)
                result = (result * base) % mod;

            base = (base * base) % mod;

            exp = Math.floor(exp / 2);
        }

        return result;
    }

    function exchange(){

        let p = parseInt(document.getElementById("p").value);
        let g = parseInt(document.getElementById("g").value);
        let a = parseInt(document.getElementById("a").value);
        let b = parseInt(document.getElementById("b").value);

        // Public Keys
        let A = power(g, a, p);
        let B = power(g, b, p);

        // Shared Secret Keys
        let aliceKey = power(B, a, p);
        let bobKey = power(A, b, p);

        document.getElementById("result").innerHTML =

            "Alice Public Key: " + A + "<br><br>" +

            "Bob Public Key: " + B + "<br><br>" +

            "Alice Shared Key: " + aliceKey + "<br><br>" +

            "Bob Shared Key: " + bobKey;
    }

</script>

</body>
</html>


week 10


import java.util.*;

public class SHA1 {

    // Left Rotate Function
    static int rot(int x, int n) {
        return (x << n) | (x >>> (32 - n));
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String msg = sc.nextLine();

        // Initial SHA-1 Values
        int h0 = 0x67452301;
        int h1 = 0xEFCDAB89;
        int h2 = 0x98BADCFE;
        int h3 = 0x10325476;
        int h4 = 0xC3D2E1F0;

        int[] w = new int[80];

        // Convert message to binary
        String bin = "";

        for (int i = 0; i < msg.length(); i++) {

            String b =
                    Integer.toBinaryString(msg.charAt(i));

            while (b.length() < 8)
                b = "0" + b;

            bin += b;
        }

        // Original length
        int ml = bin.length();

        // Append 1 bit
        bin += "1";

        // Padding with 0s
        while ((bin.length() + 64) % 512 != 0)
            bin += "0";

        // Append message length
        String len = Integer.toBinaryString(ml);

        while (len.length() < 64)
            len = "0" + len;

        bin += len;

        // First 16 words
        for (int i = 0; i < 16; i++) {

            String temp =
                    bin.substring(i * 32, (i + 1) * 32);

            w[i] = (int)
                    Long.parseLong(temp, 2);
        }

        // Remaining 64 words
        for (int i = 16; i < 80; i++) {

            w[i] = rot(
                    w[i - 3] ^
                    w[i - 8] ^
                    w[i - 14] ^
                    w[i - 16], 1);
        }

        int a = h0;
        int b = h1;
        int c = h2;
        int d = h3;
        int e = h4;

        // 80 Rounds
        for (int i = 0; i < 80; i++) {

            int f = 0;
            int k = 0;

            if (i < 20) {

                f = (b & c) | ((~b) & d);
                k = 0x5A827999;
            }

            else if (i < 40) {

                f = b ^ c ^ d;
                k = 0x6ED9EBA1;
            }

            else if (i < 60) {

                f = (b & c) | (b & d) | (c & d);
                k = 0x8F1BBCDC;
            }

            else {

                f = b ^ c ^ d;
                k = 0xCA62C1D6;
            }

            int temp =
                    rot(a, 5) + f + e + k + w[i];

            e = d;
            d = c;
            c = rot(b, 30);
            b = a;
            a = temp;
        }

        // Final Hash Values
        h0 += a;
        h1 += b;
        h2 += c;
        h3 += d;
        h4 += e;

        // Print SHA-1 Digest
        System.out.println("\nSHA-1 Digest:");

        System.out.printf(
                "%08x%08x%08x%08x%08x",
                h0, h1, h2, h3, h4);

        sc.close();
    }
}
