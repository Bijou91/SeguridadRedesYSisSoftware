# vault-door-3

# Descripción 
This vault uses ASCII encoding for the password.
The source code for this vault is here: [VaultDoor4.java](https://challenge-files.picoctf.net/c_fickle_tempest/f587295139ec9c3d23e1299b831596c3243b0e042bec63dd21168e996c0f7c8c/VaultDoor4.java)
## Solución
Lo que debemos hacer para resolver este reto es ver el contenido del archivo de código Java que nos proporcionan
```java
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18gb4c_u_4_m2r640");
    }
}
```

Como vemos, la flag ha sido desordenada en esta ocasión, pero afortunadamente, el mismo código nos dice como podemos ordenarla.

Para ordenarla, usaremos este código:
```java
public class solveV3 {
        public static void main(String[] args) {
                String s = "jU5t_a_sna_3lpm18gb4c_u_4_m2r640";

        char[] buffer = new char[32];
        int i;
        for (i=31; i>=17; i-=2) {
            buffer[i] = s.charAt(i);
        }
        for (i=16; i<32; i+=2) {
            buffer[i] = s.charAt(46-i);
        }
        for (i=8; i<16; i++) {
            buffer[i] = s.charAt(23-i);
        }
        for (i=0; i<8; i++) {
            buffer[i] = s.charAt(i);
        }
        String password = new String(buffer);

        System.out.println(password);
        }
}
```

Esto nos imprime la flag ordenada, la que le agregamos el formato de la flag (picoctf{})
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c2b680}
## Notas
- 