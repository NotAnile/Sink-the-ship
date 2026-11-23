#Sänka skepp spel
#Elina Tran

#Skriver ut instruktioner och grafik
def start():
    titel = 'SÄNKA SKEPP'
    print('-'*50 + '\n|' + titel.center(46) + ' '*2 + '|')
    print('|                               ☀               |\n'
          '|        |▻                                      |\n'
          '|      __|___      .     ~           ◀|          |\n'
          '|   ~  \____/                 .    ___|___       |\n'
          '|              〰                  \_____/       |')
    print('-'*50, '\n')
    
    instruktioner = 'Instruktioner'
    print(instruktioner.center(45), '\n')
    print('''1. Två spelare placerar i hemlighet ut 6 skepp med olika storlekar på varsin 9x9 spelplan:
Jollar - 2 rutor
Briggar - 3 rutor
Galärer - 4 rutor
Fullriggare - 5 rutor

Spelare 1 börjar med att lägga ut alla sina skepp. Sedan är det spelare 2 tur.

2. Försök att sänka varandras skepp genom att turas om att skjuta på rutor som anges med koordinater.

3. x = Träff
   ~ = Miss
   
4. Om spelaren träffar ett skepp så får den köra igen.
   Missar man blir det motståndarens tur.

5. Spelaren som sänker alla motståndarens skepp först vinner.
--------------------------------------------------------------''', '\n', '\n')
            
    
        
#Bygger vår 9x9 spelbräda
#p1 = spelare 1 och p2 = spelare 2
p1_bräda = [['O' for i in range(9)] for j in range(9)]
p2_bräda = [['O' for i in range(9)] for j in range(9)]

p1_alla_skepp = []
p2_alla_skepp = []

p1_gissningar = []
p2_gissningar = []

p1_skeppträff = []
p2_skeppträff = []

p1_antal_sänkt_skepp = 0
p2_antal_sänkt_skepp = 0

p1_antal_koordinater = 0
p2_antal_koordinater = 0

spelare_tur = 0

#Skriver ut spelbrädorna
def skriva_ut_spelbräda(p1_bräda, p2_bräda):
    global spelare_tur
    
    #Växlar spelare
    if spelare_tur%2 == 0:
        bräda = p1_bräda
        
    else:
        bräda = p2_bräda
        
    print(' ', 1, 2, 3, 4, 5, 6, 7, 8, 9)

    for rad in range(0,9):
        print(rad+1, end=' ')
        for kolumn in range(0, 9):
            print(bräda[rad][kolumn], end=' ')
            
        print('\n', end='')   
            
        
#Spelarna placerar skeppen genom att ange startkoordinaterna, typ av skepp och riktning (lodrät eller vågrät)
#Koordinaterna sparas i tredimensionella listor
def placera_skepp(p1_alla_skepp, p2_alla_skepp):
    global spelare_tur
    global p2_antal_koordinater
    global p1_antal_koordinater
    skepp_kontroll = 1
    
    #Växlar spelare
    if spelare_tur%2 == 0:
        print('Spelare 1\n')
        spelare = p1_alla_skepp
        koordinaträknare = p1_antal_koordinater
        
    else:
        print('Spelare 2\n')
        spelare = p2_alla_skepp
        koordinaträknare = p2_antal_koordinater
        
    while skepp_kontroll < 7:
        skepp = []
        skeppkoordinat = []
        
        #Kollar undantag
        skepp_startrad = input('Ange raden du vill placera skepp' + ' ' + str(skepp_kontroll) + ' på (1-9): ')
        
        if not skepp_startrad:
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        elif len(skepp_startrad) > 1:
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        elif skepp_startrad not in '123456789':
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        skepp_startkolumn = input('Ange kolumn: ')
        print('\n')
        
        if not skepp_startkolumn:
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        elif len(skepp_startkolumn) > 1:
            print('Skriv en siffra mellan 1-9!\n')
            continue
            
        elif skepp_startkolumn not in '123456789':
            print('Skriv en siffra mellan 1-9!\n')
            continue
            
        skepp_startrad = int(skepp_startrad)
        skepp_startkolumn = int(skepp_startkolumn)
        
        skeppkoordinat.append(skepp_startrad)
        skeppkoordinat.append(skepp_startkolumn)
        
        #Kollar om det redan ligger ett skepp på koordinaten som man valt
        finns_skepp = 0
        for antal in range(len(spelare)):
            for koordinat in range(len(spelare[antal])):
                if skeppkoordinat == spelare[antal][koordinat]:
                    print('Det ligger redan ett skepp där!\n')
                    finns_skepp += 1
                    
        if finns_skepp > 0:
            continue
        
        skepp.append(skeppkoordinat)
        
        riktning = input('Vill du lägga det lodrät eller vågrät(l/v)? ')
        riktning = riktning.lower()
        
        #Kollar undantag
        if not riktning:
            print('Skriv l eller v!\n')
            continue
        
        elif len(riktning) > 1:
            print('Skriv l eller v!\n')
            continue
        
        elif riktning not in 'lv':
            print('Skriv l eller v!\n')
            continue
        
        skepptyp = input('Välj mellan: Jolle - 2 rutor (J), Brigg - 3 (B), Galär - 4 (G) eller Fullriggare - 5 (F): ')
        skepptyp = skepptyp.upper()
        print('\n')

        #Kollar undantag
        if not skepptyp:
            print('Välj mellan J, B, G, eller F!\n')
            continue
        
        elif len(skepptyp) > 1:
            print('Välj mellan J, B, G, eller F!\n')
            continue
        
        elif skepptyp not in 'JBGF':
            print('Välj mellan J, B, G, eller F!\n')
            continue
        
        #Tilldelar varje typ av skepp ett värde för antalet rutor de tar upp
        skeppvärde = {'J': 2, 'B': 3, 'G': 4, 'F': 5}
        
        #If-satsen kollar om de har lagt skeppet lodrät
        #Loopen fyller in de koordinater som spelaren inte har skrivit
        utanför_karta = 0
        if riktning == 'l':
            for koordinater_rad in range(skepp_startrad+1, skeppvärde[skepptyp]+skepp_startrad):
                skeppkoordinat = []
                skeppkoordinat.append(koordinater_rad)
                skeppkoordinat.append(skepp_startkolumn)
                skepp.append(skeppkoordinat)
                
                finns_skepp = 0
                
                #Kollar undantag
                if koordinater_rad > 9:
                    print('Skeppet ligger utanför kartan! Se till att den ligger innanför.')
                    utanför_karta += 1
                    break

                for antal in range(len(spelare)):
                    for koordinat in range(len(spelare[antal])):
                        if skeppkoordinat == spelare[antal][koordinat]:
                            print('Det ligger redan ett skepp emellan på', skeppkoordinat)
                            finns_skepp += 1
                            break
                        
                    if finns_skepp > 0:
                        break
                
                if finns_skepp > 0:
                    break
                
        if finns_skepp > 0:
            continue
        
        if utanför_karta > 0:
            continue
                
        #Kollar om skeppet är placerat vågrät
        elif riktning == 'v':
            for koordinater_kolumn in range(skepp_startkolumn+1, skeppvärde[skepptyp]+skepp_startkolumn):
                skeppkoordinat = []
                skeppkoordinat.append(skepp_startrad)
                skeppkoordinat.append(koordinater_kolumn)
                skepp.append(skeppkoordinat)
                
                finns_skepp = 0
                
                #Kollar undantag
                if koordinater_kolumn > 9:
                    print('Skeppet ligger utanför kartan! Se till att den ligger innanför.')
                    utanför_karta += 1
                    break
                
                for antal in range(len(spelare)):
                    for koordinat in range(len(spelare[antal])):
                        if skeppkoordinat == spelare[antal][koordinat]:
                            print('Det ligger redan ett skepp emellan på', skeppkoordinat)
                            finns_skepp += 1
                            break
                        
                    if finns_skepp > 0:
                        break
                
                if finns_skepp > 0:
                    break
                
        if finns_skepp > 0:
            continue
                
        if utanför_karta > 0:
            continue
        
        koordinaträknare += len(skepp)
        
        if spelare_tur%2 == 0:
            p1_antal_koordinater = koordinaträknare
            
        else:
            p2_antal_koordinater = koordinaträknare
            
        skepp_kontroll += 1
        spelare.append(skepp)
        
    spelare_tur += 1
    
#Funktionen låter spelarna skjuta på varandras skepp
def gissningar(p1_bräda, p2_bräda, p1_gissningar, p2_gissningar, p1_alla_skepp, p2_alla_skepp):
    global spelare_tur
    global skjut_koordinat
    #Loopen gör att spelarna får ange rad och kolumn de vill skjuta på och kollar om det är en träff
    #Om det är en träff anropas skepp_träff
    while True:
        skeppträff = 0
        #Växlar spelare
        if spelare_tur%2 == 0:
            print('Spelare 1')
            #Spelare = motståndarens skepps lista för det är motståndaren man skjuter
            #Då jämförs spelarens gissning med motståndarens skeppskoordinater
            spelare = p2_alla_skepp
            bräda = p1_bräda
            gissning = p1_gissningar
            skriva_ut_spelbräda(p1_bräda, p2_bräda)
        
        else:
            print('Spelare 2')
            spelare = p1_alla_skepp
            bräda = p2_bräda
            gissning = p2_gissningar
            skriva_ut_spelbräda(p1_bräda, p2_bräda)
        
        skjut_koordinat = []
        skjut_rad = input('Ange raden du vill skjuta på: ')
        
        #Kollar undantag
        if not skjut_rad:
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        elif skjut_rad not in '123456789':
            print('Skriv en siffra mellan 1-9!\n')
            continue
        
        skjut_kolumn = input('Ange kolumn: ')
        print('\n')
        
        if not skjut_kolumn:
            print('Skriv en siffra mellan 1-9!\n')
            continue
            
        elif skjut_kolumn not in '123456789':
            print('Skriv en siffra mellan 1-9!\n')
            continue
            
        skjut_rad = int(skjut_rad)
        skjut_kolumn = int(skjut_kolumn)
        
        skjut_koordinat.append(skjut_rad)
        skjut_koordinat.append(skjut_kolumn)
        
        if skjut_koordinat in gissning:
            print('Du har redan gissat på detta!')
            continue
        
        gissning.append(skjut_koordinat)
        
        #Ersätter brädan med x vid träff eller ~ vid miss
        for antal in range(len(spelare)):
            for koordinat in range(len(spelare[antal])):
                if skjut_koordinat == spelare[antal][koordinat]:
                    bräda[skjut_rad-1][skjut_kolumn-1] = 'x'
                    skeppträff += 1
                    break
                    
                else:
                    bräda[skjut_rad-1][skjut_kolumn-1] = '~'
                    
            if skeppträff > 0:
                break
            
        #Kallar på funktionen som skriver ut spelbrädan
        skriva_ut_spelbräda(p1_bräda, p2_bräda)
        if skeppträff > 0:
            print('Träff!\n')
            skepp_träff(p1_alla_skepp, p2_alla_skepp)
            
        #Miss ger skeppträff == 0 så om man träffar får man köra igen
        elif skeppträff == 0:
            print('Miss!\n')
            spelare_tur += 1
        
        #Kollar om antalet koordinater som man har träffat är lika många som alla skeppens koordinater tillsammans
        #Om det är lika många betyder det att man har tagit ner alla skepp
        if p1_antal_sänkt_skepp == 6:
            print('Grattis spelare 1! Du vann!')
            break
        
        elif p2_antal_sänkt_skepp == 6:
            print('Grattis spelare 2! Du vann!')
            break
        
#Funktionen tar hand om alla träffar och kollar om det är sänkt skepp
def skepp_träff(p1_alla_skepp, p2_alla_skepp):
    global p1_antal_sänkt_skepp
    global p2_antal_sänkt_skepp
    
    global p1_skeppträff
    global p2_skeppträff
    
    if spelare_tur%2 == 0:
        #Spelare = motståndarens skepps lista för det är motståndaren man skjuter på
        spelare = p2_alla_skepp
        träff = p1_skeppträff
        antal_sänkt_skepp = p1_antal_sänkt_skepp
        
    else:
        spelare = p1_alla_skepp
        träff = p2_skeppträff
        antal_sänkt_skepp = p2_antal_sänkt_skepp
    
    träff.append(skjut_koordinat)
    träff = sorted(träff)
    
    #Looparna jämför koordinaterna och kollar om man har sänkt ett helt skepp
    for skepp in range(len(spelare)):
        #Variabeln kontrollerar så att antalet koordinater ett skepp består av = antalet koordinater man har träffat rätt på
        #så den kan avgöra om man har sänkt ett skepp
        antal_träffar = 0
        index = []
        
        for koordinater in range(len(spelare[skepp])):
            pop_räknare = 0
            #träff[träffar] är spelarens koordinater där de har träffat ett skepp och jämförs med äkta skeppens koordinater
            #Om de är lika så sparas positionen i index = []
            for träffar in range(len(träff)):
                if träff[träffar] == spelare[skepp][koordinater]:
                    antal_träffar += 1
                    index.append(träff.index(träff[träffar]))
                    index = sorted(index)
                
                #Vid sänkt skepp tas alla koordinater som tillhör det skeppet bort i träfflistan
                #Detta är så att loopen inte kollar på samma sänkt skepp nästa gång loopen körs
                if antal_träffar == len(spelare[skepp]):
                    print('Sänkt skepp! \n')
                    antal_sänkt_skepp += 1
                    
                    for plats in index:
                        träff.pop(plats-pop_räknare)
                        pop_räknare += 1

                    break
                
            if antal_träffar == len(spelare[skepp]):
                break
            
        if antal_träffar == len(spelare[skepp]):
            break
        
    if spelare_tur%2 == 0:
        p1_skeppträff = träff
        p1_antal_sänkt_skepp = antal_sänkt_skepp
        
    elif spelare_tur%2 != 0:
        p2_skeppträff = träff
        p2_antal_sänkt_skepp = antal_sänkt_skepp

start()
placera_skepp(p1_alla_skepp, p2_alla_skepp)
placera_skepp(p1_alla_skepp, p2_alla_skepp)
gissningar(p1_bräda, p2_bräda, p1_gissningar, p2_gissningar, p1_alla_skepp, p2_alla_skepp)






