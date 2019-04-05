<template>
  <div id="app">
    <v-app>
      <v-toolbar app>
        <v-icon large left>mdi-chart-line</v-icon>
        <v-toolbar-title>LMS keretrendszerek az iskolarendszerű szakképzésben - kérdőív tanulók számára</v-toolbar-title>
        <v-spacer/>
      </v-toolbar>
      <v-content>
        <v-container fluid>
          <v-layout row wrap justify-center>
            <!-- Bevezető -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-information-outline</v-icon>
                    <span>
                      Kedves Tanuló!
                      <br>A BME GTK Alkalmazott Pedagógia és Pszichológia
                      Intézet Műszaki Pedagógia Tanszék Közoktatási Vezető és pedagógus-szakvizsga szakirányú továbbképzési
                      szak végzős hallgatójaként készítem szakdolgozatomat.
                      <br>A dolgozat címe:
                      <br>
                      <b>E-learning keretrendszerek alkalmazása az iskolarendszerű szakképzésben</b>
                      <br>Kérlek, hogy a következő kérdőív kitöltésével segítsed kutatásomat!
                      <br>Köszönettel: Nits László
                    </span>
                  </div>
                </v-card-title>
              </v-card>
            </v-flex>
            <!-- 1. Neme férfi/nő -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-gender-male-female</v-icon>
                    <span>1. A kérdőívet kitöltő neme:</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-switch
                    color="success"
                    class="bordered pl-4 pt-4"
                    v-model="ferfi"
                    :label="`${ferfi ? 'Férfi' : 'Nő'}`"
                  ></v-switch>
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 2. Melyik évfolyamon tanulsz? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>directions_walk</v-icon>
                    <span>2. Melyik évfolyamon tanulsz?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    :items="evfolyamLista"
                    suffix="évfolyam"
                    clearable
                    label="Évfolyam"
                    outline
                    v-model="evfolyam"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 3. Melyik megyében található az intézmény, ahol tanulsz? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>place</v-icon>
                    <span>3. Melyik megyében található az intézmény, ahol tanulsz?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="megyekLista"
                    clearable
                    label="Megye"
                    outline
                    v-model="megyek"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>

            <!-- 4. Milyen típusú tantárgyaknál használtok LMS (Moodle, Canvas, stb.) rendszereket? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-library</v-icon>
                    <span>4. Milyen típusú tantárgyaknál használtok LMS (Moodle, Canvas, stb.) rendszereket?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    :items="tantargyakTipusaLista"
                    clearable
                    chips
                    multiple
                    label="Tanárgyak típusa"
                    outline
                    v-model="tantargyakTipusa"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 5.	Hány tanévben használtál már e-learning (LMS) keretrendszert -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-weather-sunset-down</v-icon>
                    <span>5.	Hány tanévben használtál már e-learning (LMS) keretrendszert?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    :items="evekLista"
                    suffix
                    clearable
                    label="Tanévek száma"
                    outline
                    v-model="lmsHanyEve"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 6.	Milyen eszközön használod az e-learning (LMS) keretrendszer szolgáltatásait? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>school</v-icon>
                    <span>6. Milyen eszközön használod az e-learnig (LMS) keretrendszer szolgáltatásait?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="eszkozLista"
                    clearable
                    chips
                    multiple
                    label="Eszköz(ök)"
                    outline
                    v-model="lmsEszkoz"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>


            <!-- 7.	Milyen gyakran használod az LMS keretrendszert a szorgalmi időszakban? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon large left>mdi-metronome</v-icon>
                    <span>7. Milyen gyakran használod az LMS keretrendszert a szorgalmi időszakban?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista"
                    suffix
                    clearable
                    label="Használat gyakorisága"
                    outline
                    v-model="lsmHasznalatGyakorisaga"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>

            <!-- 8.	A következő LMS szolgáltatásokat ha ismered, akkor mennyire tartod hasznosnak? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon large left>mdi-chart-histogram</v-icon>
                    <span>8.	A következő LMS szolgáltatásokat ha ismered, akkor mennyire tartod hasznosnak?</span>
                  </div>
                </v-card-title>
                <!-- Quiz -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="8.1 Tesztek tanulói teljesítmény méréséhez"
                    outline
                    v-model="tesztGyakorisaga"
                  />
                </v-card-actions>
                <!-- Assignment -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.2 Tanulói munkák (órai / házi) feltöltése"
                    outline
                    v-model="feladatGyakorisaga"
                  />
                </v-card-actions>
                <!-- Forum -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.3 Fórumok használata (aszinkron kommunikáció)"
                    outline
                    v-model="forumGyakorisaga"
                  />
                </v-card-actions>
                <!-- File -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.4 Meglévő digitális tananyagok megosztása"
                    outline
                    v-model="tananyagGyakorisaga"
                  />
                </v-card-actions>
                <!-- Page -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.5 Digitális tananyagok készítése az LMS keretrendszeren belül"
                    outline
                    v-model="oldalGyakorisaga"
                  />
                </v-card-actions>
                <!-- URL -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.6 Hivatkozások (URL címek) megosztása"
                    outline
                    v-model="urlGyakorisaga"
                  />
                </v-card-actions>
                <!-- Glossary -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.7 Fogalomtár készítése"
                    outline
                    v-model="fogalomtarGyakorisaga"
                  />
                </v-card-actions>
                <!-- Feedback -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.8 Tanulói visszajelzések"
                    outline
                    v-model="visszajelzesGyakorisaga"
                  />
                </v-card-actions>
                <!-- Choice -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.9 Tanulói választások"
                    outline
                    v-model="valasztasGyakorisaga"
                  />
                </v-card-actions>
                <!-- Database -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.10 Adatbázisok létrehozása / kezelése"
                    outline
                    v-model="adatbazisGyakorisaga"
                  />
                </v-card-actions>
                <!-- Wiki -->
                <v-card-actions>
                  <v-select
                    :items="gyakorisagLista2"
                    suffix
                    clearable
                    :disabled="!lmsYorN"
                    label="10.11 Wiki oldalak készítése (tanulói együttműködés)"
                    outline
                    v-model="wikiGyakorisaga"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 11. Mennyire tartja hasznosnak az LMS keretrendszer alkalmazását a nappali képzésben? -->
            <v-flex xs12 sm12 md12 lg12 xl12 v-show="lmsYorN">
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-weather-sunny</v-icon>
                    <span>11. Mennyire tartja hasznosnak az LMS keretrendszer alkalmazását a nappali képzésben?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="hasznossagLista"
                    clearable
                    :disabled="!lmsYorN"
                    label="Nappali képzésben"
                    outline
                    v-model="hasznosNappali"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 12. Mennyire tartja hasznosnak az LMS keretrendszer alkalmazását az esti képzésben? -->
            <v-flex xs12 sm12 md12 lg12 xl12 v-show="lmsYorN">
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-weather-sunset</v-icon>
                    <span>12. Mennyire tartja hasznosnak az LMS keretrendszer alkalmazását az esti képzésben?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="hasznossagLista"
                    clearable
                    :disabled="!lmsYorN"
                    label="Esti képzésben"
                    outline
                    v-model="hasznosEsti"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- 13. Általánosságban mennyire elégedett az Ön által használt LMS keretrendszerrel? -->
            <v-flex xs12 sm12 md12 lg12 xl12 v-show="lmsYorN">
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-emoticon-happy</v-icon>
                    <span>13. Általánosságban mennyire elégedett az Ön által használt LMS keretrendszerrel?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="elegedettsegiLista"
                    clearable
                    :disabled="!lmsYorN"
                    label="Elégedettség"
                    outline
                    v-model="lmsElegedett"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>
            <!-- MENTÉS -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>save</v-icon>
                    <span>Mentés</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-btn class="mx-auto" dark color="red" @click="add()">Kérdőív adatainak mentése</v-btn>
                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-content>
      <v-footer/>
    </v-app>
  </div>
</template>

<script  lang="ts">
import { Component, Vue } from "vue-property-decorator";
import firebase, { storage } from "firebase";
import db from "@/firebaseApp";

@Component({
  firestore: {
    locations: db.collection("kvk2019")
  }
})
export default class App extends Vue {
  private megyekLista: string[] = [
    "Budapest",
    "Bács-Kiskun megye",
    "Baranya megye",
    "Békés megye",
    "Borsod-Abaúj-Zemplén megye",
    "Csongrád megye",
    "Fejér megye",
    "Győr-Moson-Sopron megye",
    "Hajdú-Bihar megye",
    "Heves megye",
    "Jász-Nagykun-Szolnok megye",
    "Komárom-Esztergom megye",
    "Nógrád megye",
    "Pest megye",
    "Somogy megye",
    "Szabolcs-Szatmár-Bereg megye",
    "Tolna megye megye",
    "Vas megye",
    "Veszprém megye",
    "Zala megye"
  ];

  private evfolyamLista: string[] = [
    "Nyelvi előkészítő évfolyam",
    "9.",
    "10.",
    "11.",
    "12.",
    "13-14."
  ];

  private tantargyakTipusaLista: string[] = [
    "Reál tantárgyak (pl.: matematika)",
    "Humán tantárgyak (pl. irodalom)",
    "Szakmai tantárgyak"
  ];

  private evekLista: string[] = ["1", "2", "3", "4", "5-"];

  private eszkozLista: string[] = [
    "Asztal számítógép",
    "Laptop",
    "Tablet",
    "Mobiltelefon"
  ];

  private kepzesiFormaLista: string[] = ["Nappali oktatás", "Esti oktatás"];

  private lmsRendszerekLista: string[] = [
    "Moodle",
    "CANVAS",
    "Ilias",
    "Blackboard Learn",
    "Sakai",
    "Egyéb"
  ];


  private gyakorisagLista: string[] = [
    "Hetente több, mint 1 alkalommal",
    "Hetente 1 alkalommal",
    "Havonta 1-2 alkalommal",
    "2-3 havonta",
    "Szinte alig"
  ];

  private gyakorisagLista2: string[] = [
    "Hetente legalább 1 alkalommal",
    "Havonta 1-2 alkalommal",
    "2-3 havonta",
    "Szinte alig",
    "Soha"
  ];

  private hasznossagLista: string[] = [
    "Nagyon hasznos",
    "Hasznos",
    "Kevésbé hasznos",
    "Nem hasznos",
    "Egyáltalán nem hasznos"
  ];

  private elegedettsegiLista: string[] = [
    "Nagyon elégedett vagyok",
    "Elégedett vagyok",
    "Semleges",
    "Kissé elégedetlen vagyok",
    "Elégedetlen vagyok"
  ];

  private ferfi: boolean = false; // 1
  private evfolyam: string = ""; // 2
  private megyek: string = ""; // 3
  private tantargyakTipusa: string[] = []; // 4
  private lsmHanyEve: string = ""; // 5
  private lmsEszkoz: string[] = []; // 6
  private lsmHasznalatGyakorisaga: string = ""; // 7

  private kepzesiForma: string[] = [];
  private lmsYorN: boolean = false;
  private lmsHasznal: string[] = [];
  private tesztGyakorisaga: string = "";
  private feladatGyakorisaga: string = "";
  private forumGyakorisaga: string = "";
  private tananyagGyakorisaga: string = "";
  private oldalGyakorisaga: string = "";
  private urlGyakorisaga: string = "";
  private fogalomtarGyakorisaga: string = "";
  private visszajelzesGyakorisaga: string = "";
  private valasztasGyakorisaga: string = "";
  private adatbazisGyakorisaga: string = "";
  private wikiGyakorisaga: string = "";
  private hasznosNappali: string = "";
  private hasznosEsti: string = "";
  private lmsElegedett: string = "";

  // Új elem hozzáadása az adatbázishoz
  private add(): void {
    let nemAdottVálaszt: string = "";
    if (this.evfolyam === "") {
      nemAdottVálaszt += "2.  ";
    }
    if (this.megyek.length === 0) {
      nemAdottVálaszt += "3.  ";
    }
    if (this.tantargyakTipusa.length === 0) {
      nemAdottVálaszt += "4.  ";
    }
    if (this.kepzesiForma.length === 0) {
      nemAdottVálaszt += "5.  ";
    }
    if (nemAdottVálaszt.length > 0) {
      // tslint:disable-next-line:max-line-length
      alert(
        `A kérdőív adatainak mentéséhez a következő kérdésekre a választ legyen szíves megadni: \r${nemAdottVálaszt}`
      );
      return;
    }

    if (this.lmsYorN) {
      nemAdottVálaszt = "";
      if (this.lmsHasznal.length === 0) {
        nemAdottVálaszt += "7.  ";
      }
      if (this.lsmHanyEve === "") {
        nemAdottVálaszt += "8.  ";
      }
      if (this.lsmHasznalatGyakorisaga === "") {
        nemAdottVálaszt += "9.  ";
      }
      if (this.tesztGyakorisaga === "") {
        nemAdottVálaszt += "10.1  ";
      }
      if (this.feladatGyakorisaga === "") {
        nemAdottVálaszt += "10.2  ";
      }
      if (this.forumGyakorisaga === "") {
        nemAdottVálaszt += "10.3  ";
      }
      if (this.tananyagGyakorisaga === "") {
        nemAdottVálaszt += "10.4  ";
      }
      if (this.oldalGyakorisaga === "") {
        nemAdottVálaszt += "10.5  ";
      }
      if (this.urlGyakorisaga === "") {
        nemAdottVálaszt += "10.6  ";
      }
      if (this.fogalomtarGyakorisaga === "") {
        nemAdottVálaszt += "10.7  ";
      }
      if (this.visszajelzesGyakorisaga === "") {
        nemAdottVálaszt += "10.8  ";
      }
      if (this.valasztasGyakorisaga === "") {
        nemAdottVálaszt += "10.9  ";
      }
      if (this.adatbazisGyakorisaga === "") {
        nemAdottVálaszt += "10.10  ";
      }
      if (this.wikiGyakorisaga === "") {
        nemAdottVálaszt += "10.11  ";
      }
      if (this.hasznosNappali === "") {
        nemAdottVálaszt += "12.  ";
      }
      if (this.hasznosEsti === "") {
        nemAdottVálaszt += "12.  ";
      }
      if (this.lmsElegedett === "") {
        nemAdottVálaszt += "13.";
      }
      if (nemAdottVálaszt.length > 0) {
        // tslint:disable-next-line:max-line-length
        alert(
          `A kérdőív adatainak mentéséhez a következő kérdésekre a választ legyen szíves megadni: \r${nemAdottVálaszt}`
        );
        return;
      }
    }

    // Firestore objektum összeállítása
    const obj = {} as any;
    obj.K00_createdAt = new Date();
    obj.K01_ferfi = this.ferfi;
    obj.K02_evfolyam = this.evfolyam;
    obj.K03_megyek = this.megyek;
    obj.K04_tanargyakTipusa = this.tantargyakTipusa;
    obj.K05_kepzesiForma = this.kepzesiForma;
    obj.K06_lmsYorN = this.lmsYorN;
    if (this.lmsYorN) {
      obj.K07_lmsHasznal = this.lmsHasznal;
      obj.K08_lsmHanyEve = this.lsmHanyEve;
      obj.K09_lsmHasznalatGyakorisaga = this.lsmHasznalatGyakorisaga;
      obj.K10a_tesztGyakorisaga = this.tesztGyakorisaga;
      obj.K10b_feladatGyakorisaga = this.feladatGyakorisaga;
      obj.K10c_forumGyakorisaga = this.forumGyakorisaga;
      obj.K10d_tananyagGyakorisaga = this.tananyagGyakorisaga;
      obj.K10e_oldalGyakorisaga = this.oldalGyakorisaga;
      obj.K10f_urlGyakorisaga = this.urlGyakorisaga;
      obj.K10g_fogalomtarGyakorisaga = this.fogalomtarGyakorisaga;
      obj.K10h_visszajelzesGyakorisaga = this.visszajelzesGyakorisaga;
      obj.K10i_valasztasGyakorisaga = this.valasztasGyakorisaga;
      obj.K10j_adatbazisGyakorisaga = this.adatbazisGyakorisaga;
      obj.K10k_wikiGyakorisaga = this.wikiGyakorisaga;
      obj.K11_hasznosNappali = this.hasznosNappali;
      obj.K12_hasznosEsti = this.hasznosEsti;
      obj.K13_lmsElegedett = this.lmsElegedett;
    }

    db.collection("valaszok3") // Elem feltöltése az adatbázisba
      .add(obj)
      .then(docRef => {
        alert(
          `Adatok mentése sikeres!\nRekord azonosítója: ${
            docRef.id
          }\nKöszönöm a kérdőív kitöltését!`
        );
      })
      .catch(error => {
        alert(`Hiba az adatok mentésekor: ${error}`);
        return;
      });
    this.megyek = "";
    this.evfolyam = "";
    this.tantargyakTipusa = [];
    this.kepzesiForma = [];
    this.lmsYorN = false;
    this.lmsHasznal = [];
    this.lsmHanyEve = "";
    this.lsmHasznalatGyakorisaga = "";
    this.tesztGyakorisaga = "";
    this.feladatGyakorisaga = "";
    this.forumGyakorisaga = "";
    this.tananyagGyakorisaga = "";
    this.oldalGyakorisaga = "";
    this.urlGyakorisaga = "";
    this.fogalomtarGyakorisaga = "";
    this.visszajelzesGyakorisaga = "";
    this.valasztasGyakorisaga = "";
    this.adatbazisGyakorisaga = "";
    this.wikiGyakorisaga = "";
    this.hasznosNappali = "";
    this.hasznosEsti = "";
    this.lmsElegedett = "";
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  background-color: #eeeeee;
}
.myLink {
  text-decoration: none;
}
.floatleft {
  float: left;
}

.bordered {
  border: 2px solid #a5a5a5;
  border-radius: 4px;
}

.disabledTitle {
  color: rgba(175, 175, 175, 0.5);
}
</style>
