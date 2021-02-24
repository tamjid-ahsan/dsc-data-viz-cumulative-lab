
Data Visualization - Cumulative Lab
Introduction
You've completed the data visualization section — excellent work. Now we're going to do some rudimentary analysis of Shakespeare's classic play: Macbeth! You will get practice working with lists and dictionaries, conditionals, visualizing data, and thinking analytically about data.

Objectives
You will be able to:

Apply string methods to make changes to a string
Use a for loop to iterate over a collection
Assign values in a dictionary
Use data visualizations to present your findings
Your Task: Analyze the Text of Shakespeare's Macbeth
cover page of macbeth

Photo by Matt Riches on Unsplash

Business Understanding
Natural language processing (also known as NLP) is a major subfield within data science. At its most advanced, NLP has helped us build interactive AI assistants like Siri and Alexa.

Even in a simpler business context where you just need to summarize the contents of a dataset, text data often requires much more substantial preprocessing work compared to data that is already in a numeric format.

One typical technique for understanding a text dataset is to find the most common or least common words. To do this, we need to build a Frequency Distribution table, just like when we were finding the mode of a dataset. We'll display the thousands of word frequencies as a histogram.

Then we can find the mode (the word that appears most often), as well as the "runner-up" words, in order to describe a large text dataset with a minimal set of words and numbers. We'll display this information as a bar graph with the words as labels on the x-axis and the counts as the y-axis.

Data Understanding
For this lab we'll be using the full text of Shakespeare's Macbeth. We will retrieve it for you from the Project Gutenberg website in the format of a single (giant) string, containing over one hundred thousand characters. We'll refer to this string variously as the "document", "corpus", or "text dataset", all terms used frequently within NLP.

We don't recommend that you try to print the entire string due to its length, but if you're curious about any particular segment, you can use string slicing just like any other string. E.g. macbeth[1000:2000] will select just the slice from the 1000th to the 2000th character.

When counting the words, make sure you remove any punctuation and convert all words to lowercase. We want all of the following strings to be counted as instances of "is":

"is"
"Is"
"is,"
"is!"
etc.
Requirements
1. Word Count Summary
Extract each word from the document and print a count of all words.

2. Unique Word Count
First, clean up the collection of words so all punctuation is removed and every word is lowercase. Then print a count of the unique words in that collection.

3. Frequency Table
Using the cleaned collection of words, build a frequency table that has the words as keys and the counts of those words as values. From that frequency table, print the modal (most common) word as well as the least common word, along with their frequencies.

4. Visualizations
Histogram: Using Matplotlib or Seaborn, create a histogram of all of the word frequencies in Macbeth.

Bar graph: Using Matplotlib or Seaborn, create a bar graph of the 25 most common words in Macbeth, from the 1st to 25th most common.

Getting the Data
Here we start by importing a Python package called requests. You'll see this package described in more detail in future lessons, but for now all you need to know is that it allows us to fetch data over the internet!

We'll use it to pull the transcript of Macbeth from the Project Gutenberg website, specifically this page. We'll also preview a few details about what is now stored in the variable macbeth. As you can see, it's a string with 103,605 characters - the first 500 of which are printed below.

In [1]:
# Run this cell without changes
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_context("talk")
sns.set_style("whitegrid")
%matplotlib inline
In [1]:
import requests
from jupyterthemes import jtplot
jtplot.reset()
In [23]:
# Run this cell without changes
response = requests.get('https://www.gutenberg.org/cache/epub/2264/pg2264.txt')
full_text = response.text

# The beginning describes the source/copyright, it isn't the actual text
# of the play until the 16648th character
macbeth = full_text[16648:]

# Print string summary
print("Data type:", type(macbeth))
print()
print("Number of characters:", len(macbeth))
print()
print("First 500 characters:")
print(macbeth[:500])
Data type: <class 'str'>

Number of characters: 103605

First 500 characters:
The Tragedie of Macbeth

Actus Primus. Scoena Prima.

Thunder and Lightning. Enter three Witches.

  1. When shall we three meet againe?
In Thunder, Lightning, or in Raine?
  2. When the Hurley-burley's done,
When the Battaile's lost, and wonne

   3. That will be ere the set of Sunne

   1. Where the place?
  2. Vpon the Heath

   3. There to meet with Macbeth

   1. I come, Gray-Malkin

   All. Padock calls anon: faire is foule, and foule is faire,
Houer through the fogge 
Word Count Summary
Create a variable word_count that is an integer representing the total count of words in macbeth. In order to do this, first create a variable words_raw that is a list containing all words in the string.

Hint: look at the .split() string method (documentation here)

In [24]:
# Replace None with appropriate code
words_raw = macbeth.split()
word_count = len(macbeth)

print("Macbeth contains {} words".format(word_count))
print("Here are some examples:", words_raw[11:21])
Macbeth contains 103605 words
Here are some examples: ['Enter', 'three', 'Witches.', '1.', 'When', 'shall', 'we', 'three', 'meet', 'againe?']
Unique Word Count
Create a variable unique_word_count that is an integer representing the count of unique words in Macbeth.

In order to create an accurate count, first create a variable words_cleaned that contains each word stripped of punctuation and made lowercase. Then assign unique_word_count to the count of words in words_cleaned.

Hint: look at the .strip() string method (documentation here). Note that you need to strip each individual word, not just the whole macbeth string.

Reminder: strings are an immutable data type. That means that in order to modify their values, you have to reassign them with =. So, for example, if you wanted to make the variable name be title case, you need to do name = name.title(), not just name.title().

In [25]:
# Replace None with appropriate code

# You can use this punctuation string for defining what characters to remove
import string
punctuation = string.punctuation

words_cleaned = []

for word in words_raw:
    # Remove punctuation
    y = word.strip(punctuation)
    # Make lowercase
    x = y.lower()
    # Append to words_cleaned
    words_cleaned.append(x)

# Use this print statement to double-check that everything
# is lowercase and has punctuation removed
print("Cleaned word examples:", words_cleaned[0:21])
Cleaned word examples: ['the', 'tragedie', 'of', 'macbeth', 'actus', 'primus', 'scoena', 'prima', 'thunder', 'and', 'lightning', 'enter', 'three', 'witches', '1', 'when', 'shall', 'we', 'three', 'meet', 'againe']
In [26]:
# Replace None with appropriate code
# geting unique word list
uniqe_words = []
for word in words_cleaned:
    if word not in uniqe_words:
        uniqe_words.append(word)
# number of unique records
unique_word_count = len(uniqe_words)

# output
print("Macbeth contains {} unique words".format(unique_word_count))
Macbeth contains 3577 unique words
Frequency Table
Now that we have a general sense of how many words there are, let's investigate how frequently each of those words appears in the dataset. Build a frequency table called word_counts where the keys are the words (strings) and the values are the number of times that string appears. Then set most_frequent_word to the word that occurs most frequently and least_frequent_word to the word that occurs least frequently.

To accomplish this, use the same algorithm used in the Implementing Statistics with Functions lab earlier, specifically the function to find the mode. This time we will provide you with some clues, but fewer than before. Remember that you can look at that lab (and it's solution) or the solution to this lab if you are getting really stuck.

The general algorithm for building a frequency table is:

Initialize an empty dictionary (word_counts)
Loop over every element in the collection (words_cleaned) and add to the dictionary
If the element is not already in the dictionary keys, add a new key-value pair with the value 1
If the element is already in the dictionary keys, add 1 to the associated value
In [27]:
# Your code here
word_counts = {}

# method 1

# for word in words_cleaned:
#     word_counts[word] = word_counts.get(word,0)+1

# method 2
for word in words_cleaned:
    if word not in word_counts.keys():
        word_counts[word] = 1
    else:
        word_counts[word] += 1

print(type(word_counts)) # <class 'dict'>
print(len(word_counts))  # 3577
<class 'dict'>
3577
Now it's time to find most_frequent_word and least_frequent_word. Again, this follows the logic of the mode function from the previous lab.

The general algorithm for finding the most frequent word is:

Find the maximum value in the dictionary (word_counts)
Loop over all items in the dictionary until you find the key associated with that maximum value
Then the algorithm for finding the least frequent is just the inverse:

Find the minimum value in the dictionary
Loop over all items in the dictionary until you find the key associated with that minimum value
Think about how you might accomplish this with a single loop, but don't worry if it takes you two loops (just look at the solution when you are done and compare).

In [28]:
# Your code here

# # Method 1
# for key, value in word_counts.items():
#     if value == max(word_counts.values()):
#         most_frequent_word = key
#     elif value == min(word_counts.values()):
#         least_frequent_word = key
            
# Method 2
most_frequent_word = sorted(word_counts.items(), key=lambda x: x[1], reverse=True)[0][0]
least_frequent_word = sorted(word_counts.items(), key=lambda x: x[1], reverse=True)[-1][0]


## test block
# print(most_frequent_word)
# print(least_frequent_word)

print("The most frequent word in Macbeth is '{}', which appears {} times".format(
    most_frequent_word, word_counts[most_frequent_word]
))
print("The least frequent word in Macbeth is '{}', which appears {} times".format(
    least_frequent_word, word_counts[least_frequent_word]
))
The most frequent word in Macbeth is 'the', which appears 647 times
The least frequent word in Macbeth is 'finis', which appears 1 times
In [29]:
list(word_counts.keys())
Out[29]:
['the',
 'tragedie',
 'of',
 'macbeth',
 'actus',
 'primus',
 'scoena',
 'prima',
 'thunder',
 'and',
 'lightning',
 'enter',
 'three',
 'witches',
 '1',
 'when',
 'shall',
 'we',
 'meet',
 'againe',
 'in',
 'or',
 'raine',
 '2',
 "hurley-burley's",
 'done',
 "battaile's",
 'lost',
 'wonne',
 '3',
 'that',
 'will',
 'be',
 'ere',
 'set',
 'sunne',
 'where',
 'place',
 'vpon',
 'heath',
 'there',
 'to',
 'with',
 'i',
 'come',
 'gray-malkin',
 'all',
 'padock',
 'calls',
 'anon',
 'faire',
 'is',
 'foule',
 'houer',
 'through',
 'fogge',
 'filthie',
 'ayre',
 'exeunt',
 'scena',
 'secunda',
 'alarum',
 'within',
 'king',
 'malcome',
 'donalbaine',
 'lenox',
 'attendants',
 'meeting',
 'a',
 'bleeding',
 'captaine',
 'what',
 'bloody',
 'man',
 'he',
 'can',
 'report',
 'as',
 'seemeth',
 'by',
 'his',
 'plight',
 'reuolt',
 'newest',
 'state',
 'mal',
 'this',
 'serieant',
 'who',
 'like',
 'good',
 'hardie',
 'souldier',
 'fought',
 'gainst',
 'my',
 'captiuitie',
 'haile',
 'braue',
 'friend',
 'say',
 'knowledge',
 'broyle',
 'thou',
 'didst',
 'leaue',
 'it',
 'cap',
 'doubtfull',
 'stood',
 'two',
 'spent',
 'swimmers',
 'doe',
 'cling',
 'together',
 'choake',
 'their',
 'art',
 'mercilesse',
 'macdonwald',
 'worthie',
 'rebell',
 'for',
 'multiplying',
 'villanies',
 'nature',
 'swarme',
 'him',
 'from',
 'westerne',
 'isles',
 'kernes',
 'gallowgrosses',
 "supply'd",
 'fortune',
 'on',
 'damned',
 'quarry',
 'smiling',
 "shew'd",
 'rebells',
 'whore',
 'but',
 "all's",
 'too',
 'weake',
 'well',
 'hee',
 'deserues',
 'name',
 'disdayning',
 'brandisht',
 'steele',
 'which',
 "smoak'd",
 'execution',
 'valours',
 'minion',
 "caru'd",
 'out',
 'passage',
 'till',
 "fac'd",
 'slaue',
 "neu'r",
 'shooke',
 'hands',
 'nor',
 'bad',
 'farwell',
 "vnseam'd",
 'naue',
 'toth',
 'chops',
 "fix'd",
 'head',
 'our',
 'battlements',
 'o',
 'valiant',
 'cousin',
 'worthy',
 'gentleman',
 'whence',
 'gins',
 'reflection',
 'shipwracking',
 'stormes',
 'direfull',
 'thunders',
 'so',
 'spring',
 'comfort',
 "seem'd",
 'discomfort',
 'swells',
 'marke',
 'scotland',
 'no',
 'sooner',
 'iustice',
 'had',
 'valour',
 "arm'd",
 "compell'd",
 'these',
 'skipping',
 'trust',
 'heeles',
 'norweyan',
 'lord',
 'surueying',
 'vantage',
 'furbusht',
 'armes',
 'new',
 'supplyes',
 'men',
 'began',
 'fresh',
 'assault',
 "dismay'd",
 'not',
 'captaines',
 'banquoh',
 'yes',
 'sparrowes',
 'eagles',
 'hare',
 'lyon',
 'if',
 'sooth',
 'must',
 'they',
 'were',
 'cannons',
 "ouer-charg'd",
 'double',
 'cracks',
 'doubly',
 'redoubled',
 'stroakes',
 'foe',
 'except',
 'meant',
 'bathe',
 'reeking',
 'wounds',
 'memorize',
 'another',
 'golgotha',
 'cannot',
 'tell',
 'am',
 'faint',
 'gashes',
 'cry',
 'helpe',
 'thy',
 'words',
 'become',
 'thee',
 'smack',
 'honor',
 'both',
 'goe',
 'get',
 'surgeons',
 'rosse',
 'angus',
 'comes',
 'here',
 'thane',
 'haste',
 'lookes',
 'eyes',
 'should',
 'looke',
 'seemes',
 'speake',
 'things',
 'strange',
 'god',
 'saue',
 "cam'st",
 'fiffe',
 'great',
 'banners',
 'flowt',
 'skie',
 'fanne',
 'people',
 'cold',
 'norway',
 'himselfe',
 'terrible',
 'numbers',
 'assisted',
 'most',
 'disloyall',
 'traytor',
 'cawdor',
 'dismall',
 'conflict',
 "bellona's",
 'bridegroome',
 'lapt',
 'proofe',
 'confronted',
 'selfe-comparisons',
 'point',
 'against',
 'rebellious',
 'arme',
 'curbing',
 'lauish',
 'spirit',
 'conclude',
 'victorie',
 'fell',
 'vs',
 'happinesse',
 'now',
 'sweno',
 'norwayes',
 'craues',
 'composition',
 'would',
 'deigne',
 'buriall',
 'disbursed',
 'at',
 'saint',
 'colmes',
 'ynch',
 'ten',
 'thousand',
 'dollars',
 'generall',
 'vse',
 'more',
 'deceiue',
 'bosome',
 'interest',
 'pronounce',
 'present',
 'death',
 'former',
 'title',
 'greet',
 'ile',
 'see',
 'hath',
 'noble',
 'tertia',
 'hast',
 'beene',
 'sister',
 'killing',
 'swine',
 'saylors',
 'wife',
 'chestnuts',
 'her',
 'lappe',
 'mouncht',
 '',
 'giue',
 'me',
 'quoth',
 'aroynt',
 'witch',
 'rumpe-fed',
 'ronyon',
 'cryes',
 "husband's",
 'aleppo',
 'gone',
 'master',
 "o'th",
 'tiger',
 'syue',
 'thither',
 'sayle',
 'rat',
 'without',
 'tayle',
 'winde',
 "th'art",
 'kinde',
 'selfe',
 'haue',
 'other',
 'very',
 'ports',
 'blow',
 'quarters',
 'know',
 "i'th",
 'ship-mans',
 'card',
 'dreyne',
 'drie',
 'hay',
 'sleepe',
 'neyther',
 'night',
 'day',
 'hang',
 'pent-house',
 'lid',
 'liue',
 'forbid',
 'wearie',
 "seu'nights",
 'nine',
 'times',
 'dwindle',
 'peake',
 'pine',
 'though',
 'barke',
 'yet',
 'tempest-tost',
 'shew',
 'pilots',
 'thumbe',
 'wrackt',
 'homeward',
 'did',
 'drum',
 'drumme',
 'doth',
 'weyward',
 'sisters',
 'hand',
 'posters',
 'sea',
 'land',
 'thus',
 'about',
 'thrice',
 'thine',
 'mine',
 'make',
 'vp',
 'peace',
 "charme's",
 'wound',
 'banquo',
 'macb',
 'seene',
 'how',
 'farre',
 "is't",
 "call'd",
 'soris',
 'are',
 "wither'd",
 'wilde',
 'attyre',
 'th',
 'inhabitants',
 'earth',
 "on't",
 'you',
 'aught',
 'may',
 'question',
 'seeme',
 'vnderstand',
 'each',
 'once',
 'choppie',
 'finger',
 'laying',
 'skinnie',
 'lips',
 'women',
 'your',
 'beards',
 'interprete',
 'mac',
 'glamis',
 'shalt',
 'hereafter',
 'banq',
 'sir',
 'why',
 'start',
 'feare',
 'sound',
 'truth',
 'ye',
 'fantasticall',
 'indeed',
 'outwardly',
 'partner',
 'grace',
 'prediction',
 'hauing',
 'royall',
 'hope',
 'wrapt',
 'withall',
 'into',
 'seedes',
 'time',
 'graine',
 'grow',
 'then',
 'begge',
 'fauors',
 'hate',
 'hayle',
 'lesser',
 'than',
 'greater',
 'happy',
 'much',
 'happyer',
 'kings',
 'none',
 'stay',
 'imperfect',
 'speakers',
 'sinells',
 'liues',
 'prosperous',
 'stands',
 'prospect',
 'beleefe',
 'owe',
 'intelligence',
 'blasted',
 'stop',
 'way',
 'such',
 'prophetique',
 'greeting',
 'charge',
 'vanish',
 'bubbles',
 'water',
 "ha's",
 'them',
 'whither',
 "vanish'd",
 'corporall',
 'melted',
 'breath',
 "stay'd",
 'eaten',
 'insane',
 'root',
 'takes',
 'reason',
 'prisoner',
 'children',
 'went',
 'selfe-same',
 'tune',
 "who's",
 'happily',
 "receiu'd",
 'newes',
 'successe',
 'reades',
 'personall',
 'venture',
 'rebels',
 'sight',
 'wonders',
 'prayses',
 'contend',
 "silenc'd",
 'viewing',
 "o're",
 'rest',
 'findes',
 'stout',
 'rankes',
 'nothing',
 'afeard',
 'images',
 'thick',
 'tale',
 'post',
 'euery',
 'one',
 'beare',
 'kingdomes',
 'defence',
 "powr'd",
 'downe',
 'before',
 'ang',
 'wee',
 'sent',
 'thanks',
 'onely',
 'harrold',
 'pay',
 'an',
 'earnest',
 'call',
 'addition',
 'deuill',
 'true',
 'dresse',
 'borrowed',
 'robes',
 'was',
 'vnder',
 'heauie',
 'iudgement',
 'beares',
 'life',
 'loose',
 'whether',
 "combin'd",
 'those',
 'lyne',
 'hidden',
 "labour'd",
 'countreyes',
 'wracke',
 'treasons',
 'capitall',
 "confess'd",
 "prou'd",
 'ouerthrowne',
 'glamys',
 'greatest',
 'behinde',
 'thankes',
 'paines',
 'gaue',
 "promis'd",
 'lesse',
 'trusted',
 'home',
 'might',
 'enkindle',
 'vnto',
 'crowne',
 'besides',
 'tis',
 'oftentimes',
 'winne',
 'harme',
 'instruments',
 'darknesse',
 'truths',
 'honest',
 'trifles',
 "betray's",
 'deepest',
 'consequence',
 'cousins',
 'word',
 'pray',
 'told',
 'prologues',
 'swelling',
 'act',
 'imperiall',
 'theame',
 'thanke',
 'gentlemen',
 'supernaturall',
 'solliciting',
 'ill',
 'giuen',
 'commencing',
 'yeeld',
 'suggestion',
 'whose',
 'horrid',
 'image',
 'vnfixe',
 'heire',
 'seated',
 'heart',
 'knock',
 'ribbes',
 'feares',
 'horrible',
 'imaginings',
 'thought',
 'murther',
 'shakes',
 'single',
 'function',
 "smother'd",
 'surmise',
 "partner's",
 'rapt',
 'chance',
 'stirre',
 'honors',
 'garments',
 'cleaue',
 'mould',
 'aid',
 'houre',
 'runs',
 'roughest',
 'leysure',
 'fauour',
 'dull',
 'braine',
 'wrought',
 'forgotten',
 'registred',
 'turne',
 'leafe',
 'reade',
 'let',
 'toward',
 'thinke',
 "chanc'd",
 'interim',
 "weigh'd",
 'free',
 'hearts',
 'gladly',
 'enough',
 'friends',
 'quarta',
 'flourish',
 'malcolme',
 'commission',
 "return'd",
 'liege',
 'back',
 'spoke',
 'saw',
 'die',
 'frankly',
 "implor'd",
 'highnesse',
 'pardon',
 'forth',
 'deepe',
 'repentance',
 'became',
 'leauing',
 "dy'de",
 'studied',
 'throw',
 'away',
 'dearest',
 'thing',
 "ow'd",
 'twere',
 'carelesse',
 'trifle',
 "there's",
 'finde',
 'mindes',
 'construction',
 'face',
 'whom',
 'built',
 'absolute',
 'worthyest',
 'sinne',
 'ingratitude',
 'euen',
 'swiftest',
 'wing',
 'recompence',
 'slow',
 'ouertake',
 'hadst',
 "deseru'd",
 'proportion',
 'payment',
 'left',
 'due',
 'seruice',
 'loyaltie',
 'doing',
 'payes',
 'part',
 'receiue',
 'duties',
 'throne',
 'seruants',
 'safe',
 'loue',
 'welcome',
 'hither',
 'begun',
 'plant',
 'labour',
 'full',
 'growing',
 'knowne',
 'enfold',
 'hold',
 'haruest',
 'owne',
 'plenteous',
 'ioyes',
 'wanton',
 'fulnesse',
 'seeke',
 'hide',
 'themselues',
 'drops',
 'sorrow',
 'sonnes',
 'kinsmen',
 'thanes',
 'places',
 'nearest',
 'establish',
 'estate',
 'eldest',
 'prince',
 'cumberland',
 'vnaccompanied',
 'inuest',
 'signes',
 'noblenesse',
 'starres',
 'shine',
 'deseruers',
 'hence',
 'envernes',
 'binde',
 'further',
 'labor',
 "vs'd",
 'herbenger',
 'ioyfull',
 'hearing',
 'approach',
 'humbly',
 'take',
 'step',
 'fall',
 'else',
 "o're-leape",
 'lyes',
 'fires',
 'light',
 'black',
 'desires',
 'eye',
 'winke',
 'bee',
 'commendations',
 'fed',
 'banquet',
 "let's",
 'after',
 'care',
 'bid',
 'peerelesse',
 'kinsman',
 'quinta',
 'macbeths',
 'alone',
 'letter',
 'lady',
 'met',
 "learn'd",
 "perfect'st",
 'mortall',
 'burnt',
 'desire',
 'made',
 'whiles',
 'wonder',
 'came',
 'missiues',
 "all-hail'd",
 'saluted',
 "referr'd",
 'comming',
 'deliuer',
 'greatnesse',
 "might'st",
 'dues',
 'reioycing',
 'being',
 'ignorant',
 'lay',
 'farewell',
 'milke',
 'humane',
 'kindnesse',
 'catch',
 'neerest',
 "would'st",
 'ambition',
 'illnesse',
 'attend',
 'highly',
 'holily',
 'play',
 'false',
 'wrongly',
 "thould'st",
 'rather',
 "do'st",
 'wishest',
 'vndone',
 'high',
 'powre',
 'spirits',
 'eare',
 'chastise',
 'tongue',
 'impeides',
 'golden',
 'round',
 'fate',
 'metaphysicall',
 'ayde',
 "crown'd",
 'messenger',
 'tidings',
 'mess',
 "thou'rt",
 'mad',
 "wer't",
 "inform'd",
 'preparation',
 'please',
 'fellowes',
 'speed',
 'almost',
 'dead',
 'scarcely',
 'message',
 'tending',
 'brings',
 'exit',
 'rauen',
 'hoarse',
 'croakes',
 'fatall',
 'entrance',
 'duncan',
 'tend',
 'thoughts',
 'vnsex',
 'fill',
 'toe',
 'top-full',
 'direst',
 'crueltie',
 'blood',
 'accesse',
 'remorse',
 'compunctious',
 'visitings',
 'shake',
 'purpose',
 'keepe',
 'betweene',
 'effect',
 'hit',
 'womans',
 'brests',
 'gall',
 "murth'ring",
 'ministers',
 'where-euer',
 'sightlesse',
 'substances',
 'wait',
 'natures',
 'mischiefe',
 'pall',
 'dunnest',
 'smoake',
 'hell',
 'keene',
 'knife',
 'makes',
 'heauen',
 'peepe',
 'blanket',
 'darke',
 'all-haile',
 'letters',
 'transported',
 'beyond',
 'feele',
 'future',
 'instant',
 'goes',
 'morrow',
 ...]
Visualizations
Histogram
At last, it's time for some visualizations! First, let's make a histogram to visualize the frequency distribution of all 3,577 words (i.e. the distribution of word_counts.values()).

Details:

We recommend using Matplotlib for this, since it allows you to customize the figure size. A figsize of (15,5) will work well for this, since it has a "long tail". 100 bins is also a good number.
Make sure you include appropriate labels on the axes and the title
You can use any colors or styles that look good to you
In [30]:
# # Your code here
# import numpy as np
# import matplotlib.pyplot as plt
# %matplotlib inline

# Create the plot
fig, ax = plt.subplots(figsize=(15, 5))
# Plot the histogram with hist() function
ax.hist(word_counts.values(), bins = 100, histtype = 'bar')
# Label axes and set title
ax.set_title("Macbeth Word Frequency")
ax.set_xlabel("Words")
ax.set_ylabel("Word Count")
# output
plt.show()

Wow, that is a very skewed dataset! It looks like the overwhelming majority of words appear about 20 times or fewer, but we also have words (like 'the', the most common word discovered above) that appear hundreds of times. Those very frequent words are so rare that we can't even see their associated counts, the bars are so small.

Bar Graph
Let's move on to making a bar graph of the most frequent words, to gain more insight into that end of the distribution's "tail". To do this, we need to sort the contents of word_counts by value, and then select only the top 25 key-value pairs.

For this task we are giving you even fewer hints than before. Check out the Sorting HOW TO Python documentation, especially the student_tuples example. Part of being a data scientist is figuring out how to do tasks that you may not have done before. Remember, in these situations, Google is your friend!

In [31]:
# Replace None with appropriate code

# This converts word_counts into a list of tuples,
# similar to student_tuples
counts_list = list(word_counts.items())

# Sort the list of tuples by the frequency (second element in each tuple)
# Make sure it goes from most to least frequent
counts_list_sorted = sorted(word_counts.items(), key=lambda x: x[1], reverse=True)

# Slice the sorted list to just the first 25 tuples
top_25 = counts_list_sorted[:25]

# Make a list of dummy numbers to populate the axis with the words
ticks = list(range(1, 26, 1))

# Get just the words from top_25 and assign to labels
labels = [word for word, count in top_25]

# Get just the frequencies from top_25 and assign to frequencies
frequencies = [count for word, count in top_25]

print("Tick values:", ticks)
print()
print("Labels:", labels)
print()
print("Frequencies:", frequencies)
Tick values: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]

Labels: ['the', 'and', 'to', 'of', 'i', 'a', 'that', 'my', 'you', 'in', 'is', 'not', 'it', 'with', 'his', 'be', 'macb', 'your', 'our', 'haue', 'but', 'me', 'he', 'for', 'what']

Frequencies: [647, 545, 383, 338, 331, 239, 227, 203, 203, 199, 180, 165, 161, 153, 146, 137, 137, 126, 123, 122, 120, 113, 110, 109, 106]
Now that we have our data, let's make a bar graph. Just to keep it interesting, let's make this a horizontal bar graph. Horizontal bar graphs are useful when you have a lot of text labels — it avoids having to turn the labels diagonally or even sideways in order for them to fit next to each other.

Matplotlib: In a horizontal bar graph with Matplotlib, y is where you pass in the dummy tick values, and width is where you pass in the frequencies (vs. x and height in a standard bar chart). Full documentation for .barh(), the horizontal bar chart method, here.

Seaborn: With Seaborn, you still use the .barplot() function, just with the orient argument set to "h". You'll want to pass in the dummy tick values as y and frequencies as x. Full documentation here.

Details:

You can use either Matplotlib or Seaborn
Make sure you include appropriate labels on the axes and the title
You can use any colors or styles that look good to you
In [44]:
# Your code here
frequencies_reversed = frequencies[::-1]
labels_reversed = labels[::-1]
# Create the plot
fig, ax = plt.subplots(figsize=(15, 15))
# Plot the histogram with hist() function
ax.barh(ticks, frequencies_reversed, tick_label = labels_reversed)
# Label axes and set title
ax.set_yticklabels(labels_reversed)
ax.set_title("Macbeth Word Frequency")
ax.set_xlabel("Word Count")
ax.set_ylabel("Words ")
# output
plt.show()

In [33]:
import seaborn as sns

# Create the plot
fig, ax = plt.subplots(figsize=(15, 15))
g = sns.barplot(x = frequencies, y = ticks, orient = 'h')
# formatting
g.set_yticklabels(labels= labels)
ax.set_title("Macbeth Word Frequency")
ax.set_xlabel("Word Count")
ax.set_ylabel("Words ")

# output
plt.show()

Level Up (Optional)
This cumulative lab should take you about an hour and a half to complete. If you're done much more quickly than that and are not behind in the course, feel free to deepen your knowledge by completing any or all of the following tasks until you run out of time (creating a relevant visualization for each):

When counting words, skip stopwords
Stopwords are commonly-occurring words that NLP analysts often disregard. Most of the top 25 words in our current version are stopwords ("the", "and", etc.). Try redoing both the histogram and the horizontal bar chart with stopwords removed
Mechanically, that means skipping adding a word to word_counts if it is a stop word. Try using this list of stopwords:
["i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", "her", "hers", "herself", "it", "its", "itself", "they", "them", "their", "theirs", "themselves", "what", "which", "who", "whom", "this", "that", "these", "those", "am", "is", "are", "was", "were", "be", "been", "being", "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", "the", "and", "but", "if", "or", "because", "as", "until", "while", "of", "at", "by", "for", "with", "about", "against", "between", "into", "through", "during", "before", "after", "above", "below", "to", "from", "up", "down", "in", "out", "on", "off", "over", "under", "again", "further", "then", "once", "here", "there", "when", "where", "why", "how", "all", "any", "both", "each", "few", "more", "most", "other", "some", "such", "no", "nor", "not", "only", "own", "same", "so", "than", "too", "very", "s", "t", "can", "will", "just", "don", "should", "now"]
Create a list of top characters by mentions of their names
Mechanically, that means only adding a word to word_counts if it is the name of a character. Try using this list of single-word characters (leaving out characters like "Young Seyward", and "Lady Macduff" is referred to as "wife" in this version):
["duncan", "malcolm", "donalbaine", "macbeth", "banquo", "macduff", "lenox", "rosse", "menteth", "angus", "cathnes", "fleance", "seyward", "seyton", "boy", "lady", "messenger", "wife"]
Split the text by which character is talking
A character speaking is indicated by an (often-abbreviated) version of their name followed by a . as the first thing on a line. So for example, when Macbeth speaks it starts with "Macb." (notice how "macb" appears in the top 25 words — that is Macbeth speaking). You'll need to revise how you handle punctuation, since you can't just strip all punctuation
Create subgraphs of the most common words by character
Come up with some other fun analyses of the text!
There is no solution version of these level-up options. If you're having too much trouble, it's fine to move on without completing any of them!

In [35]:
# Your code here
In [36]:
# When counting words, skip stopwords

# geting unique word list
uniqe_words_sans_stop_word = []
stop_words = ["i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", "her", "hers", "herself", "it", "its", "itself", "they", "them", "their", "theirs", "themselves", "what", "which", "who", "whom", "this", "that", "these", "those", "am", "is", "are", "was", "were", "be", "been", "being", "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", "the", "and", "but", "if", "or", "because", "as", "until", "while", "of", "at", "by", "for", "with", "about", "against", "between", "into", "through", "during", "before", "after", "above", "below", "to", "from", "up", "down", "in", "out", "on", "off", "over", "under", "again", "further", "then", "once", "here", "there", "when", "where", "why", "how", "all", "any", "both", "each", "few", "more", "most", "other", "some", "such", "no", "nor", "not", "only", "own", "same", "so", "than", "too", "very", "s", "t", "can", "will", "just", "don", "should", "now"]


for word in words_cleaned:
    if word in words_cleaned:
        if word not in stop_words:
            uniqe_words_sans_stop_word.append(word)

uniqe_words_sans_stop_word_count = len(uniqe_words_sans_stop_word)

# output
print("Macbeth contains {} unique words".format(uniqe_words_sans_stop_word_count))
Macbeth contains 10142 unique words
In [38]:
# Create a list of top characters by mentions of their names
list_of_names = ["duncan", "malcolm", "donalbaine", "macbeth", "banquo", "macduff", "lenox", "rosse", "menteth", "angus", "cathnes", "fleance", "seyward", "seyton", "boy", "lady", "messenger", "wife"]

# filtering for name
name_mentions = [name for name in words_cleaned if name in list_of_names]
# getting name count
name_count_by_mention = {}
for name in name_mentions:
    name_count_by_mention[name] = name_count_by_mention.get(name,0)+1
# sorting by mention
name_count_by_mention_sorted = sorted(name_count_by_mention.items(), key=lambda x: x[1], reverse=True)

# output
print(f'Most mentioned name is {name_count_by_mention_sorted[0][0].capitalize()}, which is metioned {name_count_by_mention_sorted[0][1]} times.')
Most mentioned name is Macbeth, which is metioned 62 times.
In [39]:
# Split the text by which character is talking
In [40]:
# Create subgraphs of the most common words by character
Summary
Congratulations! You've got some extra practice combining various data types into useful programming patterns and done an initial analysis of a classic text!
