# zenebefogado-mozdulatok
Zenebefogadó mozdulatok kutatását segítő kód

## 
Halmozottan fogyatékos emberek is reagálnak a zenére apró mozdulatokkal, gesztusokkal. Ezek egyáltalán nem véletlenszerű mozdulatok és videókat elemezve szépen meg-meglátszik, ahogy az alany talán emékszik részekre, számít fordulatokra, reagál zenei kavarásokra. [Dr. Tisza Luca](https://m2.mtmt.hu/api/author/10057971) ezekre ad példát a [habilitációján készült videóban](https://youtu.be/waJhOL6B2yU?si=U1BiXfLmTosM0fgV&t=1240) is láthatunk.

Zenék, videók és EEG adatok párhuzamos elemzése kézi erővel egy rettenetesen nagy feladat. 

A zenei jutalom (tetszik a zene, értékelünk egy zenei viccet) feltételezi a memória, szabályosságok felismerése és anticipáció működését. Mivel halmozottan fogyatékos ("IQ 20") zenehallgatók gyakran több ilyenre reagálnak, mint olyan átlagember, aki zeneileg csak nagyon eyszerű zenéket hallgat, tehát ezekre a viccekre "nem állt rá a füle". Ebből következne, hogy az "IQ 20" beskatulyázás nem kielégítő, mégiscsk tud tanulni. Sőt akár van olyan erőssége, amit még jobban is csinál, mint az "átlagember", ami nagy forradalmat jelentene az oktatásban. Ehhez nem ártana egy egyszerű mérés és számolás, különben csak nagyon kis mintán tesztelhető.  Erre készült a videó, ahol a zongorista nagyon durva szabálytalanságokat művel egy Bach darabbal. Na ezzel lehet kezdeni a tesztelést, hogy észreveszi-e a hibát a hallgató, és ha igen, második hallgatásra is meglepi-e, vagy megtanulta, hogy az most ilyen. 

__Ma már lehetségesnek kell lennie, hogy zenét, mozdulatokat, és EEG adatokat összehangoljunk és táblázatos adattá gyúrjunk, hogy aztán pl. statisztikai módszerekkel kapcsolatokat fedezzünk fel.__

Ezzel a kóddal ezt az összehangolást és adat elemezést szeretnénk megtámogatni modern számítástechnikai eszközökkel.

## Alapanyag
Százas nagyságrendben állnak rendelkezésre videók és EEG adatok fogyatékkal élőkről, ahogy zenét hallgatnak. Ezeket szeretnénk hatékonyan elemezni.

Adatvédelmi okokból természetesen csak külön megállapodásokkal és szerződéssel lehet ezeket a videókat közvetlenül használni, de készítettünk tipikus videót ami mintául szolgálhat az elemzésekhez. Ha valaki belerágja magát a megoldás felé vezető programozásba, akkor lehetséges lehet az eredeti videók használata is a fejlesztés során.

Ami elérhető:
- Videó a zenélő zenészről, ahogy mozdul, interpretál, játszik, "viccelődik"
- Hanganyag a zenélő zenészről: ritmus, ütem, dinamika, harmónia, mindenféle érdekesség.
- Videó a befogadóról, ahogy zenehallgatás közben eltér megszokott mozdulataitól és másképp reagál
- EEG adatok (csv) a befogadóról, ahogy a zenét hallgatja.

## Első kihívás: az összehangolás
A két videót (a hozzájuk tartozó hangsávval) és az EEG adatokat közös nevezőre kellene hozni automatizáltan, hogy több tucat videóval is meg tudjuk ismételni a témában a kísérleteket. Az EEG adatok táblázatába kerüljön új oszlopba a video_zenesz és video_hallgato oszlopokba a videó fájl timeframe azonosítója a nagyobb felbontású EEG adatokhoz szinkronizálva. Ettől kezdve lesznek összehasonlíthatóak az adatok.

A szinkornizáció alapja a hang és a pislogás lehet
- A zene befogadásának videóján a zenész videójának hangsávja hallható többször is, de a környezeti zajoktól terhesen.
- Az EEG roppant pontosan kimutatja a pislogásokat, amiket a hallgató videóján is fel tudunk fedezni

## További moduláris kihívások: adattá alakítás
Ha már van egyetlen összehangolt közös táblázatunk, akkor további elemzéseket hajthatunk végre a videókon, hanganyagon, adatokon. Ezek eredményeit a táblázat egy-egy új oszlopában tüntethetjük fel. Minden elemzést egy külön script végezhet el, így idő és számításikapacitás fényében lehet ezeket az elemezéseket be- vagy kikapcsolni.

A mozgás elemzése a legfontosabb kihívás és egyre inkább finomhallgolható. [Optical Flow](https://docs.opencv.org/4.x/d4/dee/tutorial_optical_flow.html) megközelítéssel elemezhető a hallgató általános mozgása. Majd a testrészek és mozgástípusok elemzésével a mozgásadatok további részletezése, felismerése is lehetségessé válik.

A zene elemzése a másik fontos lépés. Ütem kezdetek, hangsúlyok, dallam indulások, harmóniák váltásának automatikus azonosításával lesz arral adatunk, hogy a hallgató előre mozdul számítva valamire, vagy utólag reagál. Dallami indulásokat és harmóniákat eleinte kézzel be tud a táblázatba jegyezni a kutató, de péládul ütemrendek elemzéséhez már egy AI alapú megközelítés hasznosabbnak tűnik.

## Következő fázis: adatelemzés
Ettől a kódtól független következő nagy varázslat, hogy az adatok között hogyan találunk aztán modern statisztika szoftverekkel, de akár AI támogatású big data elemzésekkel összefüggéseket, kapcsolatokat. Akár időben eltolva is: a hallgató mozgás struktúrája valamilyen módon lekövetheti - de időben eltolva - a zenész mozgását.


Ez tehát pilot kód, ami a szakemberek kutatási módszertanás segítené meg. A terv az, hogy innen egyre finomabb hibákat, vagy eredeti zeneszerző által belerejtett vicceket tesztelünk, hogy érti-e a hallgató.
Vagyis szeretnénk egy minél egyszerűbb eszközt ahhoz, hogy bizonyos dolgokat megmérjünk a zene és mozgás kapcsolatában.

