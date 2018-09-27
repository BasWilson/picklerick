# Rick and Morty API in gebruik.

## Informatie bronnen

#### API's & libraries
[The Rick and Morty API](https://rickandmortyapi.com/)

[Jquery](https://jquery.com/)


## De opdracht

#### Opdracht

Door middel van `The Rick and Morty API` een overzicht maken van alle Rick and Morty figuren.

#### Eisen

- [x] Afbeelding
- [x] Naam
- [x] Status
- [x] Soort
- [x] Geslacht
- [x] Oorsprong
- [x] Laatste locatie
- [x] Laatste aflevering (nummer en naam)


#### Bonus
- [x] README.md
- [x] Scalability
- [x] Kunnen doorklikken voor info op episodes, dimensies, etc

## Hoe is het gemaakt?

#### Wie wat waar.
Er is gebruik gemaakt van HTML voor markup, CSS voor de styling en JavaScript voor het ophalen en verwerken van de data van de API.

#### Ophalen van de data
The Rick and Morty API maakt gebruik van .JSON bestanden om de data te bewaren. Met behulp van Jquery kan je JSON data ophalen en uitlezen. Hier een voorbeeld om de API op te halen met Jquery.

```
$.getJSON( `https://rickandmortyapi.com/api/`, { // De link die het .JSON bestand bevat
  format: "json"
})
  .done(function( apiData ) { // Wanneer de data binnen is, kan je er mee doen wat je wil.

      characters = apiData; // We slaan de data op in het characters variable
});
```

Dit doen we ook voor de epiodes en locaties.

#### Verwerken van de data
Wanneer we de data eenmaal hebben opgehaald kunnen we het nu gewoon simpel gezegd appenden aan een `<div>` op de HTML pagina. Dit gebeurt met JavaScript. Laten we de foto van een figuur uitlezen en appenden.
```
// De foto halen we uit het eerder gemaakte characters variabele
const img = `<img src="${characters.characters[i].image}" />`; 

// Dan appenden we de foto aan een div in de HTML
$('<div>').append(`<div>${img}</div>`);
```
Dit doe je dan voor alle verschillende data, todat het compleet is.

#### Het navigatie systeem
Het characters gedeelte van de API bestaat uit veel figuren, die zijn verdeeld over pagina's in aparte .JSON betanden. Dus we moeten een manier vinden om door de pagina's heen te navigeren op een goede manier.

Door twee knoppen te maken om te navigeren kunnen we dit vrij simpel doen.
Als de pagina is geladen, starten we op pagina 1, en uit de data van de API halen we op hoeveel pagina's er totaal zijn. Met die data kan je een leuk navigatie systeem maken. 
```
function SwitchPage (page) {

    if (page == 'next') {
        if (settings.page < characters.info.pages) {
            settings.page++;
            settings.set = true;
            SetNavButtons(); // De visuele delen mooi doen
            GetAllCharacters(); // De characters opnieuw ophalen van die pagina
        }
    } else if (page == 'previous') {
        if (settings.page > 1) {
            settings.page--;
            settings.set = true;
            SetNavButtons();
            GetAllCharacters();
        }
    }
}
```
OnClick van een knop roepen we die functie aan met een parameter om aan te geven of we vooruit gaan of achteruit.
Dan laden we de figuren van de nieuwe pagina.
