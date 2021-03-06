# Tongues Script
A simple script to simulate languages on Roll20 and show the translation only to those characters that know the language.

# Index
1. [Installation](#installation)
2. [Usage](#usage)
3. [Available commands](#available-commands)

# Installation
- Add a new script on Settings -> API Scripts of the game you want to install the script in
- Copy the contents of tongues.js on this repository to the new script
- Save the script
- Enjoy!

# Usage
Tongues need you to create and define a vocabulary for every language you want to use.

In order to create a new language you may use: `!tongues --create [name]`, this command will create a new handout on your campaign named after the language (prefixed with "Tongues: ") and with its notes section [partially filled](https://i.gyazo.com/f42ef037efb3744221834743081696b1.png).

Once the template is created you must fill each row's brackets with some vocabulary, delimited by commas. When speaking a language, the script will take a vocabulary word from the closest length with words available, if you type a 16-length word and there are no 16-length words for that language then the script will take a 15-length one and so on until it finds a length with words available. The create command creates a template with up to 14-length words but you can define greater lengths just by inserting a new row.
Additionally you can specify specific translation for a given word or sentence with the syntax "Word:Translation" inside brackets.
A full functional language with new rows created will look close to [this example](https://i.gyazo.com/1eb5a7f0ad688a6fa0281172a828d9f4.png).

Once you have your language defined as you like, you just have to write the full name of its speakers on the GM Notes of the handout, delimited by commas followed with a ":" and a percentage which represent its knowledge of the language, as shown [here](https://i.gyazo.com/04bd5b16ca29a4c49b3a5b9f1b2d26c0.png). The script will look for a character with a name exact to the one written on the GM Notes, you must write the full name of the desired character. If more than one character are named after the same, the script may malfunction.

A language dictionary and vocabulary words are given a difficulty between 1 and 100, characters which meet this number with its knowledge percentage of the language will be able to speak/understand those words.
Once you have you speakers written down on the GM Notes, selecting a token representing those characters and using the command `!tongues [language] [text]`will send to the chat a translated text and whisper all its speakers the original text. **Note:** The GM will always get the original text whispered, which may cause some replicaiton issues since you could be tagged as a character's controller and the script whispers both the GM and the language speaker characters.

When sending a message thourgh Tongues, text between $ symbols will not be parsed by the script and will be displayed with grey color to those who understand the language (in order to separate it from the translation).
When a speaker sends a message, any words not meet by the knowledge level of the speaker will be displayed with blue color to those who understand the language.
Whenever reading a message, any words not meet by the knowledge level of the listener will be displayed with red color and not translated to those who understand the language.

To remove a language you simply have to delete its handout as the script does not use data storage and depends on the campaign's handouts.

# Available commands
*Note: configuration commands are only available to GM*

## !tongues (language) (message)
- **Configuration command:** No
- **Target required:** Token representing a Character Sheet
- **Example:** !tongues Draconic I will kill you!

Makes the token speak the message in the provided language if all conditions are met.
The GM can speak any language regardless of the token being a speaker of the language in which case a knowledge of 100% will be used for the translation.
The GM always gets the whole original message plus any translation from any Character it may be controlling.
## !tongues --create (language)
- **Configuration command:** Yes
- **Target required:** None
- **Example:** !tongues --create Draconic

Creates a new handout template named after the provided language.
## !tongues --ability
- **Configuration command:** Yes
- **Target required:** Token representing a Character Sheet
- **Example:** !tongues --ability

Creates or updates a token ability named "Tongues" for the selected Character which will list all the languages known by the Character and send a message with the one selected.
## !tongues --set (language:knowledge%)
- **Configuration command:** Yes
- **Target required:** Token representing a Character Sheet
- **Example:** !tongues --set Draconic | !tongues --set Draconic:50%

Adds or updates knowledge of the provided language to the selected Character. Providing a knowledge % is optional. If the character has an ability named "Tongues" this command will run a ***!tongues --ability*** command for the selected Character once language knowledge is added.
## !tongues --unset (language)
- **Configuration command:** Yes
- **Target required:** Token representing a Character Sheet
- **Example:** !tongues --unset Draconic

Removes knowledge of the provided language from the selected Character. If the character has an ability named "Tongues" this command will run a ***!tongues --ability*** command for the selected Character once language knowledge is removed.
## !tongues --speaker (name)
- **Configuration command:** Yes
- **Target required:** None
- **Example:** !tongues --speaker Elminster Aumar

Saved the provided name to the script's state storage for later use. Whenever a ***!tongues (language) (message)*** is issued by a GM without a token selected, the script will display the stored name. Defaults to ***John Smith*** if unchanged.

