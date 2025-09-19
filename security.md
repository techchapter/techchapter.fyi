# Security Awareness

Som mindre konsulenthus med adgang til kunders systemer, forretningshemmeligheder og kritisk infrastruktur er vi et attraktivt mål. Et brud hos os kan få konsekvenser for både vores egen drift og for kunder med kritisk infrastruktur. Angribere går efter penge, data og adgang — ofte ved at få almindelige mennesker til at begå helt almindelige fejl:

- **Phishing/BEC**: overbevisende e-mails, sms’er eller kalenderinvites, der lokker til klik, betaling eller deling af oplysninger.

- **Uautoriseret adgang til konti**: via stjålne eller gættede adgangskoder, genbrug af samme kode flere steder eller omgåelse af to-faktor-godkendelse.

- **Social engineering**: telefonopkald og beskeder, der udgiver sig for chefer, kolleger eller leverandører.

- **Malware/ransomware**: skadelige vedhæftninger, links eller inficerede downloads/USB-enheder.

- **Fejldeling af data**: for brede delingsrettigheder, forkerte modtagere eller ukrypteret deling af følsomt materiale.

- **Svage enheder og netværk**: manglende opdateringer, ulåste skærme, usikre offentlige Wi-Fi.

Undlad at fortælle om egne og kollegaers opgaver for kunder udadtil. Det er med til at øge opmærksomheden omkring de opgaver vi arbejder med, og dermed eksponere os som potentielle mål.

For at beskytte Tech Chapter og vores kunder bedst muligt er det vigtigt, at alle medarbejdere læser og overholder nedenstående retningslinjer. Overtrædelse kan medføre ansættelsesretlige konsekvenser, herunder bortvisning og – i grove tilfælde – politianmeldelse.

## Password hygiene & MFA

De fleste kompromitteringer starter med password-genbrug eller phishing, som giver angribere adgang til konti. MFA reducerer risikoen markant, men virker kun, hvis den er aktiveret og brugt korrekt.

Fålgende retningslinjer skal overholdes:

- **Brug 1Password som eneste password manager**: Anvend aldrig post-it, notepad, chrome password manager, apple keystore el. lign. TOTP skal ligeledes anvendes gennem 1Password. Brug ikke Google Authenticator, Duo, m.v.

- **Deling af passwords**:

  - **Personlige passwords**: Må aldrig deles.
  - **System-/shared-konti**: Må aldrig deles i klartekst (mail, chat, tickets, screenshots). Del udelukkende via 1Password (delt vault eller tidsbegrænset Share med adgangskrav).

- **Unikke, stærke passwords**: Brug 1Password’s generator (min. 16+ tegn) og genbrug aldrig passwords mellem services. Nej CorrectHorseStable er ikke mere sikkert.

- **Brug dedikerede vaults**: `Employee` vault til egne Tech Chapter adgange. Opret særskilt vault til kundeadgange, der slettes ved offboarding.

- **MFA som standard**: Registrér to FIDO2-nøgler (primær + backup) og brug TOTP som fallback. Undgå SMS og E-mail hvor muligt.

- **Slå Watchtower til** i 1Password og ryd “svage/genbrugte/kompromitterede/2FA available”-fund løbende (målsætning: 0 findings).

- **SSO først**: Brug SSO mod IdP, undgå lokale konti hvor muligt. Brug short-lived tokens fremfor statiske credentials.

- **Automatisering (op CLI)**: Hent secrets kun ved runtime (op run --env …). Log aldrig hemmeligheder, skriv dem ikke til filer, og maskér CI-logs.

- **Forbudt opbevaring**: Ingen passwords i browsere, notes/apps, regneark, tekstfiler eller screenshots. Brug kun 1Password.

- **Rotation**: Roter straks ved mistanke om læk eller rolleændring eller watchtower notifikation; Personlige SSH keys (Git/servers) roteres hver 12. måned.

- **Ved mistanke om kompromis**: Skift password, log ud af alle sessions, tilbagekald tokens, anmeld via incident-flowet straks.

- **Print din Emergency Kit** (PDF), placer den i en forseglet konvolut og opbevar den i Tech Chapters pengeskab. Kodeordet skal ikke opbevares sammen med emergency kit, men evt. i et pengeskab pá Tech Chapters andet kontor.

## Phishing awareness

Phishing er vores største “entry point”: Angribere bruger meget overbevisende e-mails/SMS/Teams/Slack/kalenderinvites og QR-koder for at få dig til at klikke, indtaste login, eller godkende MFA. Ét forkert klik kan give adgang til mail, filer og systemer – og blive springbræt til kunderne.

- **BEC (Business Email Compromise)**: falske beskeder fra “chef/leverandør” om betaling eller kontoskift.
- **Credential harvesting**: login-side der ligner den ægte for at stjæle brugernavn/password.
- **MFA fatigue**: mange push-prompter, så du trykker “Approve” på autopilot.
- **OAuth consent phishing**: pop-up beder om tilladelser til din konto (e-mail, filer, kalender).
- **Malware**: vedhæftninger/ZIP’er/“fakturaer”, der installerer skadelig software.
- **QR-phishing**: plakater/kort med QR til falske portaler.

For at gøre phishing svært at lykkes og nemt at opdage hos os, omsætter vi ovenstående risici til konkrete arbejdsregler:

- **Internt**: Brug Slack. E-mail bruges kun til eksterne.
- **Kunder**: Brug Slack/Teams hvor muligt; e-mail kun når nødvendigt og uden følsomme data.
- **Verificér altid på kendt kanal**: Ring på kendt nummer eller start ny tråd i Slack/Teams—aldrig via nummer/link i beskeden.
- **Ingen secrets i chat/e-mail.** Del kun via 1Password (vault eller tidsbegrænset Share).
- **Brug 1Password browser plugin**: 1Passwords domain-matching (exact domain) og gem TOTP i samme item.

## Datahåndtering

Beskyt kunders og vores egne oplysninger ved konsekvent klassifikation, korrekt opbevaring og sikker deling.

- Alle binære dokumenter (excel, docs, pptx, pdf, mv) opbevares på Tech Chapters filserver
- Alle text dokumenter (code, markdown, yaml, mv) opbevares på Tech Chapters GitHub account.
- Det er ikke tilladt at dele filer på USB, private cloudtjenester, private e-mails, Slack-filer.
- Kun “pull-print”/sikret print. Hent straks udskrevne dokumenter.
- Lås fortrolige dokumenter inde i skabe eller pengeskabe når de opbevares på kontoret.
- Makulér alt med kundedata, persondata eller interne fortrolige oplysninger efter brug.

## Acceptable Use & AI

AI-tjenester kan logge/træne på prompts/filer, apps/plugins kan trække repo-/kundedata, og code assistants kan indføre licens-/sikkerhedsfejl. Ét forkert paste kan lække trade secrets, persondata eller credentials.
Brug derfor AI med omtanke og del kun data, der du normalt ville kunne dele med tredjepart.

- **Code assistants (Copilot m.fl.)** må som aldrig anvendes på kunders data medmindre der eksplicit er givet tilladelse. Vær opmærksom på ikke at installere AI tooling, der giver adgang til diske, terminal, m.v.

- **Anvend de-identificering/syntetiske data og placeholders**: <CUSTOMER_NAME>, <API_KEY>, osv.

- **Kom aldrig følgende ind i AI**:
  - **Kundedata/persondata** (GDPR), **kontrakter/SOW** med identificerbare oplysninger.
  - **Credentials/secrets** (passwords, tokens, SSH keys, kubeconfigs), log-uddrag med secrets.
  - **Proprietary kode/arkitektur**, interne diagrammer, netværks-/IAM-detaljer, **Terraform/k8s el lign. values** med miljøspecifik info.
  - Screenshots af dashboards/alarms med PII eller miljønavne.

## E-mail & dokumenthåndtering

Fejldeling, spoofing/BEC og ukrypteret afsendelse kan lække kundedata/forretningshemmeligheder og udløse GDPR/kontrakt-brud. E-mail er let at forfalske og bør kun bruges eksternt – internt bruger vi Slack.

- **Internt**: brug Slack. E-mail kun eksternt og uden secrets.
- **Ingen secrets i e-mail** (passwords, tokens, SSH keys, kubeconfigs). Del kun via 1Password.
- **Del link frem for vedhæftning**: Specifike personer, brug udløb, “view only”.
- **Fakturaer** fra eksterne leverandører sendes til din egen e-mail og videresendes til betaling over slack.

## Fysisk sikkerhed

- Lås skærm når du går; ryd skrivebord ved dagens slutning.
- Opbevar følsomme papirer i låst skab/skuffe.
- Brug privacy filter ved behov.
- Laptop/telefon på dig eller låst inde;

## Enheder & adgang (baseline)

- **Lås enheder** når de efterlades. Aktiver automatisk låsning efter 5 minutters inaktivitet.
- **Opdater software**: Telefon, OS, Browser og apps skal løbende holdes opdateret for at
- **Full-disk encryption** skal slåes til på alle enheder.
- **Aktiver find my iPhone/Device** på mobile enheder.
