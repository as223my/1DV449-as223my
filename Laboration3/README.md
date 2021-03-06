Länk till mashup-applikationen: https://anniesahlberg.se/Laboration3/

#Reflektionsfrågor

###Vad finns det för krav du måste anpassa dig efter i de olika API:erna?
Sveriges radio har inga restriktioner eller krav att anpassa sig efter vad jag kan se. Förutom att materialet inte får "användas på ett sådant sätt att det skulle kunna skada Sveriges Radios oberoende eller trovärdighet." (http://sverigesradio.se/api/documentation/v2/index.html)

För att använda sig av google maps javascript api behöver man en webbläsar nyckel som man skickar med i anropet (https://developers.google.com/maps/documentation/javascript/get-api-key). 

Det är gratis att använda sig av api:et så länge man inte överskrider 25000 uppladdningar av kartor under 24 timmar, 90 dagar i sträck. 

###Hur och hur länga cachar du ditt data för att slippa anropa API:erna i onödan?
Jag cachar trafikinformationen från sveriges radio i en fil på serven, med 5 minuters intervall. Detta för att inte belasta api:et, samtidigt ville jag inte vänta längre mellan cachningarna då viktig trafikinformation kan undgå användaren. 

###Vad finns det för risker kring säkerhet och stabilitet i din applikation?
Min applikation är helt beroende av att apierna fungerar som de skall, jag har förvisso implemterat felmeddelanden i koden som visas om något skulle gå snett. Men någon vidare funktion uppfyller inte min applikation om inte apierna samarbetar, tex om överbelastning uppstår.

Min applikation är också känslig för om namn eller siffror skulle ändra betydelse i datat från sveriges radios api. 

###Hur har du tänkt kring säkerheten i din applikation?
Applikationen saknar input fält, och känslig information i form av tex inloggning (databas). Vilket gör att applikationen inte är öppen för  attacker så som xss, sql-injections, csrf. 

###Hur har du tänkt kring optimeringen i din applikation?
För att öka prestandan cachar jag information från sveriges radio api. Jag har placerat min javascript fil i botten av body tagen i mitt dokument såväl som css är placerat i headern. Jag har även minifierat min javascript fil.  

#HTTP/2
För att förhindra att det uppstår blockeringar när för många http förfrågningar skickas samtidigt började man arbeta fram det som nu kallas HTTP/2 (baserat på spdy projektet).

HTTP/2 har fortfarande samma metoder, headers, statuskoder etc som HTTP 1.1 vilket gör att applikationer med HTTP 1.1 fortfarande kommer kunna fungera som vanligt. Det som bland annat gör att HTTP/2 blir snabbare att använda är att det inte blir någon blockering av för många förfrågningar detta tack vare att transporten mellan klient och server delas upp i små namngivna delar, så kallade frames som sedan sätts ihop igen vid ankomst.

Detta kallas multiplexing, andra fördelar är också att headers kan komprimeras och att filer kan skickas till webbläsaren innan en förfrågan skickas (server push).
