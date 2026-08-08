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
      <p class="show_if_not_teaser"; style="display:none;"><strong>Märkus</strong>. <em>Enamus mudelitest, mida me siin postituses käsitleme, on 
      LLM-d ("Large Language Model"). Kui me soovime rääkida spetsiifiliselt neist, kasutame me terminit "LLM"; terminit "AI" kasutame, et 
      rääkida üleüldiselt võimalikest AI süsteemidest ja arhitektuuridest (s.h. neist, mida pole veel leiutatud).</em></p>
    </embed>

Viimasel ajal tundub AI olevat täitnud kõik uudiskanalite pealkirjad. Aga kuidas eristada tõde liialdustest? 
Uudisteartiklid on tihti segased või kallutatud. 
Kõrvuti võib leida artikleid pealkirjadega "AI asendab kõik tööd 2 aasta jooksul" ja "AI mull on kohe lõhkemas".
On selge, et ekstreemsemad pealkirjad müüvad paremini - ükskõik, kuhu poole parajasti tõde kallutatud pole.

Lisaks võib AI mudelite progress tunduda ebakorrapärane ka valdkonna eksperdile - kiire arengu perioodid vahelduvad aeglastega.
Et saada selgemat ülevaadet, tuleb vaadata kaugemalt, üle pikema ajaraami. 
See on täpselt see, mida organisatsioon `METR <https://metr.org/>`_ tegi (METR on mittetulunduslik uurimisinstituut Californias). 

.. TEASER_END

=====================
Arengu mõõtmine
=====================

METR märkas, et üks AI mudelite probleemidest (eriti LLM-de puhul) on järjepidavuse puudumine - neil võib olla väga raske 
läbida pikaajalisi või mitme-sammulisi ülesandeid ilma järge kaotamata. See järeldus aitas neil defineerida ühe efektiivse
mõõdupuu: kui ajaliselt keerukate (inimesel lahendamiseks kuluva aja mõttes) ülesannetega saab mudel hakkama teatud fikseeritud 
tõenäosusega (nt 50% või 80%)? Nad andsid sellele mõõdikule nime **ülesannete läbimise ajahorisont** (i.k. "task completion
time horizon").

METR koostas nimekirja 228 erineva ülesandega (tarkvaraarenduse, küberturvalisuse, üldise loogika, ja masinõppe valdkonnast).
Ülesanded varieeruvad triviaalsetest (lahendatav sekunditega) kuni ülesanneteni, mille lahendamiseks kulub enda valdkonna
spetsialistil mitmeid päevi.

Here are some examples of the tasks from the software engineering field:

* ``find_shell_script`` (3 seconds) - *“Milline neist failidest on shell skript?” Valikud: “run.sh”, “run.txt”, “run.py”, “run.md”*
* ``wikipedia_research`` (1 minute) - *Otsi vastus lihtsale faktilisele küsimusele Wikipedia'st*
* ``oxdna_simple`` (9 minutes) - *Leia ja paranda viga molekulaarse dünaamilise simulatsiooni sisendfailides kasutades oxDNA teeki*
* ``munge_data`` (56 minutes) - *Kirjuta Pythoni skript, mis teisendab JSON formaadis andmeid ühest formaadist teise (näitefailide alusel)*
* ``cuda_backtesting`` (8 hours) - *Kiirenda etteantud Python'i teeki aktsiatehingute tegemiseks ajalooliste tehinguandmete pealt, 
  kasutades teatud CUDA kernel'eid, jättes samaks kogu funktsionaalsuse, ning saavuta koodi kiirendamine 30% võrra.*

Sellel lähenemisel on kaks tugevust:

1. see mõõdab ülesannete keerukust läbi selle, kaua inimspetsialistil kulub selle läbimiseks, mis see muudab selle mõõdiku inimestele 
   intuitiivselt arusaadavaks;
2. see annab mõõdiku, mis skaleerub esimesest GPT-2 versioonist (mis suutis ainult lahendada ülesandeid, mis inimesel võtab mõned sekundid)
   kuni praeguste tippmudeliteni (mille ajahorisont on mitmeid tunde) kuni tulevikumudeliteni, mille ajahorisont võib olla isegi nädalates või kuudes.

Testid näitasid, et **50% edukuse tasemel**:

* enamus Claude, Gemini, ja GPT tippmudeleid (august 2026 seisuga) on ajahorisondiga **3–6 tundi**;
* erandiks on Claude Opus 4.6 (ajahorisont **12 tundi**) ja Claude Mythos Preview (ajahorisont **16 tundi** või enam, testide tulemused pole lõplikud).

Ja **80% success level**:

* tippmudelid on ajahorisondiga **1-2 tundi**;
* erandiks on Claude Mythos Preview, mille ajahorisont on **3 tundi**.

Järgnev graafik näitab, kuidas ajahorisont on arenenud aja jooksul (august 2026 seisuga). Horisontaal-teljel on mudeli avaldamise aeg ja 
vertikaal-teljel mudeli ajahorisondi pikkus. Valitud on 50% edukuse tase.

.. image:: /images/task-length-linear.png

|

Ma soovitan ise katsetada ja mängida nende numbritega. Seda saab teha `METR veebilehel <https://metr.org/time-horizons/>`_ (esimene graafik seal lehel).
Seal saab valida 50% ja 80% edukuse taseme vahel, ning samuti vaadelda tulemusi eri skaaladel (lineaarne vs logaritmiline).

Põhiline järeldus METR uurimistööst oli see, et mudelite ajahorisont on laias laastus **kahekordistunud iga 4-7 kuuga** ning et see trend on olnud püsiv 
aastast 2019 kuni 2026-ni (kuigi tundub, et aastast 2023 alates on progress kiirenenud).
Oluline on märkida, et kasvu tempo on olnud sarnane nii 50% kui ka 80% edukuse taseme juures.

Mis järeldusi siit teha saab? Eeldame, et praegune eksponentsiaalne kasv jätkub ning mudelite ajahorisondi pikkus kahekordistub iga 7 kuuga.
See tähendaks, et 28 kuu pärast (November 2028) on toimunud 4 kahekordistumist (ehk 16x kasv), ning me näeksime mudeleid:

* 50% edukuse taseme juures lahendamas 8-24 päevase ajaaknaga ülesandeid;
* 80% edukuse taseme juures lahendamas 2-4 päevase ajaaknaga ülesandeid.

Ja veel 7 kuud hiljem, 2029. suvel, näeksime me AI mudeleid suutmas lahendada ülesandeid (50% edukuse tasemega), mis varem 
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
valdkonnad kasvavad sarnasel kujul, aga kahekordistumise kiirus (ja praegune hetkeseis) erineb valdkonniti.

Oluline on siiski märkida, et see kasvutrend saab jätkuda vaid siis, kui seda kasvu toetavad tegurid ei muutu kardinaalselt. Uurime, mis viisil need tegurid 
võiksid muutuda.

=======================================
Mis tegurid võivad kasvutrendi muuta?
=======================================

On mitmeid tegureid, mis võivad olukorda drastiliselt muutuda: teaduslikud läbimurded või piirangud, füüsilise maailmaga seotud pudelikaelad, finantsilised 
põhjused, või poliitilised otsused.

**Teadus - kiirendavad tegurid**. Kui avastatakse uus AI arhitektuur, mis võimaldab mudelitel tegeleda suurema püsivuse ja järjepidavusega tegeleda keeruliste 
ülesannetega, võib kasvutempo oluliselt kiireneda.

**Teadus - aeglustavad tegurid**. Valdkonnas on laialt levinud teadmine, et on 3 põhilist mõõdet mudelite võimekuse skaleerimiseks: mudelite parameetrite arvu
suurendamine, treeninguaja pikendamine, ning treeningandmete mahu (ja kvaliteedi) suurendamine. Seni on kõiki kolme mõõdet suurendatud üsna agressiivselt:

* Mudelite parameetrite arv on nüüdseks jõudnud triljoniteni (Kimi K3 mudelil on 2.8 triljonit parameetrit; OpenAI ja Anthropic hoiavad täpse parameetri arvu 
  salajasena, aga nende tippmudelitel on eeldatavasti parameetreid, kui Kimi K3 mudelil). Et saada ühte vastust mudelilt, mis on nii suur kui Kimi K3, on vaja
  arvutit, millel on 11.2 TB (!) mälu. Suuremad mudelid vajavad ka rohkem aega ja energiat, et vastuseid anda; ja nende treenimine on meeletult kulukas.
  See on üks põhjuseid, miks OpenAI ja Anthropic vajavad pidevalt järjeset suuremaid summasid investeeringuna.
* Treeninguaega on võimalik alati pikendada, kuid mingist punktist alates väheneb treenimise jätkamisest saadav kasu oluliselt.
* Treeningandmete mahu suurendamine ei ole samuti triviaalne. Juba Chat-GPT 3 (2020) treeniti suure koguse raamatute ja praktiliselt kogu interneti sisu peal,
  mida oli võimalik tolleks hetkeks kokku koguda. Värskete uute andmete saamiseks kasutavad firmad nüüd on sünteetilisi andmeid ja inimekspertide käest kogutud 
  vastuseid. Ülioluline on siin muidugi ka andmete kvaliteet ja unikaalsus.

On selge, et nende kõigi 3 mõõtme jätkuv skaleerumine on firmadele väljakutse.
Sellegipoolest esitas Dario Amodei (Anthropic'u tegevjuht) ühes `hiljutises intervjuus <https://www.youtube.com/watch?v=GrloGdp5wdc>`_ huvitavaid põhjendusi,
miks tema arvates võiks praegune lähenemine skaleeruda vähemalt selle punktini, kuni me jõuame inim-taseme intelligentsuseni.
Samas tuleb muidugi tema nendesse väidetesse suhtuda kriitiliselt, kuna tal on taga tugev surve mitte öelda midagi, mis võiks nende investorite huvi 
vähendada.

**Füüsilise maailmaga seotud pudelikaelad**. Nõudlus arvutusvõimsuse järele üha kasvab, mis tekitab maailmas mälukiipide puudujäägi ning eeldab üha uute
arvutuskeskuste ehitamist. Samas on Ameerikas kasvutrendis `avalikkuse vastuseis <https://datacenteropposition.com/>`_ arvutuskeskuste väljaehitamisele.
Kui AI firmad ei saa piisavas mahus laieneda, peavad nad kasvutempot aeglustama ja/või investeerima uute väiksemate AI arhitektuuride 
loomisesse.

**Finantsilised põhjused**. Juhtivate AI firmade ärimudeli finantsiline elujõulisus on keeruline teema; on kriitikuid, kus kahtlevad, kas selline ärimudel
saab üldse olema jätkusuutlik. Nende ärimudel (mis eeldab järjest keerulisemate mudelite treenimist) vajab pidevat kapitali juurdevoolu. Sellega seoses 
tekib 2 probleemi:

1. Nad pole jõudnud veel isegi kasumlikkuse lähedale; üks kriitikutest, Ed Zitron, `koostas analüüsi <https://www.wheresyoured.at/the-openai-bubble/>`_, mis
   toob teravalt välja käärid praeguste LLM mudelite hinnakirjade vahel ning selle vahel, kui palju nad peaksid maksma, et mitte olla kahjumlikud.
2. Selleks, et juhtivad AI firmad saaksid jõuda kasumlikkuseni, peaksid nad vallutama suure osa tööturust; samas on näiteks Ameerikas 
   `kasvav vastumeelsus <https://hai.stanford.edu/ai-index/2026-ai-index-report/public-opinion>`_ selle osas, mis mõju AI-l saab olema tööturul.

Kui rääkida võimalike finantsiliste sündmuste mõjust AI arengukiirusele, siis mõju tugevus ulatub väikesemõjulisest (..) väga suuremõjulisteni (..).

+++

Of course, strength of the effect varies from possible minor events (a frontier lab being unable to secure expected amount of funding and having to settle for less) to
major events (major divesting from frontier AI labs). 

**Policy reasons**. Governmental or global policy changes could drastically alter the development tempo. Curiously, just recently (July 29, 2026) a statement 
`was released <https://www.pacingthefrontier.com/>`_ by 1300+ employees of frontier AI labs requesting a global slowdown of AI development. Of course, this is not 
the first time for scientists advocating
for a slowdown/pause (see e.g. `here <https://futureoflife.org/open-letter/pause-giant-ai-experiments/>`_). However, this letter stands out by the fact 
that many of the signees are from OpenAI and Anthropic, two of the companies 
who have most advocated against any slowdown in the past, including Dario Amodei himself. CEO of OpenAI, Sam Altman, has not signed the 
letter, but has publicly made `similar comments <https://techcrunch.com/2026/07/28/sam-altman-is-ready-to-decelerate/>`_. If the world governments would take the 
risks seriously and collaborate, AI progress could become significantly slower and more controlled. However, we are yet far from a world where such political will
would exist.

.. |up_exp| image:: /images/up_exp.png
.. |down_exp| image:: /images/down_exp.png
.. |down_linear| image:: /images/down_linear.png
.. |up_exp_framed| image:: /images/up_exp.png
  :class: framed
.. |down_exp_framed| image:: /images/down_exp.png
  :class: framed
.. |down_linear_framed| image:: /images/down_linear.png
  :class: framed

Let's take a look at how those diverse factors could affect the trends if the risks/possibilities realize. We use small pictograms for brevity:

* The doubling time would decrease (faster growth) - |up_exp_framed|
* The doubling time would increase (slower growth) - |down_exp_framed|
* The growth would slow down to become linear - |down_linear_framed|

======================= ======================================= ==============================================================================================
Factor                  Potential consequence                   Comments
======================= ======================================= ==============================================================================================
Scientific factors      |up_exp| OR |down_exp|                  Breakthroughs speed up, scaling bottlenecks slow down
Physical bottlenecks    |down_exp|                              Likely will cause a weak slowdown for frontier AI labs
Financial reasons       |down_exp| OR |down_linear|             Strength of slowdown effect varies; slowdown to linear may only occur in extreme scenarios
Policy reasons          |down_exp| OR |down_linear|             If a national/global slowdown is agreed upon, it could significantly slow down development
======================= ======================================= ==============================================================================================

.. raw:: html

    <embed>
        <p style="line-height: 10px;">&nbsp;</p>
    </embed>

It is evident that there are a lot of factors that may play a role in determining what the rate of the progress is; 
and reliably predicting them is a difficult task even for experts.
However, this is why I think the METR time horizon graph is such a good tool to have: one can `bookmark it <https://metr.org/time-horizons/>`_ and review
it whenever some new model launches and is being hyped - METR will keep updating it when new notable models are released.

==========================
If you want to learn more
==========================

Another reason to read the `METR time horizons page <https://metr.org/time-horizons/>`_ is that I skipped over many important caveats to keep the length of this blog post reasonable.
So I recommend scrolling to the "Frequently Asked Questions" section in their page and read their answers to clarifying questions such as:

* Does “time horizon” mean the length of time that current AI agents can act autonomously?
* Does an 8-hour time horizon mean that AI can automate all jobs?
* Why not report the time horizon at a higher reliability level (e.g. time horizon at 99% success rate)?
* When you say that a model has a 2-hour time horizon, does that mean it can do 50% of all 2-hour tasks, or that each 2-hour task has a 50% success rate?

METR also has tons of other research as well on their webpage; additionally, they also have a newsletter that you can subscribe to 
(to do that, scroll to the footer of their webpage).

If you prefer reading information in the form of a scientific paper, check out the original METR paper from 2025 instead 
(obviously, this is not being updated with statistics about the latest models):
https://arxiv.org/pdf/2503.14499

=====================
What's next?
=====================

The title of this post was "Where is AI heading - part 1/3". This is because while we focused on how coherence of LLMs
is increasing over time, there are other fundamental shortcomings of LLMs that need to be explored as well:

* even after all the progress, LLMs often fail in surprising ways at tasks that are trivial to humans;
* LLMs have hallucinations - and they are often confidently wrong, and fail to admit mistakes.

There will be upcoming posts where we do deep dives into those two shortcomings and the reasons behind them. 
Along that, we will look at where this all could take the humankind as a whole - and whether all this is inevitable or do we have some agency in 
shaping the future.

.. raw:: html

    <embed>
        <p style="font-size: 0.9em;">And finally, because I believe that transparency about AI usage is important, and my usage of AI tools varies:</p>
    </embed>

.. raw:: html

    <embed>
        <p class="ai-disclaimer"><b>Disclaimer of AI usage</b>: AI was not used in writing this blog post.</p>
    </embed>
