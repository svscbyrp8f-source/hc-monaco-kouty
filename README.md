# HC Monaco Kouty — PWA prototyp

## Co je v balíčku
- Mobilní webová aplikace s přehledem, soupiskou, zápasy a sezónními statistikami.
- Ruční zadávání výsledků, gólů, asistencí, +/- a trestných minut.
- Fotky hráčů se zmenší a uloží v prohlížeči.
- Export/import JSON zálohy.
- PWA manifest a service worker pro přidání na domovskou obrazovku.

## Důležité omezení této první verze
Tato verze je **prototyp**. Data se ukládají pouze do konkrétního prohlížeče v zařízení (`localStorage`). Nesynchronizují se mezi telefony. Sekce Správa není zabezpečena skutečným přihlášením. Proto ji zatím nepoužívejte jako veřejnou týmovou aplikaci se soukromými daty a nespoléhejte na ni jako na zabezpečený admin systém.

## Doporučené bezplatné dokončení pro sdílenou aplikaci
Použít Firebase na tarifu Spark (bez zadání platební karty pro běžné funkce) a Firebase Hosting:
1. Založ projekt na https://console.firebase.google.com/
2. Přidej webovou aplikaci a zkopíruj její konfiguraci.
3. Zapni Authentication → Email/Password a vytvoř svůj administrátorský účet.
4. Vytvoř Cloud Firestore databázi v režimu produkce.
5. Před zveřejněním doprogramuj napojení na Firestore a ověřeného správce. Firestore pravidla musí povolit veřejné čtení jen kolekcí, které chceš zpřístupnit, a zápis pouze konkrétnímu UID správce. Nikdy nepoužívej otevřená pravidla typu `allow read, write: if true`.
6. Pro fotky zvol buď komprimované fotografie v samostatném řešení pro soubory, nebo URL obrázků. Před použitím Firebase Storage ověř aktuální požadavky na tarif a limity.
7. Nahraj PWA na Firebase Hosting (ne na App Hosting, které vyžaduje Blaze) a otestuj přístup na Androidu i iPhonu.
8. Zkontroluj aktuální limity Firebase: https://firebase.google.com/pricing a https://firebase.google.com/docs/firestore/pricing.

## Výpočet statistik
- Body = góly + asistence.
- Průměr gólů na zápas = góly / počet zápasů, ve kterých hráč nastoupil.
- Plus/minus a trestné minuty se sčítají z hodnot zadaných v jednotlivých zápasech.
- Skóre týmu a bilance W-D-L se sčítají z odehraných zápasů.

## Nasazení
Souborová struktura je standardní statická PWA. Nahraj obsah složky na HTTPS hosting. Samotné otevření souboru `index.html` umožní prohlídku, ale instalace PWA a service worker vyžadují HTTPS nebo localhost. Pro ostré nasazení nejprve doplň sdílenou databázi a autentizaci podle výše uvedených kroků.
