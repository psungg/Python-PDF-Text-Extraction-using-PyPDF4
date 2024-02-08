# Python-PDF-Text-Extraction-using-PyPDF4

To create a PdfFileReader Object:

    pdfFileReaderObject.getPage(pageNum
    
    eg. pageObject = pdfReader.getPage(0)
    
To extract text from the pageObject (return string)

    pageObject.extractText()
    
    eg. text = pageObject.extractText()

1. Create PdfFileReader Object #### to read PDF #####
2. Access the target page for text extraction (get the pageObject)
3. Extract text from page object
4. Print out the extracted text

## Specific Page

```python
import PyPDF4

pdfFileName = "PortfolioTest.pdf"

pdfReader = PyPDF4.PdfFileReader(pdfFileName)
pageObject = pdfReader.getPage(0) #### page number to extract starting with 0 ####

extractedText = pageObject.extractText()

print(extractedText)
```

## All Page

```python
pdfFileName = "PortfolioTest.pdf"

pdfReader = PyPDF4.PdfFileReader(pdfFileName)
for page in pdfReader.pages:
    print(page.extractText())
```

## PDF to Docx Converter

```python
pip install pdf2docx
```

1. Specify the file paths for both PDF file and Docx file location
2. Create Converter Object
3. Convert PDF file to docx file

```python
from pdf2docx import Converter
pdfFile = "PortfolioTest.pdf"
docxFile = "PortfolioTest.docx"

cv = Converter(pdfFile)
cv.convert(docxFile)
```

## Audiobook (Offline Text to Speech)

1. Use PyPDF4 and pyttsx3
2. The library supports the following engines:
        
        sapi5: SAPI5 on Windows
        
        nsss: NSSpeechSynthesizer on Mac OS X
        
        Espeak: eSpeak on every other platform
        
3. To initialize pyttsx3

        pyttsx3.init()
        
        eg. engine = pypttsx3.init()
        
4. The text to speech engine object has the following properties:

        rate: a engine speech rate in words per minute, 200 by default (integer)
        
        voice: a identifier of the active voice (string)
        
        volume: a volume in the range of 0.0 -1.0, 1.0 by default (float)
        
        voices: a list of pyttsx3.voice.Voice descripter objects, containing the information about a speech synthesizer voice

1. Import the module and initialize the object
2. Read the pdf using pdfFileReader
3. Count the number of pages and run the loop till the last page
4. Extract text from each page
5. Convert text to speech and speak
6. Save the text as audio file

```python
import PyPDF4
import pyttsx3

engine = pyttsx3.init()

voices = engine.getProperty("voices")
engine.setProperty("rate", 220)
engine.setProperty("volume", 1.0)
engine.setProperty("voice", voices[7].id)

to_read_file = "PortfolioTest_Part1.pdf"
pdfReader = PyPDF4.PdfFileReader(to_read_file)

for page in range(pdfReader.getNumPages()):
    text = pdfReader.getPage(page).extractText()
    engine.say(text)
    engine.runAndWait()
engine.stop()

engine.save_to_file(text, "PortfolioAudio.mp3")
engine.runAndWait()
print("Done!")
```

## Read me the Text

gtts stands for Google Text to Speech

To create object:
    
    gtts.gTTS()
    
Parameter

    text: the text to convert to speech (string)
    
    tld: speaking accent (string,optional) Defult is .com
    
    lang: The language to read the text in (string,optional) Default is en
    
    slow: Read text more slowy (boolean, optional) Default is False
    
eg.

    gtts.GTTS("Hello World",tld = "co.uk", lang = "en", slow = False)

Write the result to MP3 file

    gtts.gTTS.save(path/filename)
    
Show available language in gtts

    gtts.lang.tts_langs()

Playsound Module

    pip install playsound
    
To import

    import playsound
    
eg.
    
    playsound.playsound("/Users/Psungg/Desktio/hello.mp3)

1. import the modules: gtts and playsound
2. Prepare the text to be converted
3. Specify the language and accent to use
4. Create a gtts object and convert text to speech
5. Save the audio in MP3 file
6. Play the MP3 file

```python
pip install playsound
```

```python
import gtts
gtts.lang.tts_langs()
```

```python
import gtts
import playsound

mytext = "Hello Everyone, Welcome to Python Lab Class"
language = "en"

gttsObject = gtts.gTTS(text = mytext, tld = "co.uk", lang = language, slow = False)
gttsObject.save("Welcome.mp3")

playsound.playsound("Welcome.mp3")
print("Done!")
```
