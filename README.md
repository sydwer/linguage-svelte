# Lin-guage
*An app for learning about, or creating your own, languages.*

## General Info
Lin-guage has three major functionalities: *Explore*, *Compare*, and *Create*

### Explore:
  Users can click on a "card" for one of the languages in Lin-guage's database. This displays a page with information about     the selected language.  

  Information includes: an inventory of every IPA (International Phonetic Alphabet) symbol/ sound used in that language, basic   facts including number of speakers or how to say hello, and grammar deatails like what writing system it uses.

  *Every page also includes a link to that language's program on Duolingo's website*
  
### Compare:
  The Compare page utilizes an algorithum that sorts "language transtions" (learning a second language with attention given to   the first/ "native language") ordered easiest transtion to make, to hardest. 
  
  *Ex. "English -> Spanish" is a language transition where English is the native language, and Spanish is the second/ foreign   language to be learned.*
  
  Clicking on a language comparison in the list displays a side by side table of the two languages. This table shows all
  language info/traits for both languages that are used in the algorithum, so that users can get a more detailed compare
  and contrast realtionship between them.
  
### Create:
  Users can create their own language with the Create functionaility. The user selects what language they like the "sound of"
  and one they like the grammar structure of. Lin-guage then runs an algorithum that creates a completley unique language
  based on these choices.
  
  Every time this function is used, a new mini dictionary of randomly generated nouns, pronouns, verbs, adjectives, and 
  necessary grammar markers is generated based on the phonology(sound patterns and sound inventory) selected by the user.
  
  These words are then used to fill in templates for the selected grammar. There is a unique grammar specialized for each 
  language in the database.
  
  The language generated also has a mini-grammar, wherein  a list of necessary (and also novelly generated) grammar markers
  and verb tenses are listed. 
  
  12 sample sentences that show a range of verb tenses and grammatical relations are also given
  with linguistic glosses (this is the generated sentence in IPA, with grammar markers identified clearly, as well as 
  an English translation underneath).
  
## Technologies:
- Svelte
- HTML5
- CSS
- Javascript
- Ruby
- Ruby on Rails

## To-Do List
- Finish specialized grammars for remaining languages
- Add in a save feature, so that generated languages are not lost upon exiting the page
- Refactor code to avoid redundant use of variables

## Status

The project is still in progress, as the *Create* function is undergoing some major changes, and will not be deployed until the specialized grammars have been completed.
  



