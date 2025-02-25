# FlashCards Project Plan & Pseudocode

(Project Benchmarks & Schedule)[https://trello.com/b/SOkAxuLZ/flashcards-project]

## Iteration 1:

### Cards

* A `Card` represents a single flashcard
* Each card has an id, a question, possible answers, and a correct answer

**example:**
> const card = new Card(1, 'What is Robbie\'s favorite animal', ['sea otter', 'pug', 'capybara'], 'sea otter');


#### PSEUDOCODE:

- Create a Card class instantiator with constructor method inside
- Export Card class instantiator
- Add 4 arguments to constructor method: `id`, `question`, `answers`, and `correctAnswer`
- Add 4 class properties and assign these arguments as values


### Turns

* Your Turn class should meet the following requirements:
  * Instantiated with two arguments - a string (that represents a user’s guess to the question), and a `Card` object for the current card in play.
  * `returnGuess`: method that returns the guess
  * `returnCard`: method that returns the Card
  * `evaluateGuess`: method that returns a boolean indicating if the user’s guess matches the correct answer on the card
  * `giveFeedback` - method that returns either ‘incorrect!’ or ‘correct!’ based on whether the guess is correct or not.

**example:**
>const card = new Card(1, 'What is Robbie\'s favorite animal', ['sea otter', 'pug', 'capybara'], 'sea otter');
>const turn = new Turn('pug', card);
>
>turn.returnGuess();    // => 'pug'
>
>turn.returnCard();     // => { id: 1,
>                       //      question: 'What is Robbie\'s favorite >animal',
>                       //      answers: ['sea otter', 'pug', 'capybara'],
>                       //      correctAnswer: 'sea otter'
>                       //    }
>
>turn.evaluateGuess();  // => false
>
>turn.giveFeedback();   // => incorrect!

#### PSEUDOCODE:

##### Turn.js

- Create Turn.js file with Turn class instantiator function
- Export Turn class instantiator
- Add constructor method with 2 arguments: `guess` and `card`
- Add 2 class properties and assign these arguments as values
- Add another class property - `this.status` - assigned a default value of false
- Add 4 class methods: `returnGuess`, `returnCard`, `evaluateGuess`, and `giveFeedback`
- Add simple property value returns to `returnGuess` and `returnCard`: `this.guess` and `this.card`, respectively
- Write functionality for `evaluateGuess` method: 
    - Use conditional to check if `this.guess` value is strictly equal to that of `this.card.correctAnswer`
    - Reassign value of `this.status` to true or false based on result
- Write functionality for `giveFeedback` method:
    - Use conditional to check if `this.status` is true or false
    - Return string feedback based on value

##### Turn-test.js

- Add boilerplate code to require Chai library, Expect API, and Test.js
- Add 'describe' code block
- Within block, add individucal test functions:
    - Test that `Turn` is a function
    - Assign `new Turn` to a variable and test that variable is an instanceOf `Turn`
    - Test that `turn` stores a guess
    - Test that `turn` stores a card object
    - Test that `returnGuess` returns a provided 'guess' string argument
    - Test that `returnCard` returns a provided 'card' object argument
    - Test that `evaluateGuess` returns a 'true' value in a 'correct' test case
    - Test that `evaluateGuess` returns a 'false' value in a 'incorrect' test case
    - Test that `giveFeedback` returns the appropriate string in a 'correct' test case
    - Test that `giveFeedback` returns the appropriate string in an 'incorrect' test case


## Iteration 2:

### Deck

* Your Deck class should be initialized with an array of Card objects and should have an accompanying test file. It should know how many Cards are in the Deck.

**example:**
>const card1 = new Card(1, 'What is Robbie\'s favorite animal', ['sea otter', 'pug', 'capybara'], 'sea otter');
>const card2 = new Card(14, 'What organ is Khalid missing?', ['spleen', 'appendix', 'gallbladder'], 'gallbladder');
>const card3 = new Card(12, 'What is Travis\'s middle name?', ['Lex', 'William', 'Fitzgerald'], 'Fitzgerald');
>
>const deck = new Deck([card1, card2, card3]);
>
>deck.countCards(); // => 3


#### PSEUDOCODE:

##### Deck.js

- Create Deck.js file with Deck class instantiator function
- Export Deck class instantiator
- Add constructor method with one `cards` argument
- Add `this.cards` property and assign `cards` as value
- Add `this.size` property and assign `cards.length` as value

##### Deck-test.js

- Create Deck-test.js file
- Add boilerplate code to require Chai library, Expect API, ~and Deck.js~
- Add 'describe' code block
- Within block, add individual test functions:
    - Test that `Deck` is a function
    - Assign `new Deck` to a variable and test that variable is an instanceOf `Deck`
    - Test that correct `cards` element is accessed by index
    - Test that another `cards` element is correctly accessed by index 
    - Test that `size` stores the correct length of passed cards array


### Round

* Your Round class will be the object that takes in responses and records these guesses (as well as if they are correct or incorrect). The currentCard should be the first Card in the Deck (the array of Cards) at the start of the Round

* Your Round class should meet the following requirements:
  * returnCurrentCard: method that returns the current card being played
  * takeTurn: method that updates turns count, evaluates guesses, gives feedback, and stores ids of incorrect guesses
    * When a guess is made, a new Turn instance is created.
    * The turns count is updated, regardless of whether the guess is correct or incorrect
    * The next card becomes current card
    * Guess is evaluated/recorded. Incorrect guesses will be stored (via the id) in an array of incorrectGuesses
    * Feedback is returned regarding whether the guess is incorrect or correct
  * calculatePercentCorrect: method that calculates and returns the percentage of correct guesses
  * endRound: method that prints the following to the console: ‘** Round over! ** You answered <>% of the questions correctly!’

**example:**
>const card1 = new Card(1, 'What is Robbie\'s favorite animal', ['sea otter', 'pug', 'capybara'], 'sea otter');
>const card2 = new Card(14, 'What organ is Khalid missing?', ['spleen', 'appendix', 'gallbladder'], 'gallbladder');
>const card3 = new Card(12, 'What is Travis\'s favorite stress reliever?', ['listening to music', 'watching Netflix', 'playing with bubble wrap'], 'playing with bubble wrap');
>
>const deck = new Deck([card1, card2, card3]);
>
>const round = new Round(deck);
>
>round.deck;   // => [card1, card2, card3];
>
>round.returnCurrentCard(); // => { id: 1,
>                           //      question: 'What is Robbie\'s favorite >animal',
>                           //      answers: ['sea otter', 'pug', 'capybara']>,
>                           //      correctAnswer: 'sea otter'
>                           //    }
>
>round.turns; // => 0
>
>round.incorrectGuesses;     // => []
>
>round.takeTurn('sea otter'); // => 'correct!'
>
>round.takeTurn('spleen');   // => 'incorrect!'
>
>round.turns; // => 2
>
>round.incorrectGuesses;     // => [14]
>
>round.returnCurrentCard();    // => { id: 12,
>            	              //      question: 'What is Travis\'s favorite >stress reliever?',
>            	              //      answers: ['listening to music', >'watching Netflix', 'playing with bubble wrap'],
>            	              //      correctAnswer: 'playing with bubble wrap'
>            	              //    }
>
>round.calculatePercentCorrect(); // => 50

#### PSEUDOCODE:

##### Round.js

- Create Round.js file with Round class instantiator function
- Export Round class instantiator
- Add constructor method with 1 argument: `cards`
- Add `deck` property and assign `cards` argument as value
- Add `currentCard` property and assign `this.deck[0]` as value
- Add `turns` property and assign a default value of 0
- Add `incorrectGuesses` property and assign an empty array as value
- Declare `percentCorrect` variable (no default value?)
- Add 4 methods: `returnCurrentCard`, `takeTurn`, `calculatePercentCorrect`, and `endRound`
- Add `returnCurrentCard()` functionality: should return value of `this.currentCard`
- Add `takeTurn()` functionality:
    - Assign a new `Turn` class instance to a `turn` variable using 2 arguments: the user's guess (must prompt for input) and the card at play.  
    SYNTAX: `let turn = new Turn(input, currentCard)`
    - Declare `status` variable, invoke `turn.evaluateGuess()` and assign return as value
    - Execute a conditional to test if value of `status` is false; if so, push `this.currentCard.id` into `this.incorrectGuesses` array
    - Increment `this.turns`
    - Execute conditional to test if value of `this.turns` has exceeded `this.deck.length`
        - If false:
          - Reassign the value of `this.currentCard` to the next element in `this.deck`
          - Return value of `this.turn.giveFeedback()`
        - If true:
          - Add way to deactivate round - no longer prompt for user input?
          - Return value of `this.turn.giveFeedback() \n ${this.endRound()}`

- Add `calculatePercentCorrect()` functionality: 
    - Reassign value of `this.percentCorrect` to `((this.turns - this.incorrectGuesses.length) / this.turns) * 100`
    - Return `this.percentCorrect`
- Add `endRound()` functionality:
    - Return `** Round over! ** You answered ${this.percentCorrect}% of the questions correctly!`

##### Round-test.js

- Create Round-test.js file
- Add boilerplate code to require Chai library, Expect API, and Round.js
- Add 'describe' code block
- Within block, add individual test functions:
    - Test that `Round` is a function
    - Assign `new Round` to a variable and test that variable is an instanceOf `Round`
    - Test that `deck` stores the value of passed cards array (use a short new array, not data.js)
    - Test that `currentCard` stores the value of `deck[0]`
    - Test that `turns` starts with a default value of 0
    - Test that `incorrectGuesses` starts with a default value of []
    - Test that `percentCorrect` starts with a default value of undefined
    - Test that `returnCurrentCard()` returns value of `this.currentCard`
    - Run `takeTurn()` and test that method instantiates new `Turn` class
    - Test that after a correct guess, `this.incorrectGuesses[0]` returns undefined
    - Test that after an incorrect guess, `this.incorrectGuesses[0]]` holds value of last `currentCard`
    - Test that after any guess, `turns` has incremented
    - Test that after a correct guess, 'correct!' string is returned
    - Test that after an incorrect guess, 'incorrect!' string is returned
    - Test that `calculatePercentCorrect()` returns the correct percentage
    - Test that after final card's turn has been taken, round ends (returns endGame() string)


## Iteration 3:

### Playing the Game

* Now that we have all of our classes and methods set up, we can connect this to the pre-existing code to make the game playable through the CLI (Command-Line-Interface).

### Game

* As you may have noticed, your Game class has two methods fleshed out already: printMessage and printQuestion. We are going to abandon testing for these methods - as the techniques for this type of testing are beyond the scope of this project.

- Your Game class should meet these other requirements:
    - Should keep track of the currentRound
    - start: method that starts everything
      - Creates Cards
      - Puts Cards in a Deck
      - Creates a new Round using the Deck
      - invokes printMessage to display the message in the CLI
      - invokes printQuestion to kick off our helper functions that allow interaction via the CLI

**Note: The helper functions are all fleshed out and fit to work with classes/methods that meet the requirements in the past iterations.**

#### HINT: 
Look at the file being run when we want to start the game. Think about where you need to invoke your Game.start method.

**example:**
> game.currentRound; // => Round {...} (The new Round object that has been >instatiated)

#### PSEUDOCODE:

##### Game.js

- Connect Game.js to any required class instantiator files (i.e. Round.js)
- Declare `currentDeck` property with no default value
- Declare `currentRound` property with no default value
- Add `start()` method 
  - Assign new instance of `Deck` (with `prototypeQuestions` as argument) as `currentDeck` value
  - Assign new instance of `Round` (with `currentDeck` as argument) as `currentRound` value
  - Invoke `printMessage` method with `currentDeck` and `currentRound` as arguments
  - Invoke `printQuestion` method with `currentRound` as argument
  - Should be able to "create Cards" and "put Cards in Deck", but why?  Aren't we just creating a new `Deck` with `prototypeQuestions` array as value?
- Figure out where to invoke `Game.start` (probably in `index.js` file)

##### Game-test.js

- Add boilerplate and require any needed class instantiator files
- Test that `Game` is a function
- Test that `game` is an instance of `Game`
- Test that `currentDeck` property has an empty array as value
- Test that `currentRound` property has an empty object as value
- Test that `start()` will create Cards
- Test that `start()` will assign new `Deck` instance to value of `currentDeck` property
- Test that `start()` will assign new `Round` instance to value of `currentRound` property
- All other functionality should be testable by actually running game in console

##### index.js

- Invoke `Game.start` method to initialize new game
- See what happens and refactor code as necessary!