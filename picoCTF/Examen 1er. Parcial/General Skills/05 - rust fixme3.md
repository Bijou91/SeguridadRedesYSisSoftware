## rust fixme3
# Descripción
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/dcdaf491b35c1d0f5075e9583edbbb7aaea1dffb6ad32bc000e4d87b5200ff7b/fixme3.tar.gz).
# Solución
Este reto se basa en corregir un código en rust para obtener nuestra bandera.

El código a corregir es este:
```rust
use xor_cryptor::XORCryptor;  
  
fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {  
	// Key for decryption  
	let key = String::from("CSUCKS");  
	  
	// Editing our borrowed value  
	borrowed_string.push_str("PARTY FOUL! Here is your flag: ");  
	  
	// Create decryption object  
	let res = XORCryptor::new(&key);  
	if res.is_err() {  
		return;  
	}  
	let xrc = res.unwrap();  
  
	// Did you know you have to do "unsafe operations in Rust?  
	// https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html  
	// Even though we have these memory safe languages, sometimes we need to do things outside of the rules  
	// This is where unsafe rust comes in, something that is important to know about in order to keep things in perspective  
	  
	unsafe {  
		// Decrypt the flag operations  
		let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);  
		  
		// Creating a pointer  
		let decrypted_ptr = decrypted_buffer.as_ptr();  
		let decrypted_len = decrypted_buffer.len();  
		  
		// Unsafe operation: calling an unsafe function that dereferences a raw pointer  
		let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);  
		  
		borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));  
	}  
	println!("{}", borrowed_string);  
}  
  
fn main() {  
	// Encrypted flag values  
	let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56", "41", "29", "30", "6f", "08", "c3", "61", "f9", "35"];  
	  
	// Convert the hexadecimal strings to bytes and collect them into a vector  
	let encrypted_buffer: Vec<u8> = hex_values.iter()  
		.map(|&hex| u8::from_str_radix(hex, 16).unwrap())  
		.collect();  
	  
	let mut party_foul = String::from("Using memory unsafe languages is a: ");  
	decrypt(encrypted_buffer, &mut party_foul);  
}
```

Y debemos realizar estas tres correciones:
- `let key = String::from("CSUCKS") // How do we end statements in Rust?` aquí debemos agregar un `;` al final para terminar la instrucción
- `ret; // How do we return in rust?` aquí debemos corregir el ret a return.
- Y en `println!(":?", // How do we print out a variable in the println function?` debemos cambiar el `:?` por un par de `{}`
- Agregamos varios `&mut` para que reconozcan los strings

El código terminaría así:
```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    let key = String::from("CSUCKS");
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    // No se necesita unsafe: decrypt_vec retorna un Vec<u8> normal
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    borrowed_string.push_str(&String::from_utf8_lossy(&decrypted_buffer));

    println!("{}", borrowed_string);
}

fn main() {
    let hex_values = [
        "41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53",
        "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56",
        "41", "29", "30", "6f", "08", "c3", "61", "f9", "35",
    ];

    let encrypted_buffer: Vec<u8> = hex_values
        .iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    decrypt(encrypted_buffer, &mut party_foul);
}
```

Debido a problemas con el uso de recursos de mi computadora, he tenido que pedirle a Claude ejecutar el código:
```
Using memory unsafe languages is a: PARTY FOUL! Here is your flag: picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
```

picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
# Notas adicionales
- 
# Referencias
- 