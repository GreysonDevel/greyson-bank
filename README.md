# Testovací projekt pro kandidáty Dev Capability

## Zadání 

Vytvořte aplikaci digitální banky Greyson. Internetové bankovnictví známe všichni, zkoušeli jste si ho ale někdy implementovat? V tomto projektu je cílem zobrazit informace o přihlášeném klientovi, jeho bankovním účtu, transakcích a detailu transakce. Pokud vás bude implementace bavit, můžete se pustit i do simulované možnosti odchozí platby a správy platebních karet.

odhadovaná časová náročnost: 4 - 8h

## Pro backend vývojáře

Naimplementujte backend části Greyson banky pro jednoduché internetové bankovnictví pomocí jednoho z programovacích jazyků:

* Java 17
* Kotlin

Můžete začít psát projekt na zelené louce, nebo vycházet z těchto předpřipravených základů projektů:

[https://github.com/GreysonDevel/sample-be](https://github.com/GreysonDevel/sample-be)

Funkčnost implementace APIs můžete ověřit voláním přes Swagger / OpenAPI, případně můžete využít FE část aplikace:

FE –  Připravená frontendová část Greyson banky

[https://github.com/GreysonDevel/greyson-bank-fe](https://github.com/GreysonDevel/greyson-bank-fe)

### Očekávaný výstup

* běžící backendová aplikace Greyson banky
* implementace API pro zobrazení informace o klientovi a jeho bankovním účtu
* implementace API pro zobrazení přehledu transakcí

### Bonusové body za

* čitelnost, čistotu kódu
* funkční  test
* lokálně běžící FE i BE části aplikace 
* příprava testovacích dat
* implementace API pro odchozí platbu
* implementace API pro seznam platebních karet
* implementace API pro blokování platebních karet

## Pro frontend vývojáře

Vytvořte frontend Greyson banky pro jednoduché internetové bankovnictví pomocí  jednoho z UI frameworků / knihoven:

* Angular
* React 

Vycházejte z těchto předpřipravených základů projektů:

[https://github.com/GreysonDevel/sample-react](https://github.com/GreysonDevel/sample-react)

[https://github.com/GreysonDevel/sample-angular](https://github.com/GreysonDevel/sample-angular)

Jako bankovní backend pro integraci využijte naši běžící Greyson Banka aplikaci, respektive její Bankovní API (backend) : 

https://app.test.greyson.tech/greyson-bank-be/swagger-ui/index.html?configUrl=/greyson-bank-be/v3/api-docs/swagger-config#/

### Očekávaný výstup

* běžící frontendová aplikace Greyson banky
* zobrazení informace o klientovi a jeho bankovním účtu
* zobrazení přehledu transakcí

### Bonusové body za

* čitelnost, čistotu kódu
* funkční  test
* odchozí platba
* správa platebních karet

## Use Cases

Popisují očekávané chování aplikace, slouží pro lepší pochopení zadání FE / BE

### Zobrazení účtů uživatele

* Uživatel si otevře úvodní stránku
* Uživatel klikne na přihlašovací tlačítko
* Systém zobrazí všechny účty uživatele

### Zobrazení účtu uživatele s transakcemi

* Uživatel klikne na detail účtů
* Systém zobrazí informace o účtu
    * Název účtu
    * IBAN
    * Stav účtu
    * měna
* Systém zobrazí přehled transakcí
    * Datum vykonání transakce
    * Odesílatel
    * Příjemce
    * Částka

### Platba

* Uživatel si vybere účet
* Uživatel stiskne tlačítko platba
* Uživatel zadá detail transakce
    * Příjemce
    * Částka
* Uživatel stiskne tlačítko zaplatit
* Systém vytvoří transakci pro daný účet
* Systém aktualizuje seznam transakcí uživatele

### Blokování / Odblokování karty

* Uživatel si vybere účet
* Uživatel si vybere kartu ze seznamu karet pro daný účet
* Uživatel stiskne tlačítko blokovat / odblokovat
* Systém nastaví atribut _blocked _karty na **true **pro blokování, **false **pro odblokování
* Systém aktualizuje informace o kartách pro daný účet

## API + Model


### GET /api/user

response: User

* id: long
* firstName: string
* lastName: string
* birthDate: date

### GET /api/accounts?userId={userId}

Response: Account[]


### GET /api/accounts/{id}

response: Account

* id: long
* IBAN: string
* name: string
* balance: decimal
* currency: string (3)

### GET /api/accounts/{id}/transactions

response: Transaction[]

* id: long
* amount: decimal
* creditor: string (odesílatel)
* debtor: string (příjemce)
* dateCreated: date
* dateExecuted: date

### POST /api/accounts/{id}/transactions

Request: Transaction

* amount: decimal
* debtor: string

### GET /api/accounts/{id}/cards

Response: Cards[]


### GET /api/accounts/{id}/cards/{id}

Response: Card

* id: long
* name: string
* blocked: boolean
* dateLocked: date


### PUT /api/accounts/{id}/cards/{id}

Request:

* blocked: boolean
