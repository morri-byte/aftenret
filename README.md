# 🍲 Aftenret

13 hverdagsretter til 2 voksne og et barn: ugeplan, indkøbsliste per ret og kokketilstand med timer.

- `www/index.html`: hele appen (HTML, CSS og JavaScript i én fil)
- `ios/`: det native iOS-projekt, som pakker appen ind (Capacitor 8, Swift Package Manager)
- `resources/`: kildebilleder til app-ikon og opstartsskærm

## Kør appen i browseren

Åbn `www/index.html` direkte i en browser. Det kræver ingen server.

## Byg og upload til App Store

Det skal gøres på en **Mac med Xcode** (version 16 eller nyere). Apple tillader ikke iOS-builds på andre systemer.

### 1. Forudsætninger
- En betalt **Apple Developer**-konto (99 USD om året): https://developer.apple.com/programs/
- Node.js 20 eller nyere og Xcode

### 2. Hent og forbered projektet
```bash
git clone https://github.com/morri-byte/aftenret.git
cd aftenret
npm install
npx cap sync ios      # kopierer www/ ind i iOS-projektet
npx cap open ios      # åbner Xcode
```

### 3. I Xcode
1. Vælg projektet **App**, derefter target **App** og fanen **Signing & Capabilities**.
2. Vælg dit **Team** (din Apple Developer-konto). Lad "Automatically manage signing" være slået til.
3. Bundle Identifier er sat til `dk.aftenret.app`. Hvis den er optaget, så ret den til noget unikt, fx `dk.ditnavn.aftenret`. Ret den også i `capacitor.config.json`.
4. Test på din egen iPhone: tilslut telefonen, vælg den øverst i Xcode og tryk ▶︎.

### 4. Opret appen i App Store Connect
1. Gå til https://appstoreconnect.apple.com, vælg **Apps** og tryk **+**, derefter **Ny app**.
2. Platform: iOS. Navn: *Aftenret* (eller et ledigt navn). Primært sprog: dansk. Bundle ID: det samme som i Xcode.

### 5. Upload buildet
1. Vælg **Any iOS Device (arm64)** øverst i Xcode.
2. Vælg **Product › Archive**.
3. I vinduet Organizer vælger du **Distribute App**, derefter **App Store Connect** og **Upload**.
4. Efter 10-30 minutter vises buildet i App Store Connect under **TestFlight**. Her kan du teste det, før du sender det til gennemgang.

### 6. Udfyld App Store-siden
- **Skærmbilleder**: mindst 3 i størrelsen 6,9" (1320 × 2868). Tag dem fra iPhone 16 Pro Max-simulatoren i Xcode (⌘S).
- **Beskrivelse, nøgleord, supportside-URL** (påkrævet) og **privatlivspolitik-URL** (påkrævet).
- **App Privacy**: vælg "Data Not Collected". Appen gemmer kun dine valg lokalt på telefonen.
- **Aldersgrænse**: udfyld spørgeskemaet; appen bliver 4+.
- Tryk **Tilføj til gennemgang**.

## Når appen er ændret
Ret i `www/index.html`. Kør derefter `npx cap sync ios`, hæv **Build**-nummeret (og eventuelt **Version**) i Xcode, og arkivér og upload igen.

## Godt at vide
- Apple afviser nogle gange apps, der "bare er en hjemmeside" (retningslinje 4.2). Aftenret fungerer helt uden internet og har egen funktionalitet, hvilket taler for appen. Hvis den alligevel bliver afvist, kan native funktioner som notifikation når timeren er færdig, eller at skærmen holdes tændt i kokketilstand, styrke ansøgningen.
- App-ikonet i `resources/icon.png` er en enkel første version. Udskift det gerne med et designet ikon (1024 × 1024 px uden gennemsigtighed) i `ios/App/App/Assets.xcassets/AppIcon.appiconset/`.
