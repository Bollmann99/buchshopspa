<template>
    <main>

        <form>
            <label for="fname">Vorname:</label><br>
            <input type="text" id="fname" name="fname" minlenght="2" size="25" required
                placeholder="Agustin Ignacio"><br>
            <label for="lname">Nachname:</label><br>
            <input type="text" id="lname" name="lname" minlenght="2" size="25" required
                placeholder="Calvimontes Bollmann"><br>
            <label for="email">Email:</label><br>
            <input type="email" id="email" name="email1" required placeholder="ignaciobollmann@outlook.de"
                size="25"><br>
            <label for="strasse">Strasse:</label><br>
            <input type="text" id="strasse" name="strasse1" maxlenght="50" size="25" placeholder="Holzhofgasse 1"><br>
            <label for="ort">Ort:</label><br>
            <input type="text" id="ort" name="ort1" maxlenght="50" size="25" placeholder="Dresden"><br>
            <label for="plz">PLZ:</label><br>
            <input type="text" id="plz" name="plz1" pattern="[0-9]{5}" size="25" placeholder="01099"><br>
            <label for="url">Ihre URL:</label><br>
            <input type="url" id="url" name="url1" size="25" palceholder="https://nipslip.com"><br>
            <label for="alter">Alter:</label><br>
            <input type="number" id="alter" name="alter1" min="3" max="120" style="width:15.5em" placeholder="22"><br>
            <label for="range">Ihr Interesse an ähnlichen Produkten:</label><br>
            <input type="range" id="range" name="range1" min="0" max="10" value="5" size="25"><br>
            <textarea type="text" name="site_notes" rows="5" cols="40" class="form-control"
                placeholder="Bitte geben Sie hier Ihre Anfrage an uns ein:"></textarea>
            <input class="absenden" type="submit" value="Absenden"><br>

        </form>



    </main>
</template>

<style>
form {
    background-color: #F0FFFF;
    margin: auto;
}

main {
    display: flex;
}

textarea {
    min-width: 370px;
    min-height: 20px
}

.absenden {
    text-align: center;
    padding: 5px;
    margin: 10px;
    width: 20%;
}
</style>
