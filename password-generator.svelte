<script>
    // This component requires the popular-english-words NPM package
    // https://www.npmjs.com/package/popular-english-words
    import {words} from 'popular-english-words';
    const wordList = words.getMostPopular(3000)
    let specialChars = ["?", "\\", "/", "!", "\"", "$", ".", ",", "#", "*", "+", "-"];

    // Reactive state for the password
    let password = $state('Password Here!');

    function getRanChar() {
        let char = Math.floor(Math.random() * specialChars.length);
        return specialChars[char];
    }

    function getRanNumber() {
        return Math.floor(Math.random() * 10);
    }

    function capitalizeFirstLetter(val) {
        return String(val).charAt(0).toUpperCase() + String(val).slice(1);
    }

    function getRandomWord() {
        return Math.floor(Math.random() * wordList.length);
    }

    function changetext() {
        let word1 = capitalizeFirstLetter(wordList[getRandomWord()]);
        let word2 = capitalizeFirstLetter(wordList[getRandomWord()]);
        let word3 = capitalizeFirstLetter(wordList[getRandomWord()]);
        let number1 = getRanNumber();
        let number2 = getRanNumber();
        let specialChar = getRanChar();
        let specialChar2 = getRanChar();
        let dice = Math.random() < 0.5;

        password = dice
          ? word1 + word2 + word3 + number1 + number2 + specialChar
          : specialChar2 + word1 + word2 + word3 + number1 + number2 + specialChar
    }
</script>

<h1>Password Generator</h1>
<button id="gen" onclick={changetext}>Generate!</button>
<div id="text">{password}</div>
<div class="res">
    <button id="copy" class="button-symbol" onclick={() => navigator.clipboard.writeText(password)}>
        <img class="img-small" src="https://cdn-icons-png.flaticon.com/512/54/54702.png" alt="Copy">
    </button>
</div>
