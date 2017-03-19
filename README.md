# IPK
## Client - ftrest 
 aplikace pro přenos souborů, která komunikuje pomocí HTTP a využívá jednoduché RESTful API

### SYNOPSIS
`ftrest COMMAND REMOTE-PATH [LOCAL-PATH]`

### DESCRIPTION
Aplikace klienta začíná komunikaci se serverem, který již musí být spuštěný. V HTTP hlavičce posílá žádost, který příkaz má server vykonat. U příkazu `PUT`, aplikace zavolá funkci `command_put`, ještě před odesláním zprávy serveru. Funkce uloží data souboru, který se má odeslat, do proměnné `file_buffer`. Obsah proměnné se uloží na konec zprávy serveru.

Odpověď ze serveru se zanalyzuje ve funkci `parse`.  Funkce ověří, že hlavička obsahuje zprávu `HTTP/1.1 200 OK`. V případě, že neobsahuje, funkce vypíše do`stderr` obsah těla odpovědi serveru. Tělo obsahuje podrobný popis chyby a ukončí program.

V případě operace 
- `GET` - program zavolá funkci `command_get`, která uloží požadovaný soubor
- `LST` - program vypíše data z těla odpovědi serveru, která obsahují informace o obsahu adresáře na serveru


### OPTIONS
- COMMAND 
  - příkaz co se má provést na serveru
- REMOTE-PATH
  - cesta k souboru nebo adresáři na serveru
- LOCAL-PATH
  - cesta v lokální souborovém systému, povinné pro put
  
### DIAGNOSTICS 
- "Not a directory." 
	- když REMOTE-PATH ukazuje na soubor, ale je použita operace lst, rmd
- "Directory not found." 
	- když REMOTE-PATH neukazuje na žádny existující objekt při použití operace lst, rmd
- "Directory not empty." 
	- když REMOTE-PATH ukazuje na adresář, který není prázdný a je použita operace rmdir
- "Already exists." 
	- když REMOTE-PATH ukazuje na adresář/soubor, který již existuje a je použita operace mkd či put.
- "Not a file." 
	- když REMOTE-PATH ukazuje na adresář, ale je použita operace del, get.
- "File not found." 
	- když REMOTE-PATH neukazuje na žádny existující objekt při použití operace del, get
- "User Account Not Found" 
	- pokud je operace nad neexistujícím uživatelem.
- "Unknown error." 
	- pro ostatní chyby.
  
  
## Server - ftrestd 
 aplikace pro přenos souborů, která komunikuje pomocí HTTP a využívá jednoduché RESTful API

### SYNOPSIS
`ftrestd [-r ROOT-FOLDER] [-p PORT]`

### DESCRIPTION
Server čeká na zprávu od klienta. Jakmile ji obdrží, pošle ji ke zpracování do funkce `parse`. Funkce žádost zpracuje. První řádek HTTP hlavičky rozdělí na cestu k souboru/adresáři a na příkaz, podle kterého zavolá požadovanou funkci `command_XYZ`, kde XYZ reprezentuje příkaz ze zprávy.

Každá z funkcí `command_XYZ` vrací svoje výsledky i výpisy chybových stavů v proměnné `file_buffer`. `file_buffer` se ukládá na konec odpovědi pro klienta. Hlavička odpovědi závisí, zda některá z funkcí `command_XYZ` vrátila jinou hodnotu než `OK`.


### OPTIONS
- \- r
  - specifikuje kořenový adrssář, kde budou ukládány soubory pro jednotlivé uživatele, defaultní hodnota je aktuální 
- \- p
  - specifikuje port, na kterém bude server naslouchat, implicitně 6677

### DIAGNOSTICS 
- "Not a directory." 
	- když REMOTE-PATH ukazuje na soubor, ale je použita operace lst, rmd
- "Directory not found." 
	- když REMOTE-PATH neukazuje na žádny existující objekt při použití operace lst, rmd
- "Directory not empty." 
	- když REMOTE-PATH ukazuje na adresář, který není prázdný a je použita operace rmdir
- "Already exists." 
	- když REMOTE-PATH ukazuje na adresář/soubor, který již existuje a je použita operace mkd či put.
- "Not a file." 
	- když REMOTE-PATH ukazuje na adresář, ale je použita operace del, get.
- "File not found." 
	- když REMOTE-PATH neukazuje na žádny existující objekt při použití operace del, get
- "User Account Not Found" 
	- pokud je operace nad neexistujícím uživatelem.
- "Unknown error." 
	- pro ostatní chyby.
  
## AUTHOR
 Tomáš Dyk - xdykto00
