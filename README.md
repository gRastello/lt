# nclt
Spaced repetition shell scripts based on the SM2 algorithm (it's old but it works (for me)); with an ncurses interface.

## Dependencies
Everything should be installed on your Linux distro of choice and if not you'll surely find them in your repositories.

* bash
* bc
* dialog

### notes on v0.1.0
v0.1.0 is the first release of nclt. There are not much changes in how the whole thing works from the previous stages of development, but there is a fundamental change: v0.1.0 uses a different date format from the previous versions. I've moved from `mm-dd-yyyy` to `yyyymmdd` since I find out that the former would have caused some problems with the year change while the latter should be 100% reliable (if I did the math right). So **if you were using a previous version** of nclt you should now open up you deckfiles manually and change all the dates from `mm-dd-yyyy` format to `yyyymmdd` format; I'm sorry that this is the case (but on the other side it takes literally less than a minute to do it with a Vim macro or a shell script, even for files thousand of lines long). Also by avoiding the dashes we're saving 3 bytes per line thus making our decks lighter.
I'm not sure about this but it should be possible not to have to edit manually your decks but just to study them directly, nclt will probably identify all flashcards as old and so will make you review every single on of them and, as you do so, replace the old dates with new ones in the current correct format; this should not hinder your card stats as well. However **I have not tested this myself** and you should not rely on this method working because **it is not a feature**, however you can test it and maybe I will work; in case it messes up your deck you should have the automatically generated backup, so everything will be fine.

## Usage
Clone this repository, create a deck file (`touch mydeck.deck` should suffice, .deck extension is not needed but recommended to easily spot your decks), run `./nclt mydeck.deck`. After that an ncurses menu should appear in your terminal and you'll be able to study and cram your deck as well as adding new flashcards and see some info.

### Structure of a deck file
In the remote case you'll ever need to edit a deck file manually this section provides some information about the structure of deck files. A deck file is some plain text file like this:

```
<question>;<answer>;<e-factor>;<repetition-date>;<repetition-number>;<current-interval>
<question>;<answer>;<e-factor>;<repetition-date>;<repetition-number>;<current-interval>
<question>;<answer>;<e-factor>;<repetition-date>;<repetition-number>;<current-interval>
.
.
.
```

as you can imagine each line represent a flashcard and some information about it. To add a flashcard just substitute `<question>` and `<answer>` accordingly and give the other fields the standard values as in the following example:

```
Definition of a fiel;A field is a commutative division ring;2.5;yyyymmdd;0;0
```

usually you'll want to substitute `yyyymmdd` with today's or tomorrow date but if you're making flashcards in advance you can also schedule them for later my writing a future date. You should not put any line that is not of the above format in a deck file nor use the `;` character in your questions or answers. **If you do not respect those simple rules nclt will probably fail potentially deleting part (if not all) of your flashcards** thus is good practice to back up your decks (not needed anymore because now nclt automatically backs up your decks before reviewing them; however you may want to keep different backups at different times).

## Known bugs and strange "features"
* lt does not allow you to quit a session nor saves any progress to the deck file until the session is over. If you quit from lt for any reason it is possible to recover the lost progress in the `/tmp/tmpdeck` file and merge them back into the deck file
* running more than one instance of lt will probably mess up your decks since lt saves progress in temporary file `/tmp/tmpfile`
* if you're manually editing your decks do not expect them to be well-ordered; lt literally shuffles them every time

## TODO
* [X] probably dropping lt and moving to developing only nclt
* [X] fix the info bug
* [X] add more informations to the info command
* [X] add info funtionality
* [X] add functionality to add flashcards to a deck without having to operate the deck file directly
* [X] merging cram into lt and make it available with an option
