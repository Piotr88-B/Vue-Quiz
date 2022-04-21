<template>
<div class="container__app">
  <div class="container__quiz">
    <div class="quiz__header">
      <h1>PYTANIE: {{b}}/{{questions.length}}</h1>
      <div class="box_score">
        <p>
          dobre odpowiedzi: {{score}}
        </p>
        <p>
          złe odpowiedzi: {{inscore}}
        </p>
      </div>
    </div>
    <div class="main__quiz" v-for="(element, index) in questions.slice(a,b)" :key="index">
      <div class="box__question">
        <h3>{{element.question}}</h3>
   
           <img :src="`${element.image}`"  />
        
    
      </div>
      <div class="box__sugestion">
        <ul>
          <li v-for="(item, index) in element.answers" :key="index" :class="select ? chack(item) :'' " @click="selectResponse(item)">{{item.text}}<div class="fas fa-check" v-if="select ? item.correct: ''"></div><div class="fas fa-times" v-if="select ? !item.correct: ''"></div></li>
        </ul>
      </div>
    </div>
    <div class="quiz__footer">
      <div class="box__buttom">

        <button @click="skipFast">20>></button>
        <button @click="nextQuestion">Next</button>
        <button @click="restartQuiz">RESET</button>

      </div>

    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      questions: [{
          question: '1. Urządzenie techniczne objęte dozorem technicznym może być eksploatowane na podstawie',
          image: require('@/assets/blank.png'),
          answers: [{
              text: '• Zezwolenia ustnego lub pisemnego wydanego przez upoważnionego konserwatora',
              correct: false
            },
            {
              text: '• Ważnej decyzji zezwalającej na eksploatacje wydanej przez organ właściwej jednostki dozoru technicznego ',
              correct: true
            },
            {
              text: '• Oznaczenia CE zamieszczonego na urządzeniu',
              correct: false
            },
            {
              text: '• Deklaracji zgodności wystawionej przez wytwórcę  ',
              correct: false
            },
          ]
        },
        {
          question: '2.Które z wymienionych czynności nie należą do zakresu obowiązków obsługującego UTB',
    image: require('@/assets/blank.png'),
          answers: [{
            text: '•	Wykonywanie niewielkich napraw urządzenia w ramach posiadanego wykształcenia i umiejętności',
            correct: true
          }, {
            text: '• Przestrzeganie instrukcji eksploatacji w zakresie obsługi UTB',
            correct: false
          }, {
            text: '• Zapoznanie się z planem pracy i wielkością przenoszonych ładunków',
            correct: false
          }, {
            text: '• Zszystkie odpowiedzi są poprawne ',
            correct: false
          }]
        },

        {
          question: '3.Terminy przeglądów konserwacyjnych urządzeń technicznych',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	są zawarte w instrukcji eksploatacji urządzenia',
            correct: true
          }, {
            text: '•	określa konserwator urządzenia',
            correct: false
          }, {
            text: '•	określa w protokole inspektor wykonujący badanie',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        },
        {
          question: '4.Dozorem technicznym nazywamy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	określone ustawa działania zmierzające do zapewnienia bezpiecznego funkcjonowania urządzeń technicznych i urządzeń do odzyskiwania par paliwa oraz działania zmierzające do zapewnienia bezpieczeństwa publicznego w tych obszarach',
            correct: true
          }, {
            text: '•	instytucje kontrolujące stan techniczny urządzeń',
            correct: false
          }, {
            text: '•	Urząd Dozoru Technicznego',
            correct: false
          }, {
            text: '•	UDT, WDT, TDT',
            correct: false
          }]
        }, {
          question: '5.Dozór techniczny nad urządzeniami technicznymi wykonuje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	Urząd Dozoru Technicznego oraz specjalistyczne jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	Urząd Dozoru Technicznego oraz upoważnione przez UDT organizacje',
            correct: false
          }, {
            text: '•	Urząd Dozoru Technicznego i zagraniczne jednostki dozoru technicznego',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '6.Zmiana parametrów technicznych lub zmiana konstrukcji urządzenia technicznego traktowana jest jako',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	modernizacja urządzenia technicznego',
            correct: true
          }, {
            text: '•	naprawa urządzenia technicznego',
            correct: false
          }, {
            text: '•	usuwanie usterek i innych nieprawidłowości urządzenia technicznego',
            correct: false
          }, {
            text: '•	wytworzenie nowego urządzenia',
            correct: false
          }]
        }, {
          question: '7.Uzgodniona naprawę lub modernizacje urządzeń technicznych maże wykonać',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	naprawiający lub modernizujący, który posiada uprawnienie wydane przez organ właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	konserwator posiadający odpowiednie doświadczenie w zakresie napraw lub modernizacji',
            correct: false
          }, {
            text: '•	eksploatujący urządzenie techniczne posiadający odpowiednie doświadczenie w zakresie napraw lub modernizacji',
            correct: false
          }, {
            text: '•	w niewielkim zakresie kompetentny operator',
            correct: false
          }]
        }, {
          question: '8.Ustawa o dozorze technicznym określa następujące formy dozoru technicznego',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	całkowita, częściowa, ograniczona',
            correct: false
          }, {
            text: '•	pełna, ograniczona, uproszczona',
            correct: true
          }, {
            text: '•	pełna, cykliczna, sporadyczna',
            correct: false
          }, {
            text: '•	UDT, WDT, TDT',
            correct: false
          }]
        }, {
          question: '9.Decyzje zezwalająca na eksploatacje urządzenia technicznego wydaje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	konserwator po wykonaniu przeglądu z wynikiem pozytywnym',
            correct: false
          }, {
            text: '•	organ właściwej jednostki dozoru technicznego lub eksploatujący urządzenie techniczne z upoważnienia organu właściwej jednostki dozoru technicznego',
            correct: false
          }, {
            text: '•	organ właściwej jednostki dozoru technicznego lub organ administracji publicznej z upoważnienia organu właściwej jednostki dozoru technicznego',
            correct: false
          }, {
            text: '•	organ właściwej jednostki dozoru technicznego',
            correct: true
          }]
        }, {
          question: '10.Obsługujący urządzenie techniczne może podjąć prace gdy',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	urządzenie posiada ważna decyzje zezwalająca na eksploatacje jeżeli wymagają tego odpowiednie przepisy',
            correct: false
          }, {
            text: '•	posiada zaświadczenie kwalifikacyjne odpowiedniej kategorii',
            correct: false
          }, {
            text: '•	urządzenie posiada aktualny pozytywny wynik przeglądu konserwacyjnego',
            correct: false
          }, {
            text: '•	wszystkie powyższe warunki musza być spełnione jednocześnie',
            correct: true
          }]
        },
        {
          question: '11.Obsługujący urządzenie techniczne może podjąć pracę gdy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	urządzenie posiada aktualny wpis w dzienniku konserwacji potwierdzający sprawność urządzenia',
            correct: false
          }, {
            text: '•	przeszedł odpowiednie szkolenie stanowiskowe',
            correct: false
          }, {
            text: '•	urządzenie posiada ważna decyzje zezwalająca na eksploatacje',
            correct: false
          }, {
            text: '•	wszystkie powyższe warunki musza być spełnione jednocześnie',
            correct: true
          }]
        }, {
          question: '12.W przypadku nieprzestrzegania przez eksploatującego przepisów o dozorze technicznym eksploatujący',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	otrzymuje pisemne upomnienie',
            correct: false
          }, {
            text: '•	otrzymuje zalecenia pokontrolne',
            correct: false
          }, {
            text: '•	podlega grzywnie lub karze ograniczenia wolności',
            correct: true
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: false
          }]
        }, {
          question: '13.W przypadku stwierdzenia zagrożenia dla życia lub zdrowia ludzkiego oraz mienia i środowiska inspektor',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wydaje decyzje wstrzymująca eksploatacje urządzenia technicznego',
            correct: true
          }, {
            text: '•	wystawia mandat karny',
            correct: false
          }, {
            text: '•	pisemnie poucza eksploatującego',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '14.W przypadku niebezpiecznego uszkodzenia urządzenia technicznego lub nieszczęśliwego wypadku eksploatujący',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	niezwłocznie powiadamia UDT o zaistniałym zdarzeniu',
            correct: true
          }, {
            text: '•	powiadamia producenta urządzenia o przyczynach powstałego zdarzenia',
            correct: false
          }, {
            text: '•	niezwłocznie dokonuje naprawy urządzenia i przekazuje do dalszej eksploatacji',
            correct: false
          }, {
            text: '•	zgłasza urządzenie do wykonania naprawy',
            correct: false
          }]
        }, {
          question: '15.Zaświadczenie kwalifikacyjne do obsługi może zostać cofnięte przez',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	organ właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	eksploatującego urządzenie techniczne',
            correct: false
          }, {
            text: '•	inspektora bhp',
            correct: false
          }, {
            text: '•	Państwowa Inspekcje Pracy',
            correct: false
          }]
        }, {
          question: '16.Urządzenia techniczne nieobjęte dozorem technicznym to',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	żurawie o udźwigu do 3,2 t',
            correct: false
          }, {
            text: '•	wciągniki i wciągarki oraz suwnice',
            correct: false
          }, {
            text: '•	wózki jezdniowe podnośnikowe oraz podesty ruchome',
            correct: false
          }, {
            text: '•	wózki jezdniowe podnośnikowe oraz podesty ruchome',
            correct: true
          }]
        }, {
          question: '17.Urządzenia techniczne objęte dozorem technicznym to',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	przenośniki kabinowe i krzesełkowe',
            correct: false
          }, {
            text: '•	układnice magazynowe oraz urządzenia dla osób niepełnosprawnych',
            correct: false
          }, {
            text: '•	wyciągi towarowe i wyciągi statków',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '18.Niebezpieczne uszkodzenie urządzenia technicznego to',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	każda usterka UTB',
            correct: false
          }, {
            text: '•	nieprzewidziane uszkodzenie, w wyniku którego urządzenie nadaje się do częściowej eksploatacji',
            correct: false
          }, {
            text: '•	nieprzewidziane uszkodzenie, w wyniku którego nadaje się do eksploatacji tylko przy obniżonych parametrachwyciągi towarowe i wyciągi statków',
            correct: false
          }, {
            text: '•	nieprzewidziane uszkodzenie, w wyniku którego urządzenie nie nadaje się do eksploatacji lub jego dalsza eksploatacja stanowi zagrożenie',
            correct: true
          }]
        },
        {
          question: '19.Nieszczęśliwy wypadek to',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	nagłe zdarzenie, które spowodowało obrażenia ciała lub śmierć',
            correct: true
          }, {
            text: '•	nagłe zdarzenie, które spowodowało przerwę w pracy',
            correct: false
          }, {
            text: '•	nagłe zdarzenie, które skutkuje wyłączeniem urządzenia technicznego z eksploatacji',
            correct: false
          }, {
            text: '•	każda usterka UTB spowodowana przyczyna losowa',
            correct: false
          }]
        }, {
          question: '20.Podnoszenie i przenoszenie osób przez urządzenie techniczne przeznaczone wyłącznie do transportu ładunków wymaga',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	uzgodnienia z organem właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	uzgodnienia z przełożonym',
            correct: false
          }, {
            text: '•	uzgodnienia ze służba BHP',
            correct: false
          }, {
            text: '•	jest możliwe przy zachowaniu szczególnej ostrożności i pod nadzorem inspektora',
            correct: false
          }]
        }, {
          question: '21.Odpowiedzialnym za zapewnienie właściwej obsługi i konserwacji urządzenia technicznego jest',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	eksploatujący urządzenie techniczne',
            correct: true
          }, {
            text: '•	organ właściwej jednostki dozoru technicznego',
            correct: false
          }, {
            text: '•	Państwowa Inspekcja Pracy',
            correct: false
          }, {
            text: '•	Państwowa Inspekcja Pracy',
            correct: false
          }]
        },
        {
          question: '22.Wymagane przepisami prawa przeglądy konserwacyjne wykonuje',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	osoba posiadająca zaświadczenie kwalifikacyjne do konserwacji',
            correct: false
          }, {
            text: '•	pracownik autoryzowanego serwisu producenta urządzenia (pod warunkiem posiadania zaświadczeń kwalifikacyjnych do konserwacji)',
            correct: false
          }, {
            text: '•	zakładowe służby utrzymania ruchu',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        },
        {
          question: '23.Dzienni konserwacji urządzenia technicznego prowadzi',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '23.Dzienni konserwacji urządzenia technicznego prowadzi',
            correct: false
          }, {
            text: '•	uprawniony operator',
            correct: false
          }, {
            text: '•	wyznaczony pracownik eksploatującego',
            correct: false
          }, {
            text: '•	konserwator urządzenia technicznego',
            correct: true
          }]
        },
        {
          question: '24.Badania odbiorcze przeprowadza się dla urządzeń technicznych',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w terminach zgodnych z zapisami rozporządzenia w sprawie warunków technicznych dozoru technicznego',
            correct: false
          }, {
            text: '•	przed wydaniem pierwszej decyzji zezwalającej na eksploatacje',
            correct: true
          }, {
            text: '•	po naprawie urządzenia technicznego',
            correct: false
          }, {
            text: '•	po każdej zmianie eksploatującego',
            correct: false
          }]
        }, {
          question: '25.Badania okresowe przeprowadza się dla urządzeń technicznych objętych dozorem',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	ograniczonym',
            correct: false
          }, {
            text: '•	pełnym',
            correct: true
          }, {
            text: '•	pełnym',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '26.Nieobecność konserwującego na badaniu urządzenia technicznego wymaga min.',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wcześniejszego uzgodnienia tego faktu z organem właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	przedstawienia pisemnego usprawiedliwienia nieobecności konserwatora',
            correct: false
          }, {
            text: '•	przedstawienia zwolnienia lekarskiego potwierdzającego niezdolność konserwatora do pracy',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '27.Kandydat na obsługującego urządzenie techniczne musi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	mieć ukończone 18 lat',
            correct: true
          }, {
            text: '•	posiadać przynajmniej wykształcenie zawodowe',
            correct: false
          }, {
            text: '•	posiadać przynajmniej wykształcenie zawodowe',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '28.Obsługujący urządzenie techniczne ma obowiąże przerwać prace gdy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jego stan fizyczny i psychiczny w dniu pracy jest nieodpowiedni',
            correct: false
          }, {
            text: '•	stwierdzi, ze dalsza praca urządzeniem stwarza zagrożenie',
            correct: false
          }, {
            text: '•	urządzenie jest niesprawne',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '29.Terminy przeglądów konserwacyjnych urządzenia mogą być określone',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w instrukcji eksploatacji urządzenia',
            correct: false
          }, {
            text: '•	w ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	w rozporządzeniu określającym warunki techniczne dozoru technicznego',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '30.Terminy badan obrusowych i doraźnych kontrolnych UTB określone są',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	w rozporządzeniu określającym warunki techniczne dozoru technicznego',
            correct: true
          }, {
            text: '•	w dokumentacji konstrukcyjnej urządzenia',
            correct: false
          }, {
            text: '•	w dzienniku konserwacji',
            correct: false
          }]
        }, {
          question: '31.Obowiązkiem obsługującego urządzenie techniczne jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	przestrzeganie instrukcji eksploatacji w zakresie obsługi urządzenia',
            correct: true
          }, {
            text: '•	przestrzeganie instrukcji eksploatacji w zakresie konserwacji urządzenia',
            correct: false
          }, {
            text: '•	wykonywanie napraw urządzenia',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '32.Urządzenie techniczne można eksploatować na podstawie',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	aktualnej naklejki organu właściwej jednostki dozoru technicznego określającej termin kolejnego badania',
            correct: false
          }, {
            text: '•	aktualnego wpisu konserwatora urządzenia w dzienniku konserwacji',
            correct: false
          }, {
            text: '•	ważnej decyzji zezwalającej na eksploatacje wydanej przez organ właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	pozytywnego protokołu z badania okresowego lub odbiorczego',
            correct: false
          }]
        }, {
          question: '33.Po wykonanych czynnościach przy urządzeniu technicznym inspektor sporządza',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	instrukcje eksploatacji urządzenia',
            correct: false
          }, {
            text: '•	decyzje i protokół z wykonanych czynności',
            correct: true
          }, {
            text: '•	deklaracje zgodności CE',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '34.Naprawę i modernizacje urządzenia technicznego wykonuje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	operator w ramach posiadanych umiejętności',
            correct: false
          }, {
            text: '•	konserwat or',
            correct: false
          }, {
            text: '•	zakład uprawniony',
            correct: true
          }, {
            text: '•	eksploatujący',
            correct: false
          }]
        },
        {
          question: '35.Bezpośrednio odpowiedzialnym za bezpieczna eksploatację urządzenia technicznego jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	obsługujący urządzenie',
            correct: true
          }, {
            text: '•	producent urządzenia',
            correct: false
          }, {
            text: '•	zakładowy inspektor BHP',
            correct: false
          }, {
            text: '•	inspektor UDT',
            correct: false
          }]
        }, {
          question: '36.Informacje dotyczące zasad bezpiecznej obsługi urządzenia są zawarte w',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	instrukcji eksploatacji urządzenia',
            correct: true
          }, {
            text: '•	ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	dzienniku konserwacji',
            correct: false
          }, {
            text: '•	protokole z badania wykonanego przez inspektora UDT',
            correct: false
          }]
        }, {
          question: '37.W ramach czynności przed rozpoczęciem pracy Obsługujący',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	sprawdza stan techniczny urządzenia poprzez oględziny',
            correct: false
          }, {
            text: '•	wykonuje próby statyczna i dynamiczna',
            correct: false
          }, {
            text: '•	wykonuje próby ruchowe urządzenia',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '38.Zaświadczenia kwalifikacyjne do obsługi urządzeń technicznych podlegających dozorowi technicznemu wydaje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	firma szkoleniowa po pozytywnym wyniku egzaminu sprawdzającego',
            correct: false
          }, {
            text: '•	inspektor BHP na podstawie zaświadczenia o ukończeniu kursu',
            correct: false
          }, {
            text: '•	pracodawca na podstawie zdanego egzaminu ',
            correct: false
          }, {
            text: '•	organ właściwej jednostki dozoru technicznego',
            correct: true
          }]
        }, {
          question: '39.Przeciążanie UTB w trakcie pracy',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest zabronione',
            correct: true
          }, {
            text: '•	jest dopuszczalne',
            correct: false
          }, {
            text: '•	jest dopuszczalne ale tylko do 125% udźwigu nominalnego',
            correct: false
          }, {
            text: '•	jest dopuszczalne ale tylko do 110% udźwigu nominalnego',
            correct: false
          }]
        }, {
          question: '40.Badania doraźne eksploatacyjne wykonuje się m.in.',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	po każdym usunięciu usterki przez konserwatora',
            correct: false
          }, {
            text: '•	po wymianie cięgien nośnych',
            correct: true
          }, {
            text: '•	raz na rok',
            correct: false
          }, {
            text: '•	po wypadku na urządzeniu',
            correct: false
          }]
        }, {
          question: '41.Obowiązki obsługującego określone są',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w instrukcji eksploatacji urządzenia',
            correct: true
          }, {
            text: '•	w dzienniku konserwacji',
            correct: false
          }, {
            text: '•	w ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '42.Badania okresowe urządzenia technicznego są wykonywane przez',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	konserwatora posiadającego odpowiednie zaświadczenie kwalifikacyjne',
            correct: false
          }, {
            text: '•	inspektora organu właściwej jednostki dozoru technicznego',
            correct: true
          }, {
            text: '•	pracownika serwisu producenta',
            correct: false
          }, {
            text: '•	operatora',
            correct: false
          }]
        }, {
          question: '43.Jednostka dozoru technicznego jest',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	Urząd Dozoru Technicznego',
            correct: false
          }, {
            text: '•	Wojskowy Dozór techniczny',
            correct: false
          }, {
            text: '•	Transportowy dozór Techniczny',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '44.Zaświadczenia kwalifikacyjne uprawniające do obsługi urządzeń technicznych ważne są na terenie',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	Rzeczypospolitej Polskiej',
            correct: true
          }, {
            text: '•	Unii Europejskiej',
            correct: false
          }, {
            text: '•	nie maja określonego obszaru ważności',
            correct: false
          }, {
            text: '•	krajów strefy Schengen',
            correct: false
          }]
        }, {
          question: '45.Obowiązek stosowania środków ochrony indywidualnej przez operatorów urządzeń technicznych wynika z',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	instrukcji eksploatacji producenta',
            correct: false
          }, {
            text: '•	przepisów BHP',
            correct: false
          }, {
            text: '•	przepisów wewnątrzzakładowych',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '46.Zgodnie z rozporządzeniem Rady Ministrów w sprawie rodzajów urządzeń technicznych podlegających dozorowi technicznemu przepisom dozoru technicznego podlegają',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	dźwigi, żurawie, suwnice, wciągarki i wciągniki',
            correct: false
          }, {
            text: '•	wózki jezdniowe podnośnikowe z mechanicznym napędem podnoszenia, podesty ruchome',
            correct: false
          }, {
            text: '•	dźwignice linotorowe, przenośniki kabinowe i krzesełkowe',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '47.Instrukcja eksploatacji może nie zawierać',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	informacji o terminach i zakresie przeglądów konserwacyjnych UTB',
            correct: false
          }, {
            text: '•	podstawowych parametrów i przeznaczenia UTB',
            correct: false
          }, {
            text: '•	terminów badan technicznych wykonywanych przez jednostkę inspekcyjna',
            correct: true
          }, {
            text: '•	informacji o sposobie obsługi urządzenia',
            correct: false
          }]
        }, {
          question: '48.Księga rewizyjna urządzenia musi zawierać',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zbiór protokołów z badan wykonywanych przez jednostkę inspekcyjna',
            correct: true
          }, {
            text: '•	dokument, w którym odnotowywane są przeglądy konserwacyjne',
            correct: false
          }, {
            text: '•	treść aktualnych aktów prawnych',
            correct: false
          }, {
            text: '•	wykaz uprawnionych operatorów',
            correct: false
          }]
        }, {
          question: '49.Decyzja wydana przez UDT',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	nie podlega odwołaniu',
            correct: false
          }, {
            text: '•	może zostać zmieniona przez inspektora PIP',
            correct: false
          }, {
            text: '•	podlega możliwości odwołania się przez eksploatującego',
            correct: true
          }, {
            text: '•	każda odpowiedz jest niepoprawna',
            correct: false
          }]
        }, {
          question: '50.Do egzaminu sprawdzającego kwalifikacje może przystąpić osoba, która',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	złożyła wniosek o sprawdzenie kwalifikacji',
            correct: false
          }, {
            text: '•	ukończyła 18 lat',
            correct: false
          }, {
            text: '•	nie ma przeciwwskazań zdrowotnych do obsługi urządzeń technicznych',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '51.Po zakończonym badaniu technicznym z wynikiem pozytywnym inspektor UDT',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	przedłuża ważność świadectwa kwalifikacji operatora',
            correct: false
          }, {
            text: '•	oznakowuje urządzenie naklejka, która jest zezwoleniem na użytkowanie urządzenia',
            correct: false
          }, {
            text: '•	informuje użytkownika pisemnie w dzienniku konserwacji, ze wyraża zgodę na eksploatacje urządzenia',
            correct: false
          }, {
            text: '•	sporządza protokół z wykonanych czynności i wydaje decyzje administracyjna zezwalająca na eksploatacje',
            correct: true
          }]
        }, {
          question: '52.Zaświadczenia kwalifikacyjne',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	są ważne bezterminowo',
            correct: false
          }, {
            text: '•	są terminowe z okresem ważności uzależnionym od ilości uzyskanych punktów na egzaminie',
            correct: false
          }, {
            text: '•	są terminowe z okresem ważności zgodnym z zapisami rozporządzenia w sprawie trybu sprawdzenia kwalifikacji',
            correct: true
          }, {
            text: '•	są ważne przez okres 15 lat',
            correct: false
          }]
        }, {
          question: '53.Dokonujący przeróbek urządzenia technicznego bez uzgodnienia z organem właściwej jednostki dozoru technicznego',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	podlega karze grzywny lub ograniczenia wolności',
            correct: true
          }, {
            text: '•	podlega ukaraniu mandatem karnym',
            correct: false
          }, {
            text: '•	nie podlega karze',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '54.Kto dopuszcza do eksploatacji urządzenie techniczne bez ważnej decyzji zezwalającej na eksploatację',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	podlega karze grzywny lub ograniczenia wolności',
            correct: true
          }, {
            text: '•	nie podlega karze, jeżeli nie dojdzie do wypadku',
            correct: false
          }, {
            text: '•	podlega wyłącznie karze grzywny',
            correct: false
          }, {
            text: '•	podlega karze więzienia',
            correct: false
          }]
        }, {
          question: '55.Instrukcja eksploatacji to',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zbiór informacji niezbędnych do bezpiecznej eksploatacji urządzenia udostępniany przez producenta',
            correct: true
          }, {
            text: '•	zbiór zaleceń wydawanych przez Urząd Dozoru Technicznego',
            correct: false
          }, {
            text: '•	instrukcja, która musi stworzyć użytkownik urządzenia',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '56.Zaświadczeń kwalifikacyjnych do obsługi nie wymaga się',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jeżeli urządzenie jest obsługiwane przez jego właściciela',
            correct: false
          }, {
            text: '•	jeżeli wszystkie mechanizmy urządzenia maja napęd ręczny',
            correct: true
          }, {
            text: '•	jeśli urządzenie jest wykorzystywane do celów prywatnych, nie zarobkowych',
            correct: false
          }, {
            text: '•	od osób po 60 roku życia',
            correct: false
          }]
        }, {
          question: '57.Osoba posiadająca Zaświadczenia kwalifikacyjne może obsługiwać',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	tylko urządzenia wymienione w zakresie uprawnienia',
            correct: true
          }, {
            text: '•	wszystkie urządzenia podlegające dozorowi technicznemu',
            correct: false
          }, {
            text: '•	inne urządzenia podlegające dozorowi technicznemu za zgoda pracodawcy',
            correct: false
          }, {
            text: '•	wszystkie UTB o udźwigu do 3,2 t',
            correct: false
          }]
        }, {
          question: '58. Obowiązkiem obsługującego urządzenie techniczne jest ',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	odmówić obsługi urządzenia, jeżeli wygasła decyzja zezwalająca na eksploatacje tego urządzenia',
            correct: false
          }, {
            text: '•	zawsze stosować się do poleceń przełożonego nakazujących eksploatacje urządzenia',
            correct: false
          }, {
            text: '•	stosować się do zapisów zawartych w instrukcji eksploatacji',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '59.Zaświadczenie kwalifikacyjne do obsługi urządzeń technicznych są',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	ważne na terenie Unii Europejskiej',
            correct: false
          }, {
            text: '•	ważne z dowodem tożsamości',
            correct: true
          }, {
            text: '•	bezterminowe',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '60.Obsługujący który jest świadkiem wypadku ma obowiązek',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	udzielić pomocy ofierze (lub ofiarom) wypadku',
            correct: false
          }, {
            text: '•	zabezpieczyć miejsce zdarzenia',
            correct: false
          }, {
            text: '•	powiadomić przełożonego',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '61.Obsługującemu nie wolno',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	podnosić ładunków, których masy nie potrafi określić',
            correct: true
          }, {
            text: '•	kontrolować stanu technicznego urządzenia',
            correct: false
          }, {
            text: '•	stosować się do zapisów zawartych w instrukcji eksploatacji',
            correct: false
          }, {
            text: '•	dokonywać oględzin zewnętrznych urządzenia',
            correct: false
          }]
        }, {
          question: '62.Formami dozoru technicznego są',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	dozór pełny, dozór uproszczony, dozór ograniczony',
            correct: true
          }, {
            text: '•	badanie odbiorcze, badanie okresowe i badanie doraźne',
            correct: false
          }, {
            text: '•	UDT, TDT, WDT',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '63.Podnoszenie osób urządzeniami, które zostały zaprojektowane i wykonane wyłącznie do podnoszenia ładunków',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest dopuszczalne, po zapewnieniu odpowiedniego poziomu bezpieczeństwa',
            correct: false
          }, {
            text: '•	jest zabronione',
            correct: false
          }, {
            text: '•	jest dopuszczalne, po uzgodnieniu z organem właściwej jednostki dozoru technicznego szczegółowych warunków eksploatacji',
            correct: true
          }, {
            text: '•	jest dopuszczalne jednorazowo na pisemne polecenie przełożonego',
            correct: false
          }]
        }, {
          question: 'jest dopuszczalne jednorazowo na pisemne polecenie przełożonego',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest dopuszczalne, pod warunkiem opracowania przez eksploatującego szczegółowych warunków eksploatacji, opisujących czynności organizacyjno-techniczne minimalizujące ryzyko',
            correct: true
          }, {
            text: '•	jest zawsze dopuszczalne jeżeli masa ładunku nie przekracza sumy udźwigów wykorzystywanych urządzeń',
            correct: false
          }, {
            text: '•	jest dopuszczalne jeżeli masa ładunku nie przekracza połowy udźwigu każdego z wykorzystanych urządzeń',
            correct: false
          }, {
            text: '•	nie jest nigdy dopuszczalna',
            correct: false
          }]
        }, {
          question: '65.Przebywanie osób pod ładunkiem przenoszonym jest',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zawsze niedozwolone',
            correct: true
          }, {
            text: '•	dozwolone dla osób kontrolującej spód ładunku;',
            correct: false
          }, {
            text: '•	dozwolone jeżeli współczynnik bezpieczeństwa cięgien wynosi nie mniej niż 5',
            correct: false
          }, {
            text: '•	dozwolone jeżeli współczynnik bezpieczeństwa cięgien wynosi nie mniej niż 7',
            correct: false
          }]
        }, {
          question: '66.Przenoszenia ładunków nad osobami jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	dozwolone pod warunkiem uzyskania pisemnego zezwolenia od osoby kierującej transportem',
            correct: false
          }, {
            text: '•	dozwolone, po zapewnieniu współczynników bezpieczeństwa dla cięgien i urządzeń chwytnych większych niż 10',
            correct: false
          }, {
            text: '•	dozwolone pod warunkiem powiadomienia osób i wyposażeniu ich w środki ochrony indywidualnej',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        }, {
          question: '67.Zaświadczenia kwalifikacyjne do obsługi urządzeń technicznych podlegających dozorowi technicznemu wydaje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	właściciel urządzenia',
            correct: false
          }, {
            text: '•	UDT, TDT, WDT',
            correct: true
          }, {
            text: '•	PIP',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '68.Komisja egzaminacyjna powiadamia osobę zainteresowana o wyniku egzaminu',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w ciągu 7 dni po egzaminie w formie pisemnej',
            correct: false
          }, {
            text: '•	bezpośrednio po egzaminie',
            correct: true
          }, {
            text: '•	w ciągu 14 dni po egzaminie w formie elektronicznej',
            correct: false
          }, {
            text: '•	listem poleconym lub poczta elektroniczna po upływie 30 dni roboczych od daty egzaminu',
            correct: false
          }]
        }, {
          question: '69.Dziennik konserwacji powinien być prowadzony',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	tylko w formie papierowej',
            correct: false
          }, {
            text: '•	w formie elektronicznej lub papierowej',
            correct: true
          }, {
            text: '•	tylko w formie elektronicznej',
            correct: false
          }, {
            text: '•	przez obsługującego',
            correct: false
          }]
        }, {
          question: '70.Instrukcja stanowiskowa',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest zawsze dostarczana wraz z instrukcja obsługi przez producenta urządzenia',
            correct: false
          }, {
            text: '•	stanowi niepisany zbiór zwyczajów przyjętych w zakładzie pracy',
            correct: false
          }, {
            text: '•	jest wydawana przez pracodawcę i zawiera szczegółowe wskazówki dotyczące bhp na stanowisku pracy',
            correct: true
          }, {
            text: '•	nie dotyczy operatorów urządzeń mobilnych',
            correct: false
          }]
        }, {
          question: '71.Po upływie terminu ważności zaświadczenia kwalifikacyjnego do obsługi urządzenia Obsługujący',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	może obsługiwać UTB o ile kontynuuje prace u tego samego pracodawcy',
            correct: false
          }, {
            text: '•	może obsługiwać UTB o ile złoży wniosek o wydanie kolejnego zaświadczenia',
            correct: false
          }, {
            text: '•	może obsługiwać UTB dopiero po uzyskaniu nowego zaświadczenia kwalifikacyjnego',
            correct: true
          }, {
            text: '•	składa wniosek o przedłużenie terminu ważności zaświadczenia kwalifikacyjnego',
            correct: false
          }]
        }, {
          question: '72.Przedłużenie ważności Zaświadczenie kwalifikacyjnego następuje',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	na pisemny wniosek obsługującego',
            correct: true
          }, {
            text: '•	automatycznie po upływie terminu ważności zaświadczenia',
            correct: false
          }, {
            text: '•	na pisemne zgłoszenie pracodawcy obsługującego',
            correct: false
          }, {
            text: '•	po wcześniejszym zgłoszeniu telefonicznym',
            correct: false
          }]
        }, {
          question: '73.Udźwig UTB to parametr urządzenia Bezpośrednio związany z',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	maksymalna wysokością podnoszonego ładunku',
            correct: false
          }, {
            text: '•	maksymalna objętością podnoszonego ładunku',
            correct: false
          }, {
            text: '•	maksymalna masa podnoszonego ładunku',
            correct: true
          }, {
            text: '•	iloczynem masy i objętości podnoszonego ładunku',
            correct: false
          }]
        }, {
          question: '74.Masą netto 1000 l wody wynosi od',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	800 kg',
            correct: false
          }, {
            text: '•	900 kg',
            correct: false
          }, {
            text: '•	1000 kg',
            correct: true
          }, {
            text: '•	1100 kg',
            correct: false
          }]
        }, {
          question: '75.Masą ładunku składającego się z 40 opakowań po 25 kg każdy wynosi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	800 kg',
            correct: false
          }, {
            text: '•	1000 kg',
            correct: true
          }, {
            text: '•	1100 kg',
            correct: false
          }, {
            text: '•	900 kg',
            correct: false
          }]
        }, {
          question: '76.Masą 60 kartonów po 20 kg każdy wynosi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	800 kg',
            correct: false
          }, {
            text: '•	1000 kg',
            correct: false

          }, {
            text: '•	1100 kg',
            correct: false
          }, {
            text: '•	1200 kg',
            correct: true
          }]
        }, {
          question: '77.Masę podnoszonego ładunku można określić na podstawie',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zawieszki zbiorczej znajdującej się na transportowanym ładunku',
            correct: false
          }, {
            text: '•	przeliczając uwzględniając ciężar właściwy i objętość',
            correct: false
          }, {
            text: '•	dokumentacji przewozowej i magazynowej',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '78.Informacja dotycząca udźwigu urządzenia może być zawarta',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w instrukcji eksploatacji',
            correct: false
          }, {
            text: '•	na tabliczce znamionowej',
            correct: false
          }, {
            text: '•	na urządzeniu technicznym',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '79.Prawidłowe określenie jednostki udźwigu to',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	kg',
            correct: true
          }, {
            text: '•	Pa',
            correct: false
          }, {
            text: '•	mth',
            correct: false
          }, {
            text: '•	mm',
            correct: false
          }]
        }, {
          question: '80.Które z elementów nie wchodzą w skład układu hydraulicznego wózka jezdniowego podnośnikowego?',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pompa, zamek hydrauliczny, filtr oleju',
            correct: false
          }, {
            text: '•	rozrusznik, potencjometr, silnik elektryczny',
            correct: true
          }, {
            text: '•	manometr, zawór zwrotny, odpowietrznik',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są nieprawidłowe',
            correct: false
          }]
        }, {
          question: '81.Zamek hydrauliczny zapewnia ochronę przed',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	nadmiernym wzrostem ciśnienia w układzie hydraulicznym',
            correct: false
          }, {
            text: '•	skutkami pęknięcia przewodu hydraulicznego',
            correct: true
          }, {
            text: '•	nieautoryzowanym uruchomieniem urządzenia',
            correct: false
          }, {
            text: '•	dzieleniem strumienia na poszczególne obwody układu hydraulicznego',
            correct: false
          }]
        }, {
          question: '82.Elementem przekształcającym ciśnienie oleju hydraulicznego w ruch mechaniczny jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pompa tłoczkowa',
            correct: false
          }, {
            text: '•	siłownik hydrauliczny',
            correct: true
          }, {
            text: '•	rozdzielacz hydrauliczny',
            correct: false
          }, {
            text: '•	zawór przelewowy',
            correct: false
          }]
        }, {
          question: '83.Elementem wytwarzającym ciśnienie w układzie hydraulicznym wózka jezdniowego podnośnikowego jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pompa tłoczkowa',
            correct: false
          }, {
            text: '•	silnik hydrauliczny',
            correct: true
          }, {
            text: '•	kompresor',
            correct: false
          }, {
            text: '•	sprężarka',
            correct: false
          }]
        }, {
          question: '84.Zawór przelewowy instalowany w układzie hydraulicznym wózków jezdniowych podnośnikowych ma za zadanie',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zasilanie układu hydraulicznego',
            correct: false
          }, {
            text: '•	utrzymanie stałego ciśnienia w układzie hydraulicznym',
            correct: true
          }, {
            text: '•	utrzymanie siłownika w stałej pozycji',
            correct: false
          }, {
            text: '•	zabezpieczenie układu podnoszenia przed opadaniem',
            correct: false
          }]
        }, {
          question: '85.Bezpieczny sposób sprawdzenia działania zaworu przelewowego przeprowadza się',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	z ładunkiem nominalnym na wysokości ok 1/3 wysokości podnoszenia',
            correct: false
          }, {
            text: '•	z włączonym silnikiem bez ładunku',
            correct: false
          }, {
            text: '•	wychylając i przytrzymując dźwignie mechanizmu aż do momentu uzyskania przez układ skrajnego położenia',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '86.Rozdzielacz hydrauliczny instalowany jest w układzie w celu',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	dławienia ciśnienia w poszczególnych obwodach',
            correct: false
          }, {
            text: '•	zabezpieczenia układu przed nadmiernym wzrostem ciśnienia',
            correct: false
          }, {
            text: '•	skierowanie przepływu oleju hydraulicznego do poszczególnych obwodów',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są nieprawidłowe',
            correct: false
          }]
        }, {
          question: '87.Elementem wykonawczym w układzie hydraulicznym wózka jezdniowego podnośnikowego jest',
     image: require('@/assets/blank.png'),
          answers: [{
            text: '•	siłownik mechanizmu podnoszenia',
            correct: false
          }, {
            text: '•	silnik hydrauliczny',
            correct: false
          }, {
            text: '•	siłownik mechanizmu przechyłu',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '88.Elementem chroniącym układ hydrauliczny przed nadmiernym wzrostem ciśnienia jest',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zamek hydrauliczny',
            correct: false
          }, {
            text: '•	zawór dławiący',
            correct: false
          }, {
            text: '•	rozdzielacz hydrauliczny',
            correct: false
          }, {
            text: '•	zawór bezpieczeństwa',
            correct: true
          }]
        }, {
          question: '89.Zawór zwrotno-dławiący montowany w układzie podnoszenia wózka jezdniowego podnośnikowego ma na celu',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zmniejszenie ciśnienia oleju',
            correct: false
          }, {
            text: '•	zabezpieczenie pompy hydraulicznej przed uszkodzeniem',
            correct: false
          }, {
            text: '•	spowolnienie prędkości opuszczania podniesionego ładunku, podczas pęknięcia przewodu hydraulicznego',
            correct: true
          }, {
            text: '•	zablokowanie opuszczania siłownika podczas pęknięcia przewodu hydraulicznego',
            correct: false
          }]
        }, {
          question: '90.Zawór bezpieczeństwa w układzie hydraulicznym wózka jezdniowego podnośnikowego',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	utrzymuje nurnik siłownika podnoszenia w stałym położeniu',
            correct: false
          }, {
            text: '•	jest elementem ograniczającym udźwig',
            correct: true
          }, {
            text: '•	zabezpiecza pompę hydrauliczna przed uszkodzeniem',
            correct: false
          }, {
            text: '•	ogranicza prędkość opuszczania podniesionego ładunku, w przypadku pęknięcia węża hydraulicznego',
            correct: false
          }]
        }, {
          question: '91.W przypadku wzrostu ciśnienia nadmiar oleju odprowadzany jest',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	z powrotem do zbiornika oleju',
            correct: true
          }, {
            text: '•	na zewnątrz wózka',
            correct: false
          }, {
            text: '•	do innej sekcji rozdzielacza',
            correct: false
          }, {
            text: '•	do siłownika',
            correct: false
          }]
        }, {
          question: '92.Kryteria i warunki poprawnego wykonania prób układu hydraulicznego określa',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wytwórca urządzenia',
            correct: true
          }, {
            text: '•	konserwator',
            correct: false
          }, {
            text: '•	operator',
            correct: false
          }, {
            text: '•	inspektor UDT',
            correct: false
          }]
        }, {
          question: '93.Akumulatory w elektrycznym wózku podnośnikowym',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	są źródłem zasilania układów',
            correct: false
          }, {
            text: '•	zapewniają stateczność wózka',
            correct: false
          }, {
            text: '•	decydują o prędkości ruchów roboczych',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '94.Parametry podane przez producenta na tabliczce znamionowej akumulatorów to',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	napięcie znamionowe [V]',
            correct: false
          }, {
            text: '•	pojemność [Ah]',
            correct: false
          }, {
            text: '•	masa własna [kg]',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '95.Wyłączni bezpieczeństwa STOP jest',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zabezpieczony przed przypadkowym zadziałaniem',
            correct: false
          }, {
            text: '•	umieszczony blisko operatora',
            correct: false
          }, {
            text: '•	koloru czerwonego',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '96.Wyłącznik bezpieczeństwa STOP',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wyłącza działanie mechanizmów jazdy',
            correct: false
          }, {
            text: '•	wyłącza działanie mechanizmów podnoszenia',
            correct: false
          }, {
            text: '•	uruchamia sygnalizacje ostrzegawcza',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '97.Jakiego rodzaju ogumienie stosowane jest w wózkach jezdniowych podnośnikowych',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pełne',
            correct: false
          }, {
            text: '•	superelastyczne',
            correct: false
          }, {
            text: '•	pneumatyczne',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '98.Kto decyduje o rodzaju i wielkości opon zastosowanych w wózku',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	producent opon',
            correct: false
          }, {
            text: '•	konserwator',
            correct: false
          }, {
            text: '•	inspektor UDT',
            correct: false
          }, {
            text: '•	producent wózka',
            correct: true
          }]
        }, {
          question: '99.Graniczne zużycie opon super elastycznych (w przypadku braku innych wytycznych) to',

        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	minimalna wartość bieżnika 1,6 mm',
            correct: false
          }, {
            text: '•	zmniejszenie grubości opony o 25% lub do wskaźnika wyznaczającego graniczne zużycie',
            correct: true
          }, {
            text: '•	brak bieżnika',
            correct: false
          }, {
            text: '•	minimalna wartość bieżnika 2 mm',
            correct: false
          }]
        }, {
          question: '100.Jaki rodzaj zużycia wyklucza opony pełne z dalszej eksploatacji',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wszelkie przecięcia i rozwarstwienia gumy, uszkodzenia mechaniczne',
            correct: false
          }, {
            text: '•	brak bieżnika',
            correct: false
          }, {
            text: '•	zmniejszenie grubości opony poniżej wskaźnika wyznaczającego graniczne zużycie',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        },
        {
          question: '101.Świecąca się kontrolka ciśnienia oleju może świadczyć o',
          image: require('@/assets/olej.png'),
          answers: [{
            text: '•	niskim poziomie oleju',
            correct: false
          }, {
            text: '•	podwyższonej temperaturze silnika',
            correct: false
          }, {
            text: '•	zbyt niskim ciśnieniu oleju',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '102.Oznaczenie przedstawione na rysunku znajduje się na dźwigni',
          image: require('@/assets/dzwig.png'),
          answers: [{
            text: '•	mechanizmu podnoszenia',
            correct: true
          }, {
            text: '•	mechanizmu przechyłu masztu',
            correct: false
          }, {
            text: '•	mechanizmu przesuwu wideł',
            correct: false
          }, {
            text: '•	mechanizmu przesuwu karetki',
            correct: false
          }]
        }, {
          question: '103.Widząc świecąca się kontrolkę operator',
          image: require('@/assets/operator.png'),
          answers: [{
            text: '•	powinien sprawdzić, czy pasy są prawidłowo zapięte',
            correct: true
          }, {
            text: '•	może kontynuować prace',
            correct: false
          }, {
            text: '•	może kontynuować prace ze zmniejszona prędkością jazdy',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '104.Dźwignia oznaczona poniższym piktogramem po wychyleniu przez operatora do przodu spowoduje',
          image: require('@/assets/pikto1.png'),
          answers: [{
            text: '•	ruch wideł w dół',
            correct: true
          }, {
            text: '•	ruch wideł w górę',
            correct: false
          }, {
            text: '•	przechył masztu "na siebie"',
            correct: false
          }, {
            text: '•	przechył masztu "od siebie"',
            correct: false
          }]
        }, {
          question: '105.Dźwignia oznaczona poniższym piktogramem po wychyleniu przez operatora spowoduje',
          image: require('@/assets/wychylenie.png'),
          answers: [{
            text: '•	ruch wideł w dół',
            correct: false
          }, {
            text: '•	ruch wideł w górę',
            correct: false
          }, {
            text: '•	ruch mechanizmu przechyłu masztu',
            correct: true
          }, {
            text: '•	ruch mechanizmu przesuwu karetki',
            correct: false
          }]
        }, {
          question: '106.Wózki jezdniowe podnośnikowe czołowe z fotelem dla operatora musza być wyposażone w',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	hamulec zasadniczy',
            correct: false
          }, {
            text: '•	hamulec postojowy',
            correct: false
          }, {
            text: '•	mechanizm ryglujący koła jezdne',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '107.Hamowanie jazdy wózka prowadzonego może być realizowane przez',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pedał hamulca nożnego',
            correct: false
          }, {
            text: '•	zwolnienie nacisku na dźwignie sterująca jazdę wózka',
            correct: false
          }, {
            text: '•	wychylenie dyszla prowadzącego w skrajne górne i dolne położenie',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '108.W skład układu mechanizmu podnoszenia wchodzi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	siłowniki układu podnoszenia',
            correct: false
          }, {
            text: '•	łańcuchy nośne',
            correct: false
          }, {
            text: '•	łańcuchy nośne',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '109.Wózki jezdniowe podnośnikowe czołowe z fotelem dla operatora mogą być wyposażone w maszt typu',
     image: require('@/assets/blank.png'),
          answers: [{
            text: '•	duplex',
            correct: false
          }, {
            text: '•	triplex',
            correct: false
          }, {
            text: '•	maszt z wolnym skokiem',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '110.Jakie elementy bezpieczeństwa chronią operatora w przypadku utraty stateczności wózka podnośnikowego czołowego?',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	łącznik STOP',
            correct: false
          }, {
            text: '•	kabina wózka, pas bezpieczeństwa',
            correct: true
          }, {
            text: '•	podpory',
            correct: false
          }, {
            text: '•	przeciwwaga',
            correct: false
          }]
        }, {
          question: '111.Jakie elementy maja wpływ na stateczność wózka podnośnikowego czołowego ?',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	kabina wózka, pas bezpieczeństwa',
            correct: false
          }, {
            text: '•	łącznik STOP',
            correct: false
          }, {
            text: '•	stan zużycia opon',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '112.Do zasilania wózków podnośnikowych spalinowych stosowane są butle gazowe',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	z kołnierzem',
            correct: true
          }, {
            text: '•	koloru czerwonego',
            correct: false
          }, {
            text: '•	wykorzystywane do zasilania kuchenek gazowych',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: false
          }]
        }, {
          question: '113.W wózkach podnośnikowych łańcuch mechanizmu podnoszenia jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	cięgnem nośnym',
            correct: true
          }, {
            text: '•	cięgnem przeciwślizgowym',
            correct: false
          }, {
            text: '•	cięgnem napędowym',
            correct: false
          }, {
            text: '•	żadnym z powyższych',
            correct: false
          }]
        }, {
          question: '114.Oznaczenie na poniższym rysunku przedstawia',
         image: require('@/assets/sprezyna.png'),
          answers: [{
            text: '•	lampkę kontrolna świec żarowych',
            correct: true
          }, {
            text: '•	lampkę kontrolna ładowania',
            correct: false
          }, {
            text: '•	lampkę kontrolna ciśnienia oleju hydraulicznego',
            correct: false
          }, {
            text: '•	lampkę kontrolna oświetlenia',
            correct: false
          }]
        }, {
          question: '115.Oznaczenie na poniższym rysunku przedstawia',
         image: require('@/assets/akumu.png'),
          answers: [{
            text: '•	lampkę sygnalizująca błędne podłączenie biegunów akumulatora (dotyczy tylko wózków akumulatorowych)',
            correct: false
          }, {
            text: '•	lampkę sprawności akumulatora, która dotyczy tylko wózków akumulatorowych',
            correct: false
          }, {
            text: '•	lampkę kontrolna ładowania akumulatora',
            correct: true
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: false
          }]
        }, {
          question: '116.Oznaczenie na poniższym rysunku przedstawia',
          image: require('@/assets/ciecz.png'),
          answers: [{
            text: '•	wskazania ogranicznika udźwigu wózka',
            correct: false
          }, {
            text: '•	lampkę kontrolna temperatury cieczy chłodzącej',
            correct: true
          }, {
            text: '•	lampkę kontrolna poziomu paliwa',
            correct: false
          }, {
            text: '•	lampkę kontrolna stopnia naładowania akumulatora',
            correct: false
          }]
        }, {
          question: '117.Oznaczenie na poniższym rysunku przedstawia',
          image: require('@/assets/wykrzyknik.png'),
          answers: [{
            text: '•	lampkę kontrolna - włączenia hamulca postojowego',
            correct: true
          }, {
            text: '•	lampkę kontrolna - awaria silnika',
            correct: false
          }, {
            text: '•	lampkę kontrolna – przeciążenie',
            correct: false
          }, {
            text: '•	lampkę kontrolna - nadmierna prędkość obrotowa silnika',
            correct: false
          }]
        }, {
          question: '118.Zapalona lub migająca lampka kontrolna',
          image: require('@/assets/klucz.png'),
          answers: [{
            text: '•	oznacza przekroczenie okresu serwisowego lub awarie urządzenia',
            correct: true
          }, {
            text: '•	oznacza konieczność regulacji naciągu cięgien nośnych',
            correct: false
          }, {
            text: '•	powinna być zapalona podczas pracy silnika',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są nieprawidłowe',
            correct: false
          }]
        }, {
          question: '119.Pracując wózkiem z osprzętem wymiennym operator powinien',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	przestrzegać zapisów instrukcji eksploatacji wózka oraz instrukcji osprzętu wymiennego',
            correct: false
          }, {
            text: '•	przestrzegać przepisów zakładowych',
            correct: false
          }, {
            text: '•	stosować się do właściwego diagramu udźwigu',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '120.Osprzęt wymienny może być zainstalowany do wózka przez',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	konserwatora wózków jezdniowych',
            correct: false
          }, {
            text: '•	operatora wózków jezdniowych',
            correct: false
          }, {
            text: '•	producenta osprzętu wymiennego',
            correct: false
          }, {
            text: '•	producenta osprzętu wymiennego',
            correct: true
          }]
        }, {
          question: '121.Jaki wpływ na udźwig wózka ma zamontowany dodatkowy osprzęt wymienny',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zwiększa udźwig wózka',
            correct: false
          }, {
            text: '•	zmniejsza udźwig wózka',
            correct: true
          }, {
            text: '•	nie ma wpływu',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '122.Po montażu osprzętu wymiennego przewidzianego przez wytwórcę wózka',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	urządzenie należy zgłosić do badania w UDT',
            correct: false
          }, {
            text: '•	urządzenie można eksploatować bez dodatkowych badan w UDT',
            correct: true
          }, {
            text: '•	operator wykonuje próby z przeciążeniem',
            correct: false
          }, {
            text: '•	operator dokonuje wpisu w dzienniku konserwacji',
            correct: false
          }]
        }, {
          question: '123.Dźwignia oznaczona poniższym piktogramem, po wychyleniu przez operatora powoduje',
        image: require('@/assets/pd.png'),
          answers: [{
            text: '•	uruchomienie mechanizmu podnoszenia',
            correct: false
          }, {
            text: '•	uruchomienie mechanizmu przechyłu',
            correct: false
          }, {
            text: '•	uruchomienie mechanizmu przesuwu bocznego',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są nieprawidłowe',
            correct: false
          }]
        }, {
          question: '124.Praca wózkiem z zamontowanymi przedłużkami do wideł jest dozwolona w przypadku gdy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wytwórca nie zabronił takiej pracy',
            correct: false
          }, {
            text: '•	urządzenie jest wyposażone w stosowny diagram udźwigu',
            correct: false
          }, {
            text: '•	montaż przedłużek został wykonany zgodnie z zaleceniami wytwórcy',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '125.Zabezpieczenie elektryczne montowane na zakończeniu dyszla wózka jezdniowego prowadzonego to',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	łącznik STOP',
            correct: false
          }, {
            text: '•	łącznik brzuszny',
            correct: true
          }, {
            text: '•	kontakt zluzowania łańcucha nośnego',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '126.Który z elementów wyposażenia zabezpiecza przed uruchomieniem urządzenia przez osoby niepowołane?',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	łącznik STOP',
            correct: false
          }, {
            text: '•	stacyjka',
            correct: false
          }, {
            text: '•	klawiatura kodów dostępu',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '127.Cecha 1500 x 500 znajdująca się na widle nośnej oznacza',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	maksymalny udźwig jednej widły wynoszący 1,5 t w odległości 500 mm od czoła widły',
            correct: true
          }, {
            text: '•	maksymalny udźwig pary wideł wynoszący 1,5 t w odległości 500 mm od czoła wideł',
            correct: false
          }, {
            text: '•	wymiary zewnętrzne widły nośnej',
            correct: false
          }, {
            text: '•	symbol kontroli jakości',
            correct: false
          }]
        }, {
          question: '128.Maksymalny ładunek jaki można podnieść na parze wideł oznaczonych 2500 x 500 każda wynosi',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	0,5 t',
            correct: false
          }, {
            text: '•	2,5 t',
            correct: false
          }, {
            text: '•	5,0 t',
            correct: true
          }, {
            text: '•	12,0 t',
            correct: false
          }]
        }, {
          question: '129.Praca wózkiem jezdniowym podnośnikowym ze zbyt niskim poziomem oleju w układzie hydraulicznym może objawiać się',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	„skokowym", przerywanym ruchem siłownika do góry',
            correct: false
          }, {
            text: '•	brakiem realizacji wykonania zadanych ruchów mechanizmu podnoszenia',
            correct: false
          }, {
            text: '•	głośna praca pompy hydraulicznej',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '130."Skokowy" ruch mechanizmu podnoszenia do góry może być spowodowany',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zbyt niskim poziomem oleju w układzie hydraulicznym',
            correct: true
          }, {
            text: '•	nadmierna korozja łańcucha układu podnoszenia',
            correct: false
          }, {
            text: '•	uszkodzona rolka prowadząca masztu',
            correct: false
          }, {
            text: '•	uszkodzonym przewodem hydraulicznym zasilającym siłownik podnoszenia',
            correct: false
          }]
        }, {
          question: '131.Nieszczelność w układzie hydraulicznym wózka jezdniowego podnośnikowego może się objawiać',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wyciekiem zewnętrznym',
            correct: false
          }, {
            text: '•	niekontrolowanym opadaniem ładunku',
            correct: false
          }, {
            text: '•	„skokowym", przerywanym ruchem siłownika do góry',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '132.Gęstość oleju hydraulicznego w temperaturze ujemnej',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	maleje',
            correct: false
          }, {
            text: '•	wzrasta',
            correct: true
          }, {
            text: '•	temperatura nie ma wpływu na gęstość oleju',
            correct: false
          }, {
            text: '•	pozostaje bez zmian',
            correct: false
          }]
        }, {
          question: '133.Stan poziomu oleju w układzie hydraulicznym operator sprawdza',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zawsze przed rozpoczęciem i po zakończeniu pracy',
            correct: true
          }, {
            text: '•	zawsze 1 raz w miesiącu',
            correct: false
          }, {
            text: '•	zgodnie z zaleceniami zawartymi w instrukcji eksploatacji',
            correct: false
          }, {
            text: '•	zgodnie z zaleceniami zawartymi w protokole z badan okresowych',
            correct: false
          }]
        }, {
          question: '134.O ile wytwórca nie określi inaczej, maksymalne odchylenie od pionowego położenia masztu obciążonego ciężarem nominalnym, spowodowane wewnętrznym przeciekiem w układzie wychyłu nie powinno przekroczyć',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	5% w czasie 10 min',
            correct: false
          }, {
            text: '•	5° w czasie 10 min',
            correct: true
          }, {
            text: '•	10° w czasie 10 min',
            correct: false
          }, {
            text: '•	brak ustalonych wytycznych',
            correct: false
          }]
        }, {
          question: '135.O ile wytwórca nie określi inaczej, składowa opadania mechanizmu podnoszenia wózka o udźwigu do 10 t obciążonego ciężarem nominalnym nie powinna przekroczyć',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	100 mm w ciągu pierwszych 10 min',
            correct: true
          }, {
            text: '•	50% długości siłownika w ciągu pierwszych 10 min',
            correct: false
          }, {
            text: '•	200 mm w ciągu pierwszych 10 min',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '136.O ile wytwórca nie określi inaczej, składowa opadania mechanizmu podnoszenia wózka o udźwigu powyżej 10 t obciążonego ciężarem nominalnym nie powinna przekroczyć',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	100 mm w ciągu pierwszych 10 min',
            correct: false
          }, {
            text: '•	50% długości siłownika w ciągu pierwszych 10 min',
            correct: false
          }, {
            text: '•	200 mm w ciągu pierwszych 10 min',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '137.Optymalne obciążenie potrzebne do przeprowadzenia próby szczelności wewnętrznej układu hydraulicznego wynosi',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	50% obciążenia nominalnego',
            correct: false
          }, {
            text: '•	100% obciążenia nominalnego',
            correct: true
          }, {
            text: '•	110% obciążenia nominalnego',
            correct: false
          }, {
            text: '•	125% obciążenia nominalnego',
            correct: false
          }]
        }, {
          question: '138.O ile wytyczne producenta nie stanowią inaczej, minimalna wysokość na jaką należy podnieść ładunek podczas próby szczelności wewnętrznej układu wychyłu masztu wynosi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	100 mm',
            correct: false
          }, {
            text: '•	500 mm',
            correct: false
          }, {
            text: '•	2500 mm',
            correct: true
          }, {
            text: '•	próby nie wykonuje się',
            correct: false
          }]
        }, {
          question: '139.Sprawdzenie w bezpieczny sposób działania zaworu przelewowego należy wykonać',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	z obciążeniem nominalnym',
            correct: false
          }, {
            text: '•	z obciążeniem 50% nominalnego',
            correct: false
          }, {
            text: '•	bez obciążenia',
            correct: true
          }, {
            text: '•	z obciążeniem 125% nominalnego',
            correct: false
          }]
        }, {
          question: '140.Sprawdzenie układu hydraulicznego w wózkach podnośnikowych obejmuje',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	próbę szczelności wewnętrznej',
            correct: false
          }, {
            text: '•	próbę zaworu przelewowego',
            correct: false
          }, {
            text: '•	ocenę szczelności zewnętrznej',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '141.Sprawdzenie poprawności działania dźwigni sterowniczych należy wykonać',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	sprawdzając zgodność realizowanych ruchów z oznaczeniami',
            correct: false
          }, {
            text: '•	bez obciążenia',
            correct: false
          }, {
            text: '•	wychylając dźwignie sterownicze we wszystkie przewidziane przez wytwórcę kierunki',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '142.Zakres przeprowadzonych prób wózków jezdniowych podnośnikowych wyposażonych w hydrauliczny osprzęt dodatkowy obejmuje',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	całe wyposażenia hydrauliczne wózka wraz z osprzętem dodatkowym',
            correct: true
          }, {
            text: '•	osprzęt nie stanowi wyposażenia wózka i nie podlega kontroli przez operatora',
            correct: false
          }, {
            text: '•	próby sprawdzające poprawność działania wykonuje tylko konserwator',
            correct: false
          }, {
            text: '•	próbę z obciążeniem 125%',
            correct: false
          }]
        }, {
          question: '143.Akumulatory kwasowe można ładować',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w każdym pomieszczeniu niezależnie od przeznaczenia',
            correct: false
          }, {
            text: '•	tylko w pomieszczeniu klimatyzowanym',
            correct: false
          }, {
            text: '•	w miejscu specjalnie do tego przeznaczonym',
            correct: true
          }, {
            text: '•	wyłącznie w pomieszczeniach ogrzewanych',
            correct: false
          }]
        }, {
          question: '144.Pomieszczenie, w którym odbywa się ładowanie akumulatorów wózka',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	nie musi posiadać wentylacji, ale musi być ogrzewane',
            correct: false
          }, {
            text: '•	musi być ogrzewane i musi posiadać wentylacje',
            correct: false
          }, {
            text: '•	musi posiadać wentylacje',
            correct: true
          }, {
            text: '•	brak jednoznacznych wytycznych',
            correct: false
          }]
        }, {
          question: '145.Obowiązkiem operatora wózków jezdniowych podnośnikowych jest',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	sprawdzenie stopnia naładowania akumulatora',
            correct: false
          }, {
            text: '•	sprawdzenie poziomu elektrolitu',
            correct: false
          }, {
            text: '•	sprawdzenie poprawności zamocowania akumulatora',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '146.Osoba dokonująca wymiany rozładowanych akumulatorów powinna',
      image: require('@/assets/blank.png'),
          answers: [{
            text: '•	posiadać uprawnienia elektryczne SEP',
            correct: false
          }, {
            text: '•	przestrzegać wytycznych zawartych w instrukcji',
            correct: true
          }, {
            text: '•	posiadać zaświadczenie kwalifikacyjne do konserwacji wózków',
            correct: false
          }, {
            text: '•	posiadać zaświadczenie kwalifikacyjne do obsługi wózków',
            correct: false
          }]
        }, {
          question: '147.Łącznik bezpieczeństwa "STOP" służy do',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	awaryjnego zatrzymania pracy wózka',
            correct: true
          }, {
            text: '•	normalnego zatrzymania pracy silnika',
            correct: false
          }, {
            text: '•	zabezpiecza przed uruchomieniem wózka przez osoby nieuprawnione',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '148.W przypadku stwierdzenia sytuacji niebezpiecznej operator wózka ma obowiązek',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zatrzymać wózek',
            correct: false
          }, {
            text: '•	przerwać prace',
            correct: false
          }, {
            text: '•	opuścić ładunek (pod warunkiem nie zwiększenia zagrożenia)',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '149.Sprawdzenie poprawności działania łącznika bezpieczeństwa STOP należy wykonać',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	tylko podczas przeglądów konserwacyjnych',
            correct: false
          }, {
            text: '•	tylko w ramach przeglądów specjalnych',
            correct: false
          }, {
            text: '•	zawsze przed rozpoczęciem pracy',
            correct: true
          }, {
            text: '•	nie ma konieczności sprawdzania poprawności działania',
            correct: false
          }]
        }, {
          question: '150Graniczne wartości zużycia ogumienia zawiera',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	deklaracja zgodności CE',
            correct: false
          }, {
            text: '•	instrukcja eksploatacji wózka',
            correct: true
          }, {
            text: '•	protokół z badan UDT',
            correct: false
          }, {
            text: '•	dyrektywa maszynowa',
            correct: false
          }]
        }, {
          question: '151.Ciśnienie w oponach powinno być dostosowane do',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zaleceń instrukcji eksploatacji wózka',
            correct: true
          }, {
            text: '•	wyłącznie warunków panujących w miejscu eksploatacji',
            correct: false
          }, {
            text: '•	preferencji operatora',
            correct: false
          }, {
            text: '•	wymagań właściciela terenu',
            correct: false
          }]
        }, {
          question: '152.Nierówne ciśnienie w oponach na jednej osi może spowodować',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	poprawę właściwości jezdnych wózka',
            correct: false
          }, {
            text: '•	zmniejszenie stateczności wózka podczas transportu ładunków',
            correct: true
          }, {
            text: '•	nie ma żadnego wpływu na stateczność wózka',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '153.Wpływ na przyspieszone zużycie opon pneumatycznych ma',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	gwałtowne hamowanie, najeżdżanie na przeszkody z dużą prędkością',
            correct: false
          }, {
            text: '•	jazda ze zbyt niskim ciśnieniem',
            correct: false
          }, {
            text: '•	manewrowanie wózkiem na małej przestrzeni',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '154.Nierównomierne zużycie opon pełnych znajdujących się na wspólnej osi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	poprawia właściwości jezdne wózka',
            correct: false
          }, {
            text: '•	nie ma żadnego wpływu na bezpieczna eksploatacje',
            correct: false
          }, {
            text: '•	może spowodować utratę stateczności wózka',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '155.Ocenę stanu technicznego ogumienia przeprowadza',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	konserwator podczas przeglądów konserwacyjnych',
            correct: false
          }, {
            text: '•	operator w ramach czynności przed rozpoczęciem pracy',
            correct: false
          }, {
            text: '•	inspektor UDT w trakcie wykonywanych czynności',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '156.W przypadku stwierdzenia uszkodzeń mechanicznych ogumienia, mających wpływ na bezpieczna eksploatację, operator wózka',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	powiadamia przełożonego o stwierdzonej niezgodności, ale nie przerywa pracy',
            correct: false
          }, {
            text: '•	wstrzymuje prace urządzenia i powiadamia przełożonego o stwierdzonej niezgodności',
            correct: true
          }, {
            text: '•	kontynuuje prace zmniejszając prędkość jazdy',
            correct: false
          }, {
            text: '•	kontynuuje prace zmniejszając prędkości poruszania się',
            correct: false
          }]
        }, {
          question: '157.Operator po zauważeniu podczas jazdy palącej się lampki kontrolnej ciśnienia oleju silnika powinien',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zjechać w bezpieczne miejsce, opuścić ładunek, wyłączyć silnik',
            correct: false
          }, {
            text: '•	może kontynuować jazdę jeśli stan oleju jest prawidłowy',
            correct: false
          }, {
            text: '•	nie musi podejmować żadnych działań',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '158.Po zakończeniu pracy operator powinien',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	upewnić się, ze widły są opuszczone, wózek jest w miejscu stałego postoju i nie stwarza zagrożenia',
            correct: false
          }, {
            text: '•	uruchomić hamulec postojowy',
            correct: false
          }, {
            text: '•	wcisnąć łącznik STOP',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '159.Sprawne dźwignie sterujące',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	po zwolnieniu nacisku powinny samoczynnie wracać do pozycji neutralnych',
            correct: false
          }, {
            text: '•	mogą nie mieć oznaczeń gdy operator wie do czego służą',
            correct: false
          }, {
            text: '•	powinny realizować kierunki ruchów zgodne z oznaczeniami',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '160.Opis próby sprawdzenia poprawności działania hamulca zasadniczego opisuje',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	instrukcja obsługi wózka',
            correct: true
          }, {
            text: '•	ustawa o dozorze technicznym',
            correct: false
          }, {
            text: '•	dyrektywa maszynowa',
            correct: false
          }, {
            text: '•	wewnętrzne przepisy zakładowe',
            correct: false
          }]
        }, {
          question: '161.Informacje dotyczące sposobu sprawdzania poprawności działania hamulca pomocniczego są zawarte w',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	rozporządzeniu w sprawie eksploatacji urządzeń transportu bliskiego',
            correct: false
          }, {
            text: '•	instrukcji obsługi wózka',
            correct: true
          }, {
            text: '•	ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	wytycznych inspektora BHP',
            correct: false
          }]
        }, {
          question: '162.Podczas próby hamulca zasadniczego maszt powinien być w pozycji',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	pozycja masztu nie ma znaczenia',
            correct: false
          }, {
            text: '•	przechylony „na siebie"',
            correct: true
          }, {
            text: '•	przechylony „od siebie"',
            correct: false
          }, {
            text: '•	pionowej',
            correct: false
          }]
        }, {
          question: '163.Próbę hamulca zasadniczego należy przeprowadzać',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	z ładunkiem 110% udźwigu urządzenia',
            correct: false
          }, {
            text: '•	z ładunkiem 125% udźwigu urządzenia',
            correct: false
          }, {
            text: '•	bez ładunku',
            correct: false
          }, {
            text: '•	bez ładunku a następnie z ładunkiem nominalnym',
            correct: true
          }]
        }, {
          question: '164.Jeżeli w czasie próby hamulca pomocniczego operator uzna, ze jego działanie jest nieprawidłowe powinien',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	wstrzymać eksploatacje urządzenia',
            correct: false
          }, {
            text: '•	poinformować przełożonego',
            correct: false
          }, {
            text: '•	kontynuować prace ze zmniejszona prędkością jazdy',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '165.W przypadku stwierdzenia awarii układu hamulcowego operator powinien',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w ramach posiadanych kompetencji wykonać naprawę hamulca',
            correct: false
          }, {
            text: '•	wstrzymać eksploatacje urządzenia',
            correct: true
          }, {
            text: '•	poinformować Urząd Dozoru Technicznego',
            correct: false
          }, {
            text: '•	kontynuować prace z zachowaniem szczególnej ostrożności',
            correct: false
          }]
        }, {
          question: '166.W przypadku stwierdzenia wycieku płynu hamulcowego, operator powinien',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	uzupełnić płyn hamulcowy i kontynuować jazdę do zakończenia pracy',
            correct: false
          }, {
            text: '•	wstrzymać eksploatacje urządzenia i powiadomić przełożonego',
            correct: true
          }, {
            text: '•	wstrzymać eksploatacje urządzenia i powiadomić inspektora UDT',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: false
          }]
        }, {
          question: '167.W przypadku stwierdzenia niewłaściwego działania hamulca pomocniczego, operator',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	na wyraźne polecenie przełożonego dokonuje jego naprawy',
            correct: false
          }, {
            text: '•	zgłasza awarie do UDT',
            correct: false
          }, {
            text: '•	wstrzymuje eksploatacje urządzenia i powiadamia przełożonego',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '168.Hamulec zasadniczy należy sprawdzać jadąc wózkiem podnośnikowym i hamując',
        image: require('@/assets/blank.png'),
          answers: [{
            text: '•	do przodu',
            correct: false
          }, {
            text: '•	do tyłu',
            correct: false
          }, {
            text: '•	w obu kierunkach',
            correct: true
          }, {
            text: '•	hamulec sprawdza tylko konserwator',
            correct: false
          }]
        }, {
          question: '169.Operator powinien przeprowadzić sprawdzenie hamulców',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zgodnie z terminami zawartymi w instrukcji konserwacji',
            correct: false
          }, {
            text: '•	raz na miesiąc',
            correct: false
          }, {
            text: '•	raz na tydzień',
            correct: false
          }, {
            text: '•	zawsze przed rozpoczęciem pracy',
            correct: true
          }]
        }, {
          question: '170.Schodząc z fotela operatora, Obsługujący wózek powinien',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zawsze załączyć hamulec postojowy',
            correct: true
          }, {
            text: '•	załączyć hamulec postojowy tylko w przypadku postoju wózka na wzniesieniu',
            correct: false
          }, {
            text: '•	unieść widły na maksymalna wysokość',
            correct: false
          }, {
            text: '•	przechylić maszt w pozycje "na siebie"',
            correct: false
          }]
        }, {
          question: '171.Zakres czynności kontrolnych masztu wózka podnośnikowego obejmuje',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	sprawdzenie czy nie wystąpiły pęknięcia',
            correct: false
          }, {
            text: '•	sprawdzenie stanu rolek prowadzących',
            correct: false
          }, {
            text: '•	sprawdzenie ogranicznika krańcowego położenia karetki',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: true
          }]
        }, {
          question: '172.Podczas jazdy wózkiem podnośnikowym z ładunkiem na widłach należy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	manipulować pochyłem masztu w zależności od ukształtowania terenu',
            correct: false
          }, {
            text: '•	poruszać się z masztem przechylonym „na siebie"',
            correct: true
          }, {
            text: '•	transportować ładunek w dowolny wybrany przez operatora sposób',
            correct: false
          }, {
            text: '•	manipulować pochyłem masztu w zależności od prędkości poruszania się',
            correct: false
          }]
        }, {
          question: '173.Ładunek należy transportować',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	na wysokości powyżej linii wzroku operatora, jeżeli poprawia to widoczność',
            correct: false
          }, {
            text: '•	na wysokości około 20-30 cm nad poziomem podłoża',
            correct: true
          }, {
            text: '•	na dowolnej wysokości',
            correct: false
          }, {
            text: '•	na wysokości ok 90 cm',
            correct: false
          }]
        }, {
          question: '174.Podczas zjazdu z pochyłej rampy wózkiem czołowym podnośnikowym wraz z ładunkiem, operator',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	porusza się przodem',
            correct: false
          }, {
            text: '•	porusza się tyłem',
            correct: false
          }, {
            text: '•	zachowuje szczególna ostrożność',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '175.Podczas wjazdu na pochyła rampę wózkiem jezdniowym podnośnikowym z ładunkiem ograniczającym widoczność, operator',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	korzysta z pomocy drugiej osoby',
            correct: false
          }, {
            text: '•	porusza się przodem',
            correct: false
          }, {
            text: '•	porusza się tyłem',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: true
          }]
        }, {
          question: '176.Poruszanie się wózkiem w poprzek pochyłej rampy jest',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zabronione',
            correct: true
          }, {
            text: '•	dozwolone',
            correct: false
          }, {
            text: '•	dopuszczalne pod warunkiem zachowania szczególnej ostrożności',
            correct: false
          }, {
            text: '•	dopuszczalne pod warunkiem obciążenia wózka ładunkiem uniesionym na minimalna wysokość',
            correct: false
          }]
        }, {
          question: '177.Poruszając się wózkiem z ładunkiem ograniczającym widoczność operator powinien',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jechać tyłem',
            correct: false
          }, {
            text: '•	jechać przodem, z pomocą osoby informującej o zagrożeniach',
            correct: false
          }, {
            text: '•	poruszać się z bezpieczna prędkością',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '178.Podczas jazdy wózkiem jezdniowym podnośnikowym z ładunkiem należy',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	unikać gwałtownych skrętów',
            correct: false
          }, {
            text: '•	przewozić ładunek na wysokości transportowej',
            correct: false
          }, {
            text: '•	dostosować prędkość jazdy do panujących warunków',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '179.Wylot zaworu butli gazowej powinien być skierowany',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w dół',
            correct: true
          }, {
            text: '•	w górę',
            correct: false
          }, {
            text: '•	poziomo',
            correct: false
          }, {
            text: '•	pozycja nie ma znaczenia',
            correct: false
          }]
        }, {
          question: '180.Szczelność instalacji gazowej sprawdza się przy pomocy',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	detektora gazu',
            correct: false
          }, {
            text: '•	specjalnego środka',
            correct: false
          }, {
            text: '•	wody mydlanej',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '181.Eksploatacja wózka jezdniowego w temperaturze poniżej -10?C',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest dozwolona pod warunkiem wyposażenia wózka w ogrzewanie kabiny operatora',
            correct: false
          }, {
            text: '•	jest dozwolona jeśli instrukcja eksploatacji na to zezwala',
            correct: true
          }, {
            text: '•	jest zabroniona z uwagi na możliwości utraty przyczepności',
            correct: false
          }, {
            text: '•	jest zabroniona z uwagi na zmianę parametrów technicznych oleju hydraulicznego',
            correct: false
          }]
        },
        {
          question: '182.Eksploatacja wózka jezdniowego w temperaturze powyżej 30?Cp',
         image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest zabroniona z uwagi na pogorszenie warunków pracy operatora',
            correct: false
          }, {
            text: '•	jest dozwolona pod warunkiem wyposażenia wózka w klimatyzowana kabinę operatora',
            correct: false
          }, {
            text: '•	jest zabroniona z uwagi na zmianę parametrów technicznych oleju hydraulicznego',
            correct: false
          }, {
            text: '•	jest dozwolona jeśli instrukcja eksploatacji na to zezwala',
            correct: true
          }]
        }, {
          question: '183.W oparciu o tabele określ jakie maksymalne obciążenie może przenieść gniazdo ładunkowe regału',
        image: require('@/assets/diagram1.png'),
          answers: [{
            text: '•	1320 kg',
            correct: false
          }, {
            text: '•	1100 kg',
            correct: false
          }, {
            text: '•	2700 kg',
            correct: false
          }, {
            text: '•	2200 kg',
            correct: true
          }]
        }, {
          question: '184.W oparciu o tabele, określ na które najwyższe gniazdo ładunkowe podasz towar dysponując wózkiem o maksymalnej wysokości podnoszenia 2100 mm',
          image: require('@/assets/diagram1.png'),
          answers: [{
            text: '•	gniazdo 1',
            correct: false
          }, {
            text: '•	gniazdo 2',
            correct: false
          }, {
            text: '•	gniazdo 3',
            correct: false
          }, {
            text: '•	gniazdo 4',
            correct: true
          }]
        }, {
          question: '185.Odstawiając ładunek na regał magazynowy operator powinien znać',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	masę towaru i obciążenie maksymalne gniazda regału',
            correct: false
          }, {
            text: '•	masę towaru i obciążenie minimalne ramy regału',
            correct: false
          }, {
            text: '•	wymiary zewnętrzne transportowanego ładunku',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '186.Podczas transportu ładunków wielkogabarytowych operator powinien',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jechać tyłem',
            correct: false
          }, {
            text: '•	jechać przodem wychylając się poza obrys wózka',
            correct: false
          }, {
            text: '•	jechać przodem korzystając z pomocy drugiej osoby',
            correct: false
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: true
          }]
        },
        {
          question: '187.Na co powinien zwrócić uwagę operator podczas wymiany baterii trakcyjnych?',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	na masę i wymiary baterii',
            correct: false
          }, {
            text: '•	na pojemność baterii',
            correct: false
          }, {
            text: '•	na dane adresowe producenta baterii',
            correct: false
          }, {
            text: '•	odpowiedzi a i b są prawidłowe',
            correct: true
          }]
        }, {
          question: '188.Przyczyna utraty stateczności wózka może być',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zbyt niskie ciśnienie w oponach',
            correct: false
          }, {
            text: '•	szybka jazda w zakrętach',
            correct: false
          }, {
            text: '•	gwałtowne hamowanie przy jeździe z ładunkiem',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '189.Dopuszczalna prędkość jazdy wózka jest określona',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w ustawie o dozorze technicznym',
            correct: false
          }, {
            text: '•	w protokole badania wystawionym przez UDT',
            correct: false
          }, {
            text: '•	w decyzji zezwalającej na eksploatacje',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        }, {
          question: '190.Przed rozpoczęciem pracy wózkiem należy sprawdzić funkcjonowanie',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	układu hydraulicznego',
            correct: false
          }, {
            text: '•	układu hamulcowego',
            correct: false
          }, {
            text: '•	układu kierowniczego',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '191.Po zamontowaniu dodatkowego osprzętu wymiennego należy',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zapoznać się z właściwym diagramem udźwigu',
            correct: true
          }, {
            text: '•	zgłosić do UDT w celu wykonania badania technicznego',
            correct: false
          }, {
            text: '•	sprawdzić, czy zakres posiadanych uprawnień do obsługi obejmuje zamontowany osprzęt',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: false
          }]
        }, {
          question: '192.Przed wjazdem wózkiem na rampę załadowcza operator powinien sprawdzić',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	kat nachylenia rampy, oraz zdolność wózka do pokonywania wzniesień',
            correct: false
          }, {
            text: '•	nośność rampy',
            correct: false
          }, {
            text: '•	ciężar ładunku oraz masę własna wózka',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '193.Podczas jazdy wózkiem podnośnikowym należy',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	przestrzegać przepisów BHP',
            correct: false
          }, {
            text: '•	stosować się do znaków, oznaczeń i symboli umieszczonych w obszarze pracy wózka',
            correct: false
          }, {
            text: '•	przestrzegać instrukcji obsługi wózka',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '194.Gdzie znajduje się informacja dotycząca udźwigu wózka',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	w instrukcji eksploatacji wózka',
            correct: false
          }, {
            text: '•	na tabliczce znamionowej wózka',
            correct: false
          }, {
            text: '•	na diagramie udźwigu',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '195.Przed rozpoczęciem pracy wózkiem należy',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	zapoznać się z zakresem pracy',
            correct: false
          }, {
            text: '•	określić masę transportowanego ładunku',
            correct: false
          }, {
            text: '•	sprawdzić, czy osprzęt wózka jest właściwie dobrany do ładunku',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są prawidłowe',
            correct: true
          }]
        }, {
          question: '196.Praca wózka z koszem do podnoszenia osób zakładanym na widły',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	jest dozwolona wyłącznie po uzgodnieniu szczegółowych warunków eksploatacji z UDT',
            correct: true
          }, {
            text: '•	jest dozwolona bez dodatkowych wymagań',
            correct: false
          }, {
            text: '•	jest zabroniona',
            correct: false
          }, {
            text: '•	jest dozwolona za zgoda właściciela zakładu bez dodatkowych wymagań',
            correct: false
          }]
        }, {
          question: '197.W przypadku kiedy wózek traci stateczność, operator',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	stara się opuścić kabinę wózka (przed jego wywróceniem się)',
            correct: false
          }, {
            text: '•	pozostaje w kabinie',
            correct: false
          }, {
            text: '•	utrzymuje pozycje siedząca trzymając się mocno kierownicy',
            correct: false
          }, {
            text: '•	odpowiedz b i c jest prawidłowa',
            correct: true
          }]
        }, {
          question: '198.W chwili wywracania się wózka należy',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	niezwłocznie wyskoczyć z kabiny',
            correct: false
          }, {
            text: '•	ostro zahamować',
            correct: false
          }, {
            text: '•	skręcić gwałtownie koła w kierunku przechylenia, by spróbować zapobiec wywróceniu',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        }, {
          question: '199.Wózek może stracić stateczność na skutek',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	podnoszenia ładunku o ciężarze większym niż udźwig wózka',
            correct: false
          }, {
            text: '•	wykonywania gwałtownych skrętów kół podczas jazdy',
            correct: false
          }, {
            text: '•	zawracania wózkiem na wzniesieniu',
            correct: false
          }, {
            text: '•	wszystkie powyżej są prawidłowe',
            correct: true
          }]
        }, {
          question: '200.Jeżeli instrukcja wózka nie stanowi inaczej, następujące w toku eksploatacji maksymalne wydłużenie łańcucha nośnego może wynosić',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	3 cm',
            correct: false
          }, {
            text: '•	3 mm',
            correct: false
          }, {
            text: '•	3%',
            correct: true
          }, {
            text: '•	10%',
            correct: false
          }]
        },
        {
          question: '201.Jeżeli instrukcja wózka nie stanowi inaczej, dopuszczalna ilość pękniętych płytek łańcucha nośnego (konstrukcji Flyera) wynosi',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	3% całkowitej ilości płytek',
            correct: false
          }, {
            text: '•	6 sztuk na długości 30 ogniw',
            correct: false
          }, {
            text: '•	1 sztuka na każdy metr łańcucha',
            correct: false
          }, {
            text: '•	0',
            correct: true
          }]
        }, {
          question: '202.Jeżeli instrukcja wózka nie stanowi inaczej, minimalna dopuszczalna grubość poziomej części wideł zmierzona w pobliżu ich naroża (piety) wynosi',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	25 mm przy grubości nominalnej 30 mm',
            correct: false
          }, {
            text: '•	57 mm przy grubości nominalnej 60 mm',
            correct: false
          }, {
            text: '•	36 mm przy grubości nominalnej 40 mm',
            correct: true
          }, {
            text: '•	zawsze wynosi 50% grubości nominalnej wideł',
            correct: false
          }]
        }, {
          question: '203.Jeżeli instrukcja wózka nie stanowi inaczej, minimalna dopuszczalna grubość poziomej części wideł zmierzona w pobliżu ich naroża (piety) wynosi',
          image: require('@/assets/blank.png'),
          answers: [{
            text: '•	27 mm przy grubości nominalnej 30 mm',
            correct: true
          }, {
            text: '•	57 mm przy grubości nominalnej 60 mm',
            correct: false
          }, {
            text: '•	25 mm przy grubości nominalnej 30 mm',
            correct: false
          }, {
            text: '•	zawsze wynosi 50% grubości nominalnej wideł',
            correct: false
          }]
        }, {
          question: '204.Jeżeli instrukcja wózka nie stanowi inaczej, minimalna dopuszczalna grubość poziomej części wideł zmierzona w pobliżu ich naroża (piety) wynosi',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	25 mm przy grubości nominalnej 30 mm',
            correct: false
          }, {
            text: '•	55 mm przy grubości nominalnej 60 mm',
            correct: true
          }, {
            text: '•	40 mm przy grubości nominalnej 60 mm',
            correct: false
          }, {
            text: '•	zawsze wynosi 50% grubości nominalnej wideł',
            correct: false
          }]
        }, {
          question: '205.Jeżeli instrukcja wózka nie stanowi inaczej, minimalna dopuszczalna grubość poziomej części wideł zmierzona w pobliżu ich naroża (piety) wynosi',
           image: require('@/assets/blank.png'),
          answers: [{
            text: '•	25 mm przy grubości nominalnej 30 mm',
            correct: false
          }, {
            text: '•	45 mm przy grubości nominalnej 50 mm',
            correct: true
          }, {
            text: '•	50 mm przy grubości nominalnej 60 mm',
            correct: false
          }, {
            text: '•	zawsze wynosi 50% grubości nominalnej wideł',
            correct: false
          }]
        }, {
          question: '206.Jeżeli instrukcja wózka nie stanowi inaczej, maksymalne dopuszczalne rozgięcie widły względem wartości oryginalnej (zwykle 90 stopni), wynosi',
       image: require('@/assets/blank.png'),
          answers: [{
            text: '•	1 cm',
            correct: false
          }, {
            text: '•	3%',
            correct: false
          }, {
            text: '•	3 stopnie',
            correct: true
          }, {
            text: '•	0 stopni',
            correct: false
          }]
        },
        {
          question: '207.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony A',
        image: require('@/assets/diagram2.png'),
          answers: [{
            text: '•	4836 mm',
            correct: true
          }, {
            text: '•	4030 mm',
            correct: false
          }, {
            text: '•	3100 mm',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '208.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony B',
         image: require('@/assets/diagram2.png'),
          answers: [{
            text: '•	3100 mm',
            correct: false
          }, {
            text: '•	4836 mm',
            correct: false
          }, {
            text: '•	4030 mm',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '209.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony A',
          image: require('@/assets/diagram3.png'),
          answers: [{
            text: '•	3510 mm',
            correct: true
          }, {
            text: '•	4212 mm',
            correct: false
          }, {
            text: '•	2700 mm',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '210.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony B',
           image: require('@/assets/diagram3.png'),
          answers: [{
            text: '•	4212 mm',
            correct: false
          }, {
            text: '•	2700 mm',
            correct: false
          }, {
            text: '•	3520 mm',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        },
        {
          question: '211.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony A',
           image: require('@/assets/diagram4.png'),
          answers: [{
            text: '•	2600 mm',
            correct: false
          }, {
            text: '•	3380 mm',
            correct: false
          }, {
            text: '•	4056 mm',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '212.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony B',
         image: require('@/assets/diagram4.png'),
          answers: [{
            text: '•	4056 mm',
            correct: false
          }, {
            text: '•	2600 mm',
            correct: true
          }, {
            text: '•	3380 mm',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        },
        {
          question: '213.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony A',
          image: require('@/assets/diagram5.png'),
          answers: [{
            text: '•	3640 mm',
            correct: false
          }, {
            text: '•	4368 mm',
            correct: false
          }, {
            text: '•	2800 mm',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '214.W oparciu o przedstawiony diagram udźwigu i rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego od strony B',
          image: require('@/assets/diagram5.png'),
          answers: [{
            text: '•	2800 mm',
            correct: false
          }, {
            text: '•	3640 mm',
            correct: false
          }, {
            text: '•	4368 mm',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        },
        {
          question: '215.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna bezpieczna wysokość podnoszenia ładunku pobranego z kierunku A',
          image: require('@/assets/diagram6.png'),
          answers: [{
            text: '•	2350 mm',
            correct: false
          }, {
            text: '•	3300 mm',
            correct: true
          }, {
            text: '•	1400 mm',
            correct: false
          }, {
            text: '•	1300 mm',
            correct: false
          }]
        }, {
          question: '216.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna bezpieczna wysokość podnoszenia, ładunku pobranego z kierunku A',
          image: require('@/assets/diagram7.png'),
          answers: [{
            text: '•	700 mm',
            correct: false
          }, {
            text: '•	1200 mm',
            correct: false
          }, {
            text: '•	4500 mm',
            correct: true
          }, {
            text: '•	1800 mm',
            correct: false
          }]
        },
        {
          question: '217.W oparciu o przedstawiony diagram udźwigu oraz rysunek wskaż, na który regał lub regały można postawić ładunek',
          image: require('@/assets/diagram8.png'),
          answers: [{
            text: '•	Regał 1',
            correct: false
          }, {
            text: '•	Regał 2',
            correct: false
          }, {
            text: '•	Regał 3',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        }, {
          question: '218.W oparciu o przedstawiony diagram udźwigu oraz rysunek wskaż, na który regał lub regały można postawić ładunek',
          image: require('@/assets/diagram9.png'),
          answers: [{
            text: '•	Regał 1',
            correct: true
          }, {
            text: '•	Regał 2',
            correct: false
          }, {
            text: '•	Regał 3',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są poprawne',
            correct: false
          }]
        },
        {
          question: '219.W oparciu o przedstawiony diagram udźwigu oraz rysunek wskaż, na ktory regał lub regały można postawić ładunek',
         image: require('@/assets/diagram10.png'),
          answers: [{
            text: '•	Regał 1',
            correct: false
          }, {
            text: '•	Regał 2',
            correct: true
          }, {
            text: '•	Regał 3',
            correct: false
          }, {
            text: '•	odpowiedz a i b jest prawidłowa',
            correct: false
          }]
        }, {
          question: '220.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna bezpieczna wysokość podnoszenia, ładunku pobranego z kierunku A',
          image: require('@/assets/diagram11.png'),
          answers: [{
            text: '•	5940 mm',
            correct: true
          }, {
            text: '•	7890 mm',
            correct: false
          }, {
            text: '•	3600 mm',
            correct: false
          }, {
            text: '•	4500 mm',
            correct: false
          }]
        },
        {
          question: '221.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną bezpieczną wysokość podnoszenia, ładunku pobranego z kierunku B',
          image: require('@/assets/diagram12.png'),
          answers: [{
            text: '•	5940 mm',
            correct: false
          }, {
            text: '•	7890 mm',
            correct: false
          }, {
            text: '•	3600 mm',
            correct: true
          }, {
            text: '•	4500 mm',
            correct: false
          }]
        }, {
          question: '222.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną bezpieczną wysokość podnoszenia, ładunku pobranego z kierunku A',
         image: require('@/assets/diagram13.png'),
          answers: [{
            text: '•	4860 mm',
            correct: false
          }, {
            text: '•	8820 mm',
            correct: false
          }, {
            text: '•	7070 mm',
            correct: true
          }, {
            text: '•	10820 mm',
            correct: false
          }]
        },
        {
          question: '223.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną bezpieczną wysokość podnoszenia, ładunku pobranego z kierunku B',
          image: require('@/assets/diagram14.png'),
          answers: [{
            text: '•	4860 mm',
            correct: false
          }, {
            text: '•	5660 mm',
            correct: true
          }, {
            text: '•	7070 mm',
            correct: false
          }, {
            text: '•	10820 mm',
            correct: false
          }]
        }, {
          question: '224.W oparciu o przedstawiony diagram udźwigu określ maksymalny udźwig wózka na wysokości 6 m',
          image: require('@/assets/diagram14.png'),
          answers: [{
            text: '•	1300 kg',
            correct: false
          }, {
            text: '•	1500 kg',
            correct: true
          }, {
            text: '•	1700 kg',
            correct: false
          }, {
            text: '•	2000 kg',
            correct: false
          }]
        },
        {
          question: '225.W oparciu o przedstawiony diagram udźwigu określ maksymalny udźwig wózka na wysokości 6,7 m',
          image: require('@/assets/diagram15.png'),
          answers: [{
            text: '•	1400 kg',
            correct: false
          }, {
            text: '•	1200 kg',
            correct: false
          }, {
            text: '•	1000 kg',
            correct: true
          }, {
            text: '•	1300 kg',
            correct: false
          }]
        }, {
          question: '226.W oparciu o przedstawiony diagram udźwigu określ maksymalną masę ładunku, o wymiarach podstawy 1,6 m x 1,6 m',
          image: require('@/assets/diagram16.png'),
          answers: [{
            text: '•	4,5 t',
            correct: false
          }, {
            text: '•	4,0 t',
            correct: true
          }, {
            text: '•	3,5 t',
            correct: false
          }, {
            text: '•	3,0 t',
            correct: false
          }]
        },
        {
          question: '227.W oparciu o przedstawiony diagram udźwigu określ maksymalną masę ładunku, o wymiarach podstawy 2 m x 2 m',
           image: require('@/assets/diagram16.png'),
          answers: [{
            text: '•	2,5 t',
            correct: false
          }, {
            text: '•	3,5 t',
            correct: true
          }, {
            text: '•	4,5 t',
            correct: false
          }, {
            text: '•	3,0 t',
            correct: false
          }]
        }, {
          question: '228.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną masę ładunku pobranego od strony B',
           image: require('@/assets/diagram17.png') ,
          answers: [{
            text: '•	1300 kg',
            correct: false
          }, {
            text: '•	1400 kg',
            correct: true
          }, {
            text: '•	1600 kg',
            correct: false
          }, {
            text: '•	2300 kg',
            correct: false
          }]
        },
        {
          question: '229.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną masę ładunku pobranego od strony A',
           image: require('@/assets/diagram17.png'),
          answers: [{
            text: '•	1500 kg',
            correct: false
          }, {
            text: '•	2000 kg',
            correct: false
          }, {
            text: '•	2300 kg',
            correct: true
          }, {
            text: '•	2500 kg',
            correct: false
          }]
        }, {
          question: '230.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalną masę ładunku pobranego od strony B',
           image: require('@/assets/diagram18.png'),
          answers: [{
            text: '•	1100 kg',
            correct: false
          }, {
            text: '•	1450 kg',
            correct: true
          }, {
            text: '•	1800 kg',
            correct: false
          }, {
            text: '•	2300 kg',
            correct: false
          }]
        },
        {
          question: '231.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, jaką można bezpiecznie podnieść pobierając ładunek od strony A :',
          image: require('@/assets/diagram18.png'),
          answers: [{
            text: '•	1500 kg',
            correct: false
          }, {
            text: '•	2000 kg',
            correct: false
          }, {
            text: '•	2300 kg',
            correct: false
          }, {
            text: '•	1800 kg',
            correct: true
          }]
        },
        {
          question: '232.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, jaką można bezpiecznie podnieść pobierając ładunek od strony A',
          image: require('@/assets/diagram19.png'),
          answers: [{
            text: '•	2695 kg',
            correct: false
          }, {
            text: '•	3185 kg',
            correct: false
          }, {
            text: '•	3500 kg',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '233.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, jaką można bezpiecznie podnieść pobierając ładunek od strony B',
          image: require('@/assets/diagram19.png'),
          answers: [{
            text: '•	2695 kg',
            correct: false
          }, {
            text: '•	3500 kg',
            correct: false
          }, {
            text: '•	3185 kg',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '234.W oparciu o przedstawiony diagram udźwigu określ maksymalny udźwig wózka, podnoszącego ładunek na wysokość 3000 mm',
         image: require('@/assets/diagram20.png'),
          answers: [{
            text: '•	2400 kg',
            correct: false
          }, {
            text: '•	3600 kg',
            correct: true
          }, {
            text: '•	3500 kg',
            correct: false
          }, {
            text: '•	1500 kg',
            correct: false
          }]
        }, {
          question: '235.W oparciu o przedstawiony diagram udźwigu określ maksymalny udźwig wózka, podnoszącego ładunek na wysokość 4000 mm',
          image: require('@/assets/diagram20.png'),
          answers: [{
            text: '•	3300 kg',
            correct: false
          }, {
            text: '•	4000 kg',
            correct: false
          }, {
            text: '•	3400 kg',
            correct: true
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: false
          }]
        }, {
          question: '236.W oparciu o przedstawiony diagram udźwigu określ maksymalny udźwig wózka, podnoszącego ładunek na wysokość 5000 mm',
          image: require('@/assets/diagram20.png'),
          answers: [{
            text: '•	4000 kg',
            correct: false
          }, {
            text: '•	2700 kg',
            correct: false
          }, {
            text: '•	3400 kg',
            correct: false
          }, {
            text: '•	wszystkie odpowiedzi są niepoprawne',
            correct: true
          }]
        }, {
          question: '237.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku jaką można bezpiecznie podnieść na wysokość 4000 mm, pobierając od strony B',
           image: require('@/assets/diagram21.png'),
          answers: [{
            text: '•	3400 kg',
            correct: false
          }, {
            text: '•	2900 kg',
            correct: true
          }, {
            text: '•	2700 kg',
            correct: false
          }, {
            text: '•	3600 kg',
            correct: false
          }]
        }, {
          question: '238.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku jaką można bezpiecznie podnieść na wysokość 4000 mm, pobierając od strony A',
         image: require('@/assets/diagram21.png'),
          answers: [{
            text: '•	2900 kg',
            correct: false
          }, {
            text: '•	3600 kg',
            correct: false
          }, {
            text: '•	3400 kg',
            correct: true
          }, {
            text: '•	3200 kg',
            correct: false
          }]
        }, {
          question: '239.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony B',
          image: require('@/assets/diagram22.png'),
          answers: [{
            text: '•	1000 kg',
            correct: false
          }, {
            text: '•	1200 kg',
            correct: false
          }, {
            text: '•	1500 kg',
            correct: true
          }, {
            text: '•	2300 kg',
            correct: false
          }]
        }, {
          question: '240.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony A',
          image: require('@/assets/diagram22.png'),
          answers: [{
            text: '•	1600 kg',
            correct: false
          }, {
            text: '•	1900 kg',
            correct: false
          }, {
            text: '•	2300 kg',
            correct: true
          }, {
            text: '•	2500 kg',
            correct: false
          }]
        }, {
          question: '241.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony A',
          image: require('@/assets/diagram23.png'),
          answers: [{
            text: '•	400 kg',
            correct: false
          }, {
            text: '•	600 kg',
            correct: false
          }, {
            text: '•	1500 kg',
            correct: false
          }, {
            text: '•	2000 kg',
            correct: true
          }]
        }, {
          question: '242.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony B',
          image: require('@/assets/diagram23.png'),
          answers: [{
            text: '•	400 kg',
            correct: false
          }, {
            text: '•	600 kg',
            correct: false
          }, {
            text: '•	1500 kg',
            correct: true
          }, {
            text: '•	2000 kg',
            correct: false
          }]
        }, {
          question: '243.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony A',
          image: require('@/assets/diagram24.png'),
          answers: [{
            text: '•	1400 kg',
            correct: true
          }, {
            text: '•	1255 kg',
            correct: false
          }, {
            text: '•	1040 kg',
            correct: false
          }, {
            text: '•	840 kg',
            correct: false
          }]
        }, {
          question: '244.W oparciu o przedstawiony diagram udźwigu oraz rysunek określ maksymalna masę ładunku, pobranego od strony B',
        image: require('@/assets/diagram24.png'),
          answers: [{
            text: '•	1400 kg',
            correct: false
          }, {
            text: '•	1255 kg',
            correct: false
          }, {
            text: '•	1040 kg',
            correct: true
          }, {
            text: '•	840 kg',
            correct: false
          }]
        }, {
          question: '245.Świecąca się kontrolka ciśnienia oleju może świadczy o',
        image: require('@/assets/diagram25.png'),
          answers: [{
            text: '•	zbyt niskim poziomie płyny w układzie hamulcowym',
            correct: false
          }, {
            text: '•	podwyższonej temperaturze silnika',
            correct: false
          }, {
            text: '•	zbyt niskim ciśnieniu oleju',
            correct: true
          }, {
            text: '•	odpowiedz a i c jest prawidłowa',
            correct: false
          }]
        },
      ],
      a: 0,
      b: 1,
    select: false,
    score: 0,
    inscore:0,
    // props: ['source'],
    }
  },
  methods: {
    selectResponse(e) {
      this.select = true;

      if(e.correct){
        this.score++;
      }else{
        this.inscore++;
      }
    },
    chack(status) {
      if (status.correct) {
        return 'correct'
      } else {
        return 'false'
      }
    },
    nextQuestion(){
       if(this.a <= (this.questions.length -2)){
      this.a++
      this.b++
      this.select = false
       }
    },
    skipFast(){
      if(this.a <= (this.questions.length -10) ){
      this.a = this.a +20
      this.b = this.b +20
      this.select = false
    }
    },
    restartQuiz(){
        Object.assign(this.$data, this.$options.data())
    },
  //   function() {
  //   if (this.source) { //is it empty
  //     this.img = this.source //replace placeholder
  //   }
  //  this.loading = true
  // },
  }
}
</script>
