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
                    <span>5. Hány tanévben használtál már e-learning (LMS) keretrendszert?</span>
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
                    <span>6. Milyen eszközön használod az e-learning (LMS) keretrendszer szolgáltatásait?</span>
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
                    v-model="lmsHasznalatGyakorisaga"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>

            <!-- 8.	A következő e-learning (LMS) szolgáltatásokat ha ismered, akkor mennyire tartod őket hasznosnak? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon large left>mdi-chart-histogram</v-icon>
                    <span>8.	A következő e-learning (LMS) szolgáltatásokat ha ismered, akkor mennyire tartod őket hasznosnak?</span>
                  </div>
                </v-card-title>
              
                <!-- Quiz -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.1 Tesztek tanulói teljesítmény mérésére"
                    outline
                    v-model="tesztHasznos"
                  />
                </v-card-actions>

                <!-- Assignment -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.2 Állományok feltöltése (órai feladatok, házi feladatok)"
                    outline
                    v-model="feladatHasznos"
                  />
                </v-card-actions>

                <!-- Forum -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.3 Fórumok használata"
                    outline
                    v-model="forumHasznos"
                  />
                </v-card-actions>

                <!-- File -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.4 Megosztott tananyagok olvasása / letöltése"
                    outline
                    v-model="tananyagHasznos"
                  />
                </v-card-actions>
                
                <!-- URL -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.5 Megosztott hivatkozások (URL címek) látogatása"
                    outline
                    v-model="urlHasznos"
                  />
                </v-card-actions>
                
                <!-- Glossary -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.6 Beépített fogalomtár használata"
                    outline
                    v-model="fogalomtarHasznos"
                  />
                </v-card-actions>

                <!-- Feedback -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.7 Tanulói visszajelzések készítse a tanóráról"
                    outline
                    v-model="visszajelzesHasznos"
                  />
                </v-card-actions>

                <!-- Choice -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.8 Tanulói választások, szavazások"
                    outline
                    v-model="valasztasHasznos"
                  />
                </v-card-actions>

                <!-- Database -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.9 Adatbázisok létrehozása / kezelése"
                    outline
                    v-model="adatbazisHasznos"
                  />
                </v-card-actions>

                <!-- Wiki -->
                <v-card-actions>
                  <v-select
                    :items="hasznossagLista"
                    suffix
                    clearable
                    label="8.10 Wiki oldalak készítése"
                    outline
                    v-model="wikiHasznos"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>

            <!-- 9. Mennyire tartod hasznosnak az e-learning (LMS) keretrendszer alkalmazását a nappali képzésben? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-weather-sunny</v-icon>
                    <span>9. Mennyire tartod hasznosnak az e-learning (LMS) keretrendszert a tanulmányaid támogatásához?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="hasznossagLista2"
                    clearable
                    label="Hasznosság"
                    outline
                    v-model="hasznosTanulmanyokhoz"
                  />
                </v-card-actions>
              </v-card>
            </v-flex>

            <!-- 10. Általánosságban mennyire vagy elégedett az iskolában használt LMS keretrendszerrel? -->
            <v-flex xs12 sm12 md12 lg12 xl12>
              <v-card class="mx-auto my-2" color="lightblue" max-width="600" elevation="18" dark>
                <v-img></v-img>
                <v-card-title primary-title>
                  <div>
                    <v-icon class="floatleft" large left>mdi-emoticon-happy</v-icon>
                    <span>10. Általánosságban mennyire vagy elégedett az iskolában használt LMS keretrendszerrel?</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-select
                    dark
                    :items="elegedettsegiLista"
                    clearable
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
    "13-14.",
    "Felnőttképzés"
  ];

  private tantargyakTipusaLista: string[] = [
    "Reál tantárgyak (pl.: matematika, kémia, informatika)",
    "Humán tantárgyak (pl. irodalom, történelem)",
    "Szakmai tantárgyak (pl. hálózati ismeretek, programozás)"
  ];

  private evekLista: string[] = ["1", "2", "3", "4", "5-"];

  private eszkozLista: string[] = [
    "Asztal számítógép",
    "Laptop",
    "Tablet",
    "Mobiltelefon"
  ];

  private kepzesiFormaLista: string[] = ["Nappali oktatás", "Esti oktatás"];


  private gyakorisagLista: string[] = [
    "Hetente több, mint 1 alkalommal",
    "Hetente 1 alkalommal",
    "Havonta 1-2 alkalommal",
    "2-3 havonta",
    "Szinte alig"
  ];

  private hasznossagLista: string[] = [
    "Nem ismerem, nincs véleményem",
    "Nagyon hasznos",
    "Hasznos",
    "Semleges",
    "Kevésbé hasznos",
    "Nem hasznos"
  ];

  private hasznossagLista2: string[] = [
    "Nagyon hasznos",
    "Hasznos",
    "Semleges",
    "Kevésbé hasznos",
    "Nem hasznos"
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
  private lmsHanyEve: string = ""; // 5
  private lmsEszkoz: string[] = []; // 6
  private lmsHasznalatGyakorisaga: string = ""; // 7
  private tesztHasznos: string = ""; // 8.1
  private feladatHasznos: string = ""; // 8.2
  private forumHasznos: string = ""; // 8.3
  private tananyagHasznos: string = ""; // 8.4
  private urlHasznos: string = ""; // 8.5
  private fogalomtarHasznos: string = ""; // 8.6;
  private visszajelzesHasznos: string = "";  // 8.7;
  private valasztasHasznos: string = ""; // 8.8;
  private adatbazisHasznos: string = ""; // 8.9;
  private wikiHasznos: string = ""; // 8.10
  private hasznosTanulmanyokhoz: string = ""; // 9.
  private lmsElegedett: string = ""; // 10.

  // Új elem hozzáadása az adatbázishoz
  private add(): void {
    let nemAdottVálaszt: string = "";
    if (this.evfolyam === "") {
      nemAdottVálaszt += "2.  ";
    }
    if (this.megyek === "") {
      nemAdottVálaszt += "3.  ";
    }
    if (this.tantargyakTipusa.length === 0) {
      nemAdottVálaszt += "4.  ";
    }
    if (this.lmsHanyEve === "") {
      nemAdottVálaszt += "5.  ";
    }
    if (this.lmsEszkoz.length === 0) {
      nemAdottVálaszt += "6.  ";
    }
    if (this.lmsHasznalatGyakorisaga === "") {
      nemAdottVálaszt += "7.  ";
    }
    if (this.tesztHasznos === "") {
      nemAdottVálaszt += "8.1  ";
    }
    if (this.feladatHasznos === "") {
      nemAdottVálaszt += "8.2  ";
    }
    if (this.forumHasznos === "") {
      nemAdottVálaszt += "8.3  ";
    }
    if (this.tananyagHasznos === "") {
      nemAdottVálaszt += "8.4  ";
    }
    if (this.urlHasznos === "") {
      nemAdottVálaszt += "8.5  ";
    }
    if (this.fogalomtarHasznos === "") {
      nemAdottVálaszt += "8.6  ";
    }
    if (this.visszajelzesHasznos === "") {
      nemAdottVálaszt += "8.7  ";
    }
    if (this.valasztasHasznos === "") {
      nemAdottVálaszt += "8.8  ";
    }
    if (this.adatbazisHasznos === "") {
      nemAdottVálaszt += "8.9  ";
    }
    if (this.wikiHasznos === "") {
      nemAdottVálaszt += "8.10  ";
    }
    if (this.hasznosTanulmanyokhoz === "") {
      nemAdottVálaszt += "9.  ";
    }
    if (this.lmsElegedett === "") {
      nemAdottVálaszt += "10.  ";
    }
    if (nemAdottVálaszt.length > 0) {
      // tslint:disable-next-line:max-line-length
      alert(
        `A kérdőív adatainak mentéséhez a következő kérdésekre a választ legyél kedves megadni: \r${nemAdottVálaszt}`
      );
      return;
    }

    // Firestore objektum összeállítása
    const obj = {} as any;
    obj.K00_createdAt = new Date();
    obj.K01_ferfi = this.ferfi;
    obj.K02_evfolyam = this.evfolyam;
    obj.K03_megyek = this.megyek;
    obj.K04_tantargyakTipusa = this.tantargyakTipusa;
    obj.K05_lmsHanyEve = this.lmsHanyEve;
    obj.K06_lmsEszkoz = this.lmsEszkoz;
    obj.K07_lmsHasznalatGyakorisaga = this.lmsHasznalatGyakorisaga;
    obj.K8a_tesztHasznos = this.tesztHasznos;
    obj.K8b_feladatHasznos = this.feladatHasznos;
    obj.K8c_forumHasznos = this.forumHasznos;
    obj.K8d_tananyagHasznos = this.tananyagHasznos;
    obj.K8e_urlHasznos = this.urlHasznos;
    obj.K8f_fogalomtarHasznos = this.fogalomtarHasznos;
    obj.K8g_visszajelzesHasznos = this.visszajelzesHasznos;
    obj.K8h_valasztasHasznos = this.valasztasHasznos;
    obj.K8i_adatbazisHasznos = this.adatbazisHasznos;
    obj.K8j_wikiHasznos = this.wikiHasznos;
    obj.K9_hasznosTanulmanyokhoz = this.hasznosTanulmanyokhoz;
    obj.K10_lmsElegedett = this.lmsElegedett;

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

    this.ferfi = false;
    this.megyek = "";
    this.evfolyam = "";
    this.tantargyakTipusa = [];
    this.lmsHanyEve = "";
    this.lmsEszkoz = [];
    this.lmsHasznalatGyakorisaga = "";
    this.tesztHasznos = "";
    this.feladatHasznos = "";
    this.forumHasznos = "";
    this.tananyagHasznos = "";
    this.urlHasznos = "";
    this.fogalomtarHasznos = "";
    this.visszajelzesHasznos = "";
    this.valasztasHasznos = "";
    this.adatbazisHasznos = "";
    this.wikiHasznos = "";
    this.hasznosTanulmanyokhoz = "";
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
