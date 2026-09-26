# Rent A Car Leli: si ta vendosësh online

Faqja ka tre pjesë:

- **index.html**: faqja për klientët (makinat, çmimet, rezervimi, kontakti)
- **rezervimi.html**: klienti e sheh statusin e rezervimit (Në pritje / Aprovuar / Refuzuar)
- **admin.html**: paneli yt, ku sheh rezervimet dhe i aprovon

**Për ta parë:** hape zip-in (Extract), pastaj hap `index.html` me dy klikime. Mos i nxirr skedarët nga dosja, sepse `css/`, `js/` dhe `img/` duhet të jenë bashkë me faqen.

Derisa të mos e lidhësh me Firebase, faqja punon në **modalitet DEMO**. Rezervimet ruhen vetëm në shfletuesin tënd, dhe fjalëkalimi i panelit është `demo`.

---

## 1. Krijo databazën falas (Firebase), rreth 10 minuta

1. Hyr në https://console.firebase.google.com me llogarinë Google, pastaj **Add project**. Emri: `rentacar-leli`. Google Analytics nuk të duhet.
2. **Build → Firestore Database → Create database**. Zgjidh lokacionin `europe-west` dhe **Production mode**.
3. Te Firestore, hap skedën **Rules**. Fshi çka ka aty dhe ngjit përmbajtjen e skedarit `firestore.rules`. **Ndrysho emailin** `VENDOS_EMAILIN_E_ADMINIT@gmail.com` me emailin e adminit. Shtyp **Publish**.
4. **Build → Authentication → Get started → Email/Password → Enable**.
5. Te **Users → Add user**, shkruaj emailin dhe një fjalëkalim të fortë. Me këto hyn në panel.
6. Te **Authentication → Settings → User actions**, hiq shenjën te **Enable create (sign-up)**. Kështu askush tjetër nuk mund të hapë llogari.
7. **Project settings** (ikona ⚙️) **→ Your apps → Web (</>)**. Regjistro aplikacionin dhe kopjo vlerat e `firebaseConfig`.
8. Hap `js/config.js`:
   - ngjit vlerat te `FIREBASE_CONFIG`
   - vendos të njëjtin email te `ADMIN_EMAIL`

Me kaq, modaliteti demo fiket dhe faqja punon me të dhëna të vërteta.

## 2. Vendos fotot e makinave

Fotografo makinat me telefon në dritë dite. Foto horizontale nga ana ose nga para-anash duken më mirë. Ruaji në dosjen `img/makinat/` me saktësisht këta emra:

- `astra.jpg`
- `corsa.jpg`
- `captur.jpg`

Tani aty janë fotot që dërgove. Për t'i ndërruar, zëvendëso skedarët me të njëjtët emra. Nëse një foto mungon, faqja shfaq një ilustrim me ngjyrën e makinës.

## 3. Kontrollo të dhënat e makinave

Të gjitha makinat janë me naftë dhe automatike. Nëse ndryshon diçka, p.sh. përshkrimet, hap `js/cars.js`.

## 4. Publikoje online falas (Netlify)

1. Hap https://app.netlify.com/drop dhe krijo llogari falas.
2. Tërhiq të gjithë dosjen `rentacar-leli` në faqe. Për pak sekonda merr një link, p.sh. `rentacar-leli.netlify.app`. Emrin mund ta ndryshosh te **Site settings**.
3. Kthehu te Firebase: **Authentication → Settings → Authorized domains → Add domain** dhe shto domenin e Netlify-t.
4. Kur ndryshon diçka (foto, tekste), tërhiqe dosjen përsëri te **Deploys**.

Nëse më vonë blen domen (p.sh. `rentacarleli.com`), e lidh te Netlify → **Domain settings**.

## 5. Si e përdor babai panelin

1. Hap `emrifaqes.netlify.app/admin.html` në telefon dhe ruaje në ekranin kryesor (**Add to Home screen**).
2. Kur vjen rezervim i ri, del te **Në pritje**. Numri shfaqet edhe në titullin e faqes.
3. Shtyp **Aprovo** dhe ndodhin tri gjëra:
   - makina shfaqet **e zënë** për ato data në faqe, dhe të tjerët nuk mund ta rezervojnë
   - klienti e sheh statusin **Aprovuar** te faqja e rezervimit
   - hapet mesazhi i gatshëm: shtyp **Dërgo në WhatsApp** (ose SMS), pastaj vetëm **Send**
4. **Refuzo** e hap mesazhin e refuzimit në të njëjtën mënyrë.
5. Kur klienti e kthen makinën, shtyp **U kthye** dhe makina lirohet.
6. Nëse dikush rezervon me telefon, përdor **Shëno të zënë** te kalendari që ta bllokosh makinën.

**Pse mesazhi nuk dërgohet vetë:** SMS-të automatike kërkojnë shërbim me pagesë (p.sh. Twilio). Kështu mesazhi del nga numri i babait, falas, dhe klienti e njeh se kush i shkruan.

## Çmimet

Ndryshohen te `js/config.js` → `CMIMET`. Tani janë: 1 ditë 40€, 2 ditë 35€/ditë, 3+ ditë 30€/ditë.
