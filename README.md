# Web-scraping-and-nltk
Web scraping &amp; Machine Learning in Python

In this section we will learn how to build a data science pipeline to plot frequency distributions of words from 'Project Gutenberg', also learn how to scrap data using BeautifulSoup.

Using our scrapped data we will learn about important aspects of Natural Language Processing (NLP) like word tokenization and stopwords (NLTK),and lastly we can get 'word frequency distributions' of any novel that you can find on Project Gutenberg and visualize our data using matplotlib.

What we will learn today

Scrap data using BeautifulSoup
Python NLP using NLTK
data visualization using matplotlib

Get Data from 'Project Gutenberg'-
#Store url
url = 'https://www.gutenberg.org/files/2701/2701-h/2701-h.htm'
import requests
from bs4 import BeautifulSoup
# Make the request
r = requests.get(url)
# Extract HTML from Response object
html = r.text

#Get the Text from the HTML
soup = BeautifulSoup(html, "html5lib")

#From these soup objects, you can extract all types of interesting
#information about the website you're scraping, such as title:
print(soup.title.string)

# Get hyperlinks from soup and check out first 6
soup.findAll('a')[:6]

# Get the text out of the soup and print it
text = soup.get_text()
print(text)

Next use nltk, the Natural Language Toolkit, to

Tokenize the text (fancy term for splitting into tokens, such as words);
Remove stopwords (words such as 'a' and 'the' that occur a great deal in ~ nearly all English language texts.
# Import RegexpTokenizer from nltk.tokenize
from nltk.tokenize import RegexpTokenizer
# Create tokenizer
tokenizer = RegexpTokenizer('\w+')

# Create tokens
tokens = tokenizer.tokenize(text)
print(tokens[:8])

# Initialize new list
words = []


# Loop through list tokens and make lower case
for word in tokens:
    words.append(word.lower())

# Print some words
print(words[:8])

# Import nltk
import nltk

# Get English stopwords and print some of them
sw = nltk.corpus.stopwords.words('english')
print(sw[:5])
# Initialize new list
words_ns = []

# Add to words_ns all words that are in words but not in sw
for word in words:
    if word not in sw:
        words_ns.append(word)

# Print list items 
print(words_ns[:5])

#We can now plot a frequency histogram of words in Moby Dick in two line of
#code using nltk. To do this,
#we create a frequency distribution object using the function nltk.FreqDist();
#Import datavis libraries
import matplotlib.pyplot as plt
import seaborn as sns

# Figures inline and set visualization style
sns.set()

# Create frequency distribution and plot

freqdist1 = nltk.FreqDist(words_ns)

freqdist1.plot(25)
