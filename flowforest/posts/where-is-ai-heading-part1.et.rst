.. title: Ülevaade AI arengusuundadest - osa 1/3
.. slug: where-is-ai-heading-part1
.. date: 2026-08-10 08:22:32 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. tags: AI, AI-progress

.. raw:: html

    <embed>
      <p class="show_if_not_teaser"; style="display:none;"><em>See postitus on esimene osa 3-osalisest seeriast, mis räägib AI arengusuundadest ja 
      trendidest.</em></p>
      <p class="show_if_not_teaser"; style="display:none;"><strong>Märkus</strong>. <em>Enamus mudelitest, mida siin postituses käsitlen, on 
      LLM-d ("Large Language Model", eesti keeles "suur keelemudel"). Kasutan terminit "LLM", kui soovin rõhutada, et räägin just neist; 
      üldisemat terminit "AI" kasutan, kui räägin üleüldiselt kõikvõimalikest AI süsteemidest ja arhitektuuridest 
      (sealhulgas neist, mida võidakse leiutada tulevikus).
      Kui termin 'LLM' või 'suur keelemudel' pole tuttav, loe ikka edasi - lähitulevikus tuleb järgmine postitus, kus me räägime sellest, mis 
      keelemudelid oma olemuselt on. Käesoleva postituse mõistmiseks piisab vaid, kui mõelda mõnedest tuntud keelemudelitest 
      nagu Chat-GPT, Claude, DeepSeek, Gemini, jne.</em></p>
      <h1 class="show_if_not_teaser"; style="display:none;">Sissejuhatus</h1>
    </embed>

Viimasel ajal tundub AI olevat täitnud kõik uudiskanalite pealkirjad. Aga kuidas eristada tõde liialdustest? 
Uudisteartiklid on tihti segased või kallutatud. 
Kõrvuti võib leida artikleid pealkirjadega "AI võtab üle kõik töökohad järgneva 2 aasta jooksul" ja "AI mull on kohe lõhkemas".
On selge, et ekstreemsemad pealkirjad müüvad paremini - nii ühele või teisele poole tõde kallutades.

Lisaks võib AI mudelite progress tunduda ebakorrapärane ka spetsialisti vaatenurgast - kiire arengu perioodid vahelduvad aeglastega.
Et saada selgemat ülevaadet, tuleb olukorda vaadata kaugemalt ning üle pikema ajaraami. 
See on täpselt see, mida organisatsioon `METR <https://metr.org/>`_ (mittetulunduslik uurimisinstituut Californias) on oma uurimistöös teinud. 

.. TEASER_END

=====================
Arengu mõõtmine
=====================

METR märkas, et üks AI mudelite probleemidest (eriti LLM-de puhul) on järjepidavuse puudumine - neil võib olla väga raske 
läbida pikaajalisi või mitme-sammulisi ülesandeid ilma järge kaotamata. See tähelepanek aitas neil defineerida ühe efektiivse
mõõdupuu: kui ajaliselt keerukate (inimesel ülesande lahendamiseks kuluva aja mõttes) ülesannetega saab mudel hakkama teatud fikseeritud 
tõenäosusega (nt 50% või 80%)? Nad andsid sellele mõõdikule nime **ülesannete läbimise ajahorisont** (i.k. "*task completion
time horizon*").

METR koostas nimekirja 228 erinevast ülesandest (tarkvaraarenduse, küberturvalisuse, üldise loogika, ja masinõppe valdkondadest).
Ülesanded varieeruvad triviaalsetest (lahendatav sekunditega) kuni ülesanneteni, mille lahendamiseks võib valdkonna
spetsialistil kuluda mitmeid päevi.

Siin on mõned näited ülesannetest tarkvara arenduse valdkonnast:

* ``find_shell_script`` (3 sekundit) - *“Milline neist failidest on shell'i skript?” Valikud: “run.sh”, “run.txt”, “run.py”, “run.md”*
* ``wikipedia_research`` (1 minut) - *Otsi vastus lihtsale faktilisele küsimusele Wikipedia'st*
* ``oxdna_simple`` (9 minutit) - *Leia ja paranda viga molekulaarse dünaamilise simulatsiooni sisendfailides, mis kasutavad oxDNA teeki*
* ``munge_data`` (56 minutit) - *Kirjuta Pythoni skript, mis teisendab JSON formaadis andmeid ühest formaadist teise (näitefailide alusel)*
* ``cuda_backtesting`` (8 tundi) - *Kiirenda etteantud Python'i teeki aktsiatehingute tegemiseks ajalooliste tehinguandmete pealt, 
  kasutades teatud CUDA kernel'eid, jättes samaks kogu funktsionaalsuse, ning saavuta koodi kiirendamine 30% võrra.*

Sellel lähenemisel on kaks eelist:

1. see mõõdab ülesannete keerukust läbi selle, kaua inimspetsialistil kulub selle lahendamiseks - see muudab selle mõõdiku inimestele 
   intuitiivselt arusaadavaks;
2. see annab mõõdiku, mis skaleerub esimesest GPT-2 versioonist (mis suutis ainult lahendada ülesandeid, mis inimesel võtavad mõne sekundi)
   kuni praeguste tippmudeliteni (mille ajahorisont on mitmeid tunde) kuni tulevikumudeliteni, mille ajahorisont võib ulatuda nädalate või kuudeni.

Testid näitasid, et **50% edukuse tasemel**:

* on enamus Claude, Gemini, ja GPT tippmudeleid (graafik on august 2026 seisuga) ajahorisondiga **3–6 tundi**;
* erandiks on Claude Opus 4.6 (ajahorisont **12 tundi**) ja Claude Mythos Preview (ajahorisont **16 tundi** või enam, testide tulemused pole lõplikud).

Ja **80% edukuse tasemel**:

* on tippmudelid ajahorisondiga **1-2 tundi**;
* erandiks on Claude Mythos Preview, mille ajahorisont on **3 tundi**.

Järgnev graafik näitab, kuidas ajahorisont on arenenud aja jooksul (august 2026 seisuga). Horisontaal-teljel on mudeli avaldamise aeg ja 
vertikaal-teljel mudeli ajahorisondi pikkus. Valitud on 50% edukuse tase.

.. image:: /images/task-length-linear.png
   :alt: Aja horisondi diagramm

Põhiline järeldus METR uurimistööst oli see, et mudelite ajahorisont on laias laastus **kahekordistunud iga 4-7 kuuga** ning et see trend on olnud püsiv 
aastast 2019 kuni 2026-ni (kuigi tundub, et aastast 2023 alates on progress kiirenenud).
Seda on kõige parem näha järgnevast graafikust (see on sisuliselt sama graafik, kui eelmine; ent nüüd on vertikaaltelje skaala logaritmiline - see tähendab,
et ajalised väärtused vertikaalteljel kahekordistuvad iga teatud sammu tagant):

.. image:: /images/task-length-log.png
   :alt: Aja horisondi diagramm (logaritmiline skaala)

Ma soovitan ise katsetada ja uurida neid andmeid. Seda saab teha `METR veebilehel <https://metr.org/time-horizons/>`_ (kõige esimene graafik seal lehel).
Soovitan ka uurida graafikut 80% edukuse taseme jaoks. METR ise tõi oma uurimistöö tulemustes välja, et kasvu trend on olnud sarnane nii 
50% kui ka 80% edukuse taseme juures.

Mis järeldusi siit kõigest teha saab? Eeldame, et praegune eksponentsiaalne kasv jätkub ning mudelite ajahorisondi pikkus kahekordistub iga 7 kuuga.
See tähendaks, et 28 kuu pärast (november 2028) on toimunud 4 kahekordistumist (ehk 16x kasv), ning võiksime näha mudeleid saavutamas järgmisi tulemusi:

* 50% edukuse taseme juures lahendamas 8-24 päevase ajaaknaga ülesandeid;
* 80% edukuse taseme juures lahendamas 2-4 päevase ajaaknaga ülesandeid.

Ja veel 7 kuud hiljem, 2029. suvel, näeksime me AI mudeleid suutmas 50% edukuse taseme juures lahendada ülesandeid, mis varem 
võtsid inimspetsialistil terve kuu.

See trend on üks põhjustest, miks AI turvalisuse valdkonna spetsialistid hoiatavad, et me oleme väga kiiresti liikumas maailma, milleks me ei ole ühiskonnana 
valmis.

==========================================
Kui kindlad on eksperdid selles trendis?
==========================================

METR loodud ajahorisondi kriteerium on üks enim tsiteeritud mõõdikuid AI valdkonnas. Pole ühest konsensust, mis on kõige tõenäolisem 
kasvu kiirus (kahekordistumise ajasamm) praegusel hetkel (kas 4 kuud või 7 kuud) - üldiselt arvatakse, et see jääb pigem vahemikku 4-6 kuud.

Kriitikud on ka välja toonud, et see mõõdik keskendub liialt programmeerimisülesannetele; teised päris-elulised ülesanded ei pruugi järgida sama
kasvutrendi. METR `uuris ka seda <https://metr.org/blog/2025-07-14-how-does-time-horizon-vary-across-domains>`_ ja jõudis järeldusele, et teised 
valdkonnad kasvavad sarnasel viisil, aga kahekordistumise kiirus (ja praegune hetkeseis) erineb valdkonniti.

Oluline on siiski märkida, et see kasvutrend saab jätkuda vaid siis, kui seda kasvu toetavad tegurid ei muutu kardinaalselt. Vaatleme, mis viisil need tegurid 
võiksid muutuda.

=======================================
Mis tegurid võivad kasvutrendi muuta?
=======================================

On mitmeid tegureid, mis võivad olukorda drastiliselt muuta: teaduslikud läbimurded või piirangud, füüsilise maailmaga seotud pudelikaelad, finantsilised 
tegurid, või poliitilised otsused.

**Teadus - kiirendavad tegurid**. Kui näiteks leitakse uus AI arhitektuur, mis võimaldab mudelitel suurema püsivuse ja järjepidavusega tegeleda keeruliste 
ülesannetega, võib kasvutempo oluliselt kiireneda.

**Teadus - aeglustavad tegurid**. Valdkonnas on laialt levinud arusaam, et on 3 põhilist mõõdet mudelite võimekuse skaleerimiseks: mudelite parameetrite arvu
suurendamine, treeninguaja pikendamine, ning treeningandmete mahu (ja kvaliteedi) suurendamine. Seni on kõiki kolme mõõdet suurendatud üsna agressiivselt:

* **Mudelite parameetrite arv** on nüüdseks jõudnud triljoniteni (Kimi K3 mudelil on 2.8 triljonit parameetrit; OpenAI ja Anthropic hoiavad täpse parameetri arvu 
  salajasena, aga nende tippmudelitel on eeldatavasti rohkem parameetreid, kui Kimi K3 mudelil). Et saada ühte vastust Kimi K3 suurusega mudelilt, 
  on vaja arvutit, millel on 11.2 TB (!) mälu. Suuremad mudelid vajavad ka rohkem aega ja energiat, et vastuseid anda; samuti on nende treenimine 
  meeletult kulukas. See on üks põhjuseid, miks OpenAI ja Anthropic vajavad pidevalt järjest suuremaid summasid investeeringute näol.
* **Treeninguaega** on võimalik alati pikendada, kuid mingist punktist alates väheneb treenimise jätkamisest saadav kasu oluliselt.
* **Treeningandmete mahu** suurendamine ei ole samuti triviaalne. Juba Chat-GPT 3 (2020) treeniti suure koguse raamatute ja praktiliselt kogu interneti sisu peal,
  mida oli võimalik tolleks hetkeks kokku koguda. Värskete uute andmete saamiseks kasutavad firmad nüüd sünteetilisi andmeid ja inimekspertide käest kogutud 
  vastuseid (mille kogumine on kallim ja ajamahukam). Ülioluline on siin muidugi ka andmete kvaliteet ja unikaalsus.

On selge, et nende kõigi 3 mõõtme jätkuv skaleerumine on firmadele väljakutse.
Sellegipoolest oli huvitav kuulata Dario Amodei (firma Anthropic tegevjuht) `põhjendusi <https://www.youtube.com/watch?v=GrloGdp5wdc>`_ selle kohta,
miks tema arvates võiks praegune lähenemine skaleeruda vähemalt selle punktini, kuni me jõuame inimtasemele sarnase intelligentsuseni.
Samas tuleb muidugi tema nendesse väidetesse suhtuda kriitiliselt, kuna tal on tugev surve mitte öelda midagi, mis võiks nende investorite huvi 
vähendada.

**Füüsilise maailmaga seotud pudelikaelad**. Nõudlus arvutusvõimsuse järele üha kasvab, mis tekitab maailmas mälukiipide puudujäägi ning eeldab üha uute
arvutuskeskuste ehitamist. Samas on Ameerikas kasvutrendis `avalikkuse vastuseis <https://datacenteropposition.com/>`_ arvutuskeskuste väljaehitamisele.
Kui AI firmad ei saa piisavas mahus laieneda, peavad nad kasvutempot aeglustama ja/või investeerima uute (väiksemate) AI arhitektuuride 
loomisesse.

**Finantsilised tegurid**. Juhtivate AI firmade ärimudeli finantsiline elujõulisus on keeruline teema; on kriitikuid, kus kahtlevad, kas selline ärimudel
saab üldse olema jätkusuutlik. Nende ärimudel (mis eeldab järjest keerulisemate mudelite treenimist) vajab pidevat kapitali juurdevoolu. Sellega seoses 
tekib 2 probleemi:

1. Nad pole jõudnud veel isegi kasumlikkuse lähedale; üks kriitikutest, Ed Zitron, `koostas analüüsi <https://www.wheresyoured.at/the-openai-bubble/>`_, mis
   toob teravalt välja käärid praeguste LLM mudelite hinnakirjade vahel ning selle vahel, kui palju nad peaksid kasutuse eest raha küsima, et jõuda 
   rahavoogudega nulli.
2. Selleks, et juhtivad AI firmad saaksid jõuda kasumlikkuseni, peaksid nad vallutama suure osa tööturust; samas on näiteks Ameerikas 
   `kasvav vastumeelsus <https://hai.stanford.edu/ai-index/2026-ai-index-report/public-opinion>`_ sellele, milline mõju AI-l saab olema tööturule.

Loomulikult on erinevatel võimalikel finantsilistel sündmustel väga erinev mõju ulatus.

**Poliitilised tegurid**. Poliitilised otsused riikide tasemel või globaalselt võivad drastiliselt mõjutada arengutempot. Just hiljuti (29. juuli 2026)
`avaldati ühiskiri <https://www.pacingthefrontier.com/>`_ koos 1300+ allkirjaga juhtivate AI firmade töötajate poolt. Ühiskirjas nõuavad nad, et USA valitsus
püüaks luua rahvusvahelist lepet, et aeglustada AI mudelite arengut ja keskenduda ohutumate lahenduste leidmisele. See ei ole muidugi esimene kord, kui 
teadlased soovitavad AI arengu tempot aeglustada (`varasem näide <https://futureoflife.org/open-letter/pause-giant-ai-experiments/>`_). Kuid praegune ühiskiri
on tähelepanuväärne selle poolest, et allkirjastajate hulgas on palju OpenAI ja Anthropic'u töötajaid, sealhulgas Dario Amodei ise. OpenAI tegevjuht Sam Altman 
ei allkirjastanud küll seda pöördumist, kuid on avalikult avaldanud hiljuti 
`sarnaseid mõtteid <https://techcrunch.com/2026/07/28/sam-altman-is-ready-to-decelerate/>`_.
Kui eri riikide valitsused võtaksid riske tõsiselt ja teeksid koostööd, saaks AI progress muutuda oluliselt aeglasemaks ja kontrollitumaks. 
Kahjuks oleme me veel kaugel maailmast, kus selle jaoks oleks olemas piisav poliitiline tahe.

.. |up_exp| image:: /images/up_exp.png
   :alt: Eksponentsiaalne kasv kiireneb
.. |down_exp| image:: /images/down_exp.png
   :alt: Eksponentsiaalne kasv aeglustub
.. |down_linear| image:: /images/down_linear.png
   :alt: Kasv aeglustub lineaarseks
.. |up_exp_framed| image:: /images/up_exp.png
   :alt: Eksponentsiaalne kasv kiireneb
   :class: framed
.. |down_exp_framed| image:: /images/down_exp.png
   :alt: Eksponentsiaalne kasv aeglustub
   :class: framed
.. |down_linear_framed| image:: /images/down_linear.png
   :alt: Kasv aeglustub lineaarseks
   :class: framed

Järgnev tabel kirjeldab, kuidas need erinevad tegurid mõjutaksid arengutrende, kui need riskid või võimalused realiseeruksid. 
Lühiduse eesmärgil kasutan järgnevaid piltmärke:

* Kahekordistumise aeg lüheneks (ehk kiirem kasv) - |up_exp_framed|
* Kahekordistumise aeg pikeneks (ehk aeglasem kasv) - |down_exp_framed|
* Kasvutempo aeglustuks niivõrd, et muutuks lineaarseks - |down_linear_framed|

.. table:: 
    :widths: 15 16 69

    +-------------------------+---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+ 
    | Mõjutegur               |  Võimalik tagajärg                    |  Kommentaar                                                                                                                     |
    +=========================+=======================================+=================================================================================================================================+
    | Teaduslikud tegurid     | |up_exp| VÕI |down_exp|               | Läbimurded kiirendavad, pudelikaelad aeglustavad                                                                                |
    +-------------------------+---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
    | Füüsilised pudelikaelad | |down_exp|                            | Teguri mõju on aeglustav                                                                                                        |
    +-------------------------+---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
    | Finantsilised tegurid   | |down_exp| VÕI |down_linear|          | Teguri mõju tugevus varieerub; aeglustumine lineaarseks kasvuks saab realiseeruda vaid ekstreemsetel juhtudel (a la börsikrahh) |
    +-------------------------+---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
    | Poliitilised tegurid    | |down_exp| VÕI |down_linear|          | Kui jõutaks rahvusvahelise leppeni, siis selle mõju arengutrendidele saaks olla väga tugev                                      |
    +-------------------------+---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+

.. raw:: html

    <embed>
        <p style="line-height: 10px;">&nbsp;</p>
    </embed>

On selge, et on palju erinevaid faktoreid, mis mängivad rolli arengutempo muutmisel;
nende kõikide täpselt ennustamine on raske ülesannde isegi valdkonna ekspertidele.
See on põhjus, miks ma näen palju väärust sellel samal METR ajahorisondi graafikul - see on hea tööriist, kui `salvestada 
see endale järjehoidjaribale <https://metr.org/time-horizons/>`_ (i.k. *bookmarks*) ja vaadata tulemusi aeg-ajalt (või iga kord, kui uus oluline 
mudel avaldatakse).
METR plaanib jätkata selle lehe uuendamist iga kord, kui uus märkimisväärne mudel tehakse firmade poolt avalikuks ja saab METRi poolt testitud.

=================================
Kui on soov rohkem teada saada
=================================

Veel üks hea põhjus lugeda `METR ajahorisondi lehte <https://metr.org/time-horizons/>`_ on see, et ma libisesin selles postituses 
üle mõnest oluliselt täpsustusest, et hoida selle postituse pikkust mõistlikuna. 
Ma soovitan lugeda nende lehelt (vajadusel tõlget kasutades) "Korduma Kippuvaid Küsimusi" (i.k. *Frequently Asked Questions*), kus nad vastavad sellistele täpsustavatele küsimustele:

* Kas "ajahorisont" vastab ajavahemikule, mille jooksul AI agent saab tegutseda autonoomselt?
* Kas 8-tunnine ajahorisont tähendab, et AI saab automatiseerida kõiki töökohti?
* Miks mitte raporteerida ajahorisonti kõrgema edukuse taseme (näiteks 99%) juures?
* Kui te ütlete, et mudelil on 2-tunnine ajahorisont, kas see tähendab, et ta saab hakkama 50% kõigist 2-tunnistest ülesannetest, või seda,
  et iga 2-tunnine ülesanne on 50% edukuse määraga?

METR on avaldanud oma kodulehel ka palju muid uurimistulemusi; lisaks on neil e-maili uudiskiri, millega saab liituda (selle leidmiseks tuleb
kerida lehe allosani).

Lisaks on võimalik tutvuda ka METR'i algse teadusartikliga aastast 2025 ajahorisondi teemal:
https://arxiv.org/pdf/2503.14499
(kahjuks aga seda ei uuendata uute mudelite mõõtmistulemustega).

=====================
Kuhu edasi?
=====================

Selle postitus oli 1. osa AI arengu teemalisest artiklite seeriast. Keskendusin siin sellele, kuidas LLM'de ajaline järjepidevus on paranenud aja jooksul.
Samas on LLM'del teisi olulisi puudujääke, mida on vaja lahata:

* hoolimata sellest, et LLM'd on oluliselt edasi arenenud, jäävad nad tihti hätta üllatavate ülesannete juures, mis on inimestele väga lihtsad;
* LLM'del esinevad "hallutsinatsioonid" - ja neil esineb tihti seda, et nad "eksivad enesekindlalt" ja ei suuda enda vigu tunnistada.

Järgmistes postitustes keskendun nende kahe puudujäägi telgitagustesse. 
Muuhulgas puudutan seda, kuhu võib see kõik viia inimkonna tervikuna - ning jagan enda mõtteid selle kohta, kas tulevik on "kivisse raiutud" või on meil 
võimalik seda veel oluliselt kujundada oma tahte järgi.

.. raw:: html

    <embed>
        <p style="font-size: 0.9em;">Ja lõpetuseks, kuna ma usun, et avatus AI mudelite kasutamise osas on oluline (ja mu enda AI mudelite kasutus varieerub ajas):</p>
    </embed>

.. raw:: html

    <embed>
        <p class="ai-disclaimer"><b>Teave AI kasutamise kohta</b>: Selle postituse loomisel ei kasutatud AI mudeleid</p>
    </embed>
