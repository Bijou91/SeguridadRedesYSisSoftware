## rust fixme1
# Descripción
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz).
# Solución
Este reto se basa en corregir un código en rust para obtener nuestra bandera.

El código a corregir es este:
```
use xor_cryptor::XORCryptor;  
  
fn main() {  
	// Key for decryption  
	let key = String::from("CSUCKS") // How do we end statements in Rust?  
	  
	// Encrypted flag values  
	let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];  
	  
	// Convert the hexadecimal strings to bytes and collect them into a vector  
	let encrypted_buffer: Vec<u8> = hex_values.iter()  
		.map(|&hex| u8::from_str_radix(hex, 16).unwrap())  
		.collect();  
	  
	// Create decrpytion object  
	let res = XORCryptor::new(&key);  
	if res.is_err() {  
		ret; // How do we return in rust?  
	}  
	let xrc = res.unwrap();  
	  
	// Decrypt flag and print it out  
	let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);  
	println!(  
		":?", // How do we print out a variable in the println function?  
		String::from_utf8_lossy(&decrypted_buffer)  
	);  
}
```

Y debemos realizar estas tres correciones:
- `let key = String::from("CSUCKS") // How do we end statements in Rust?` aquí debemos agregar un `;` al final para terminar la instrucción
- `ret; // How do we return in rust?` aquí debemos corregir el ret a return.
- Y en `println!(":?", // How do we print out a variable in the println function?` debemos cambiar el `:?` por un par de `{}`

Este es el código corregido:
```
use xor_cryptor::XORCryptor;  
  
fn main() {  
	// Key for decryption  
	let key = String::from("CSUCKS"); //Correción #1  
	  
	// Encrypted flag values  
	let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];  
	  
	// Convert the hexadecimal strings to bytes and collect them into a vector  
	let encrypted_buffer: Vec<u8> = hex_values.iter()  
		.map(|&hex| u8::from_str_radix(hex, 16).unwrap())  
		.collect();  
	  
	// Create decrpytion object  
	let res = XORCryptor::new(&key);  
	if res.is_err() {  
		return; //Corrección #2  
	}  
	let xrc = res.unwrap();  
	  
	// Decrypt flag and print it out  
	let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);  
	println!(  
		"{}", //Corrección #3  
		String::from_utf8_lossy(&decrypted_buffer)  
	);  
}
```

Debido a problemas con el uso de recursos de mi computadora, he tenido que pedirle a Claude ejecutar el código y desencriptar la bandera.

picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}
# Notas adicionales
- 
# Referencias
- 