# IPK
## Client
 aplikace pro přenos souborů, která komunikuje pomocí HTTP a využívá jednoduché RESTful API

### SYNOPSIS
`ftrest COMMAND REMOTE-PATH [LOCAL-PATH]`

### DESCRIPTION
asdf

### OPTIONS
- COMMAND 
  - je příkaz 
- REMOTE-PATH
  - je cesta k souboru nebo adresáři na serveru
- LOCAL-PATH
  - je cesta v lokální souborovém systému, povinné pro put
  
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
  
  
## Server
 aplikace pro přenos souborů, která komunikuje pomocí HTTP a využívá jednoduché RESTful API

### SYNOPSIS
`ftrestd [-r ROOT-FOLDER] [-p PORT]`

### DESCRIPTION
asdf

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
