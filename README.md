# examcode
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
___________________________________________________

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

__________________________________________

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



____________________________________________________

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
            int y = (key[1][0]*a + key[1][1]*b) % 26;

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
________________________________________________________________
import java.util.*;

public class CryptoCombined {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        while(true) {
            System.out.println("\n--- MENU ---");
            System.out.println("1. Caesar Cipher");
            System.out.println("2. Substitution Cipher");
            System.out.println("3. Exit");

            System.out.println("______________________");
            System.out.print("Enter your choice: ");

            int choice = sc.nextInt();
            sc.nextLine();

            switch(choice) {

                case 1:
                    // Caesar Cipher
                    System.out.print("Enter text: ");
                    String text = sc.nextLine();

                    System.out.print("Enter shift key: ");
                    int key = sc.nextInt();
                    sc.nextLine();

                    String encrypt = "", decrypt = "";

                    for (int i = 0; i < text.length(); i++) {
                        char ch = text.charAt(i);

                        if (Character.isLetter(ch)) {
                            char base = Character.isUpperCase(ch) ? 'A' : 'a';
                            encrypt += (char)((ch - base + key) % 26 + base);
                        } else {
                            encrypt += ch;
                        }
                    }

                    for (int i = 0; i < encrypt.length(); i++) {
                        char ch = encrypt.charAt(i);

                        if (Character.isLetter(ch)) {
                            char base = Character.isUpperCase(ch) ? 'A' : 'a';
                            decrypt += (char)((ch - base - key + 26) % 26 + base);
                        } else {
                            decrypt += ch;
                        }
                    }

                    System.out.println("Encrypted Text: " + encrypt);
                    System.out.println("Decrypted Text: " + decrypt);
                    break;

                case 2:
                    // Substitution Cipher
                    System.out.print("Enter text: ");
                    String text2 = sc.nextLine().toUpperCase();

                    System.out.print("Enter 26-letter key: ");
                    String subKey = sc.nextLine().toUpperCase();

                    String alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
                    String enc2 = "", dec2 = "";

                    for (char ch : text2.toCharArray()) {
                        if (Character.isLetter(ch)) {
                            enc2 += subKey.charAt(alphabet.indexOf(ch));
                        } else {
                            enc2 += ch;
                        }
                    }

                    for (char ch : enc2.toCharArray()) {
                        if (Character.isLetter(ch)) {
                            dec2 += alphabet.charAt(subKey.indexOf(ch));
                        } else {
                            dec2 += ch;
                        }
                    }

                    System.out.println("Encrypted Text: " + enc2);
                    System.out.println("Decrypted Text: " + dec2);
                    break;

                case 3:
                    System.out.println("Exiting program...");
                    return;

                default:
                    System.out.println("Invalid choice!");
            }
        }
    }
}
_________________________________________________________________
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

__________________________________________________________
import java.util.*;

public class SimpleAESFinal {

    static int[][] state = new int[4][4];

    static int sub(int x) {
        return (x * 5 + 3) % 26;
    }

    static int invsub(int x) {
        for (int i = 0; i < 26; i++)
            if ((i * 5 + 3) % 26 == x)
                return i;
        return 0;
    }

    static void shiftRows() {
        for (int i = 1; i < 4; i++) {
            int[] temp = state[i].clone();
            for (int j = 0; j < 4; j++)
                state[i][j] = temp[(j + i) % 4];
        }
    }

    static void invShiftRows() {
        for (int i = 1; i < 4; i++) {
            int[] temp = state[i].clone();
            for (int j = 0; j < 4; j++)
                state[i][(j + i) % 4] = temp[j];
        }
    }

    static void addKey(int[][] key) {
        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                state[i][j] = (state[i][j] + key[i][j]) % 26;
    }

    static void subKey(int[][] key) {
        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                state[i][j] = (state[i][j] - key[i][j] + 26) % 26;
    }

    static void load(String text) {
        int k = 0;
        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                state[i][j] = text.charAt(k++) - 'A';
    }

    static String getText() {
        String s = "";
        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                s += (char)(state[i][j] + 'A');
        return s;
    }

    static int[][] getKey(String keyText) {
        int[][] key = new int[4][4];
        int k = 0;
        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                key[i][j] = keyText.charAt(k++) - 'A';
        return key;
    }

    static String encrypt(String text, int[][] key) {
        load(text);
        addKey(key);

        for (int r = 0; r < 9; r++) {
            for (int i = 0; i < 4; i++)
                for (int j = 0; j < 4; j++)
                    state[i][j] = sub(state[i][j]);

            shiftRows();
            addKey(key);
        }

        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                state[i][j] = sub(state[i][j]);

        shiftRows();
        addKey(key);

        return getText();
    }

    static String decrypt(String text, int[][] key) {
        load(text);
        subKey(key);

        for (int r = 0; r < 9; r++) {
            invShiftRows();

            for (int i = 0; i < 4; i++)
                for (int j = 0; j < 4; j++)
                    state[i][j] = invsub(state[i][j]);

            subKey(key);
        }

        invShiftRows();

        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 4; j++)
                state[i][j] = invsub(state[i][j]);

        subKey(key);

        return getText();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter 16-letter text: ");
        String text = sc.nextLine().toUpperCase();

        System.out.print("Enter 16-letter key: ");
        String keyText = sc.nextLine().toUpperCase();

        if (text.length() != 16 || keyText.length() != 16) {
            System.out.println("Must be exactly 16 letters!");
            return;
        }

        int[][] key = getKey(keyText);

        String enc = encrypt(text, key);
        System.out.println("Encrypted: " + enc);

        String dec = decrypt(enc, key);
        System.out.println("Decrypted: " + dec);
    }
}
_______________________________________________________________
import java.util.Base64;
import java.util.Scanner;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;

public class BlowfishAPI {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String text = sc.nextLine();

        System.out.print("Enter key: ");
        String key = sc.nextLine();

        SecretKeySpec secretKey = new SecretKeySpec(key.getBytes(), "Blowfish");
        Cipher cipher = Cipher.getInstance("Blowfish");

        cipher.init(Cipher.ENCRYPT_MODE, secretKey);
        byte[] encrypted = cipher.doFinal(text.getBytes());
        String encryptedText = Base64.getEncoder().encodeToString(encrypted);

        System.out.println("Encrypted: " + encryptedText);

        cipher.init(Cipher.DECRYPT_MODE, secretKey);
        byte[] decrypted = cipher.doFinal(Base64.getDecoder().decode(encryptedText));

        System.out.println("Decrypted: " + new String(decrypted));

        sc.close();
    }
}



_____________________________________________________

import java.util.Base64;
import java.util.Scanner;
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;

public class BlowfishAutoKey {

    public static void main(String[] args) throws Exception {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String text = sc.nextLine();

        // Generate Blowfish key
        KeyGenerator keyGen = KeyGenerator.getInstance("Blowfish");
        keyGen.init(128); // key size
        SecretKey key = keyGen.generateKey();

        // Cipher
        Cipher cipher = Cipher.getInstance("Blowfish");

        // Encryption
        cipher.init(Cipher.ENCRYPT_MODE, key);
        byte[] encrypted = cipher.doFinal(text.getBytes());
        String enc = Base64.getEncoder().encodeToString(encrypted);

        System.out.println("Encrypted: " + enc);

        // Decryption
        cipher.init(Cipher.DECRYPT_MODE, key);
        byte[] decrypted = cipher.doFinal(Base64.getDecoder().decode(enc));

        System.out.println("Decrypted: " + new String(decrypted));

        sc.close();
    }
}
________________________________________________________________
import java.util.*;

public class BlowfishStandardSim {

    static int[] P = new int[18];
    static int[][] S = new int[4][256];

    // Initialize P-array and S-box using key
    static void init(int key) {
        for (int i = 0; i < 18; i++)
            P[i] = (i + 1) ^ key;

        for (int i = 0; i < 4; i++)
            for (int j = 0; j < 256; j++)
                S[i][j] = (i * 256 + j) ^ key;
    }

    // F function using S-box
    static int F(int x) {
        int a = (x >>> 24) & 0xFF;
        int b = (x >>> 16) & 0xFF;
        int c = (x >>> 8) & 0xFF;
        int d = x & 0xFF;

        return ((S[0][a] + S[1][b]) ^ S[2][c]) + S[3][d];
    }

    // Encryption (16 rounds)
    static int[] encrypt(int L, int R) {
        for (int i = 0; i < 16; i++) {
            L ^= P[i];
            R ^= F(L);

            int temp = L;
            L = R;
            R = temp;
        }

        int temp = L;
        L = R;
        R = temp;

        R ^= P[16];
        L ^= P[17];

        return new int[]{L, R};
    }

    // Decryption
    static int[] decrypt(int L, int R) {
        for (int i = 17; i > 1; i--) {
            L ^= P[i];
            R ^= F(L);

            int temp = L;
            L = R;
            R = temp;
        }

        int temp = L;
        L = R;
        R = temp;

        R ^= P[1];
        L ^= P[0];

        return new int[]{L, R};
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter text: ");
        String text = sc.nextLine();

        // 🔥 Added line (clean input)
        text = text.toUpperCase().replaceAll(" ", "");

        System.out.print("Enter key (int): ");
        int key = sc.nextInt();

        // Initialize with key
        init(key);

        // Padding if odd length
        if (text.length() % 2 != 0)
            text += "X";

        String decrypted = "";

        System.out.println("Encrypted blocks:");

        for (int i = 0; i < text.length(); i += 2) {

            int L = text.charAt(i);
            int R = text.charAt(i + 1);

            int[] enc = encrypt(L, R);
            System.out.println(Arrays.toString(enc));

            int[] dec = decrypt(enc[0], enc[1]);

            decrypted += (char) dec[0];
            decrypted += (char) dec[1];
        }

        System.out.println("Decrypted Text: " + decrypted);

        sc.close();
    }
}
