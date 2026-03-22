## Flag_Shop
# Descripción
There's a flag shop selling stuff, can you buy a flag?
[Source](https://challenge-files.picoctf.net/c_fickle_tempest/00517bd6f4d62bae3c15297f6bf9305fc49253f0638e1c52580a02a1c8cbd8a7/store.c). Connect with nc fickle-tempest.picoctf.net 54108.
# Solución
Este reto se basa en seguir un 'minijuego' de una tienda de flags, al conectarnos al servidor, nos muestra esto
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/examen1/gs/flagshop]
└─$ nc fickle-tempest.picoctf.net 54108
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit
```

Para saber como pasar este reto, nos han entregado el código fuente
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    setbuf(stdout, NULL);
    int con;
    con = 0;
    int account_balance = 1100;
    while(con == 0){
        
        printf("Welcome to the flag exchange\n");
        printf("We sell flags\n");

        printf("\n1. Check Account Balance\n");
        printf("\n2. Buy Flags\n");
        printf("\n3. Exit\n");
        int menu;
        printf("\n Enter a menu selection\n");
        fflush(stdin);
        scanf("%d", &menu);
        if(menu == 1){
            printf("\n\n\n Balance: %d \n\n\n", account_balance);
        }
        else if(menu == 2){
            printf("Currently for sale\n");
            printf("1. Defintely not the flag Flag\n");
            printf("2. 1337 Flag\n");
            int auction_choice;
            fflush(stdin);
            scanf("%d", &auction_choice);
            if(auction_choice == 1){
                printf("These knockoff Flags cost 900 each, enter desired quantity\n");
                
                int number_flags = 0;
                fflush(stdin);
                scanf("%d", &number_flags);
                if(number_flags > 0){
                    int total_cost = 0;
                    total_cost = 900*number_flags;
                    printf("\nThe final cost is: %d\n", total_cost);
                    if(total_cost <= account_balance){
                        account_balance = account_balance - total_cost;
                        printf("\nYour current balance after transaction: %d\n\n", account_balance);
                    }
                    else{
                        printf("Not enough funds to complete purchase\n");
                    }
                                    
                    
                }
                    
                    
                    
                
            }
            else if(auction_choice == 2){
                printf("1337 flags cost 100000 dollars, and we only have 1 in stock\n");
                printf("Enter 1 to buy one");
                int bid = 0;
                fflush(stdin);
                scanf("%d", &bid);
                
                if(bid == 1){
                    
                    if(account_balance > 100000){
                        FILE *f = fopen("flag.txt", "r");
                        if(f == NULL){

                            printf("flag not found: please run this on the server\n");
                            exit(0);
                        }
                        char buf[64];
                        fgets(buf, 63, f);
                        printf("YOUR FLAG IS: %s\n", buf);
                        }
                    
                    else{
                        printf("\nNot enough funds for transaction\n\n\n");
                    }}

            }
        }
        else{
            con = 1;
        }

    }
    return 0;
}
```

Como podemos notar, nuestro saldo se asigna automáticamente a 1100 en la línea 8, y a su vez, el saldo se actualiza tras una transacción en la línea 42. Para obtener nuestra bandera que cuesta más del saldo inicial que nos dan, deberemos sobrecargar la variable de nuestro saldo.

Esto lo haremos al volverlo negativo comprando muchas unidades
```
 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
234872398478521

The final cost is: -1963427228

Your current balance after transaction: 1963428328
```

Ahora simplemente, compramos la bandera real
```
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1
YOUR FLAG IS: picoCTF{m0n3y_bag5_44cFf530}
```
picoCTF{m0n3y_bag5_44cFf530}
# Notas adicionales
- 
# Referencias
- 