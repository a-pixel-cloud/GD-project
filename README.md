# Overview
The __objective__ of this project is to attempt the implementation of the polar questions with a special focus on the *clitic* in Russian. A __polar question__ is a question that requires a *yes-no answer*. One of the ways to ask such questions in Russian is to change the intonation of declarative sentences, or to put the word in question at the biginning of a sentence. This word usually bears prosodic information, and to get more emphasis, it can also be followed by a clitic *li*. 

## Short description of the phenomena
The phenomenon of yes-no questions in Russian involves many aspects, such as word order, copula, clitics, topic/focus, and constituent structure. We will not consider embedded sentences but focus solely on simple present and past tense questions.

Russian shares some features of non-configurational languages, i.e., extensive case system and pro-drop, making it a free word order language. However, King (1993) assumes that the non-configurational properties of Russian are misleading. Word order is not free since it encodes topic and focus information. King (1993) proposes that Russian has __SVO word order with scrambling constituents__.

In questions with *li* the main focus is the questioned element which appears in the left-most position (King 1993). Clitic *li* lets the constituents scramble within the sentence (Butt et al. 2021). The questioned element can be an __NP, PP, AP, or AdvP__. When one of the constituents is an initial element, __it is focused and questioned__. Polar *li* is enclitic, so it __cannot occur in initial or final sentence position__. 
For instance, in the sentence below the speaker asks about __the book being read__ but not the magazine or newspaper. All the constituents receive their focus reading from clitic *li*.

- *__Knigu li__ on chitaet?* / Is he reading a __book__? or Is it __a book__ that he is reading?

## Reasons for choice
The topic has been selected for a number of reasons. There is a strong iterest in Slavic clitics in general and particularly in their prosodic features. The topic itself is complex and challenging, as it incorporates both topic/focus and prosodic structure. In this regard, the works of Butt et al. (2020) and Bögel et al.(2010) on syntax-prosody interface inspired the idea for this implementation. 

## Challenges
Since in Russian *li* follows the first prosodic word, __clitic placement is solely prosodic__. This means that the c-structure cannot bear the prosodic requirements of forming constituents but must follow syntactic requirements. Considering that, it is challenging syntactically provide a c-structure which can satisfy both syntactic and prosodic needs. 




# Implementation approach/design

## Testsuite design
The testsuite consists of a total of __18 sentences__. Among them are __three ill-formed sentences__ with wrong clitic positions (sentence initial, sentence final, and in the middle). 

The remaining __15 correct sentences__ also form *three constituent groups* where: __NP; PP, or AdvP__ is a questioned element/ focus of the sentence. The constituent group also includes *a declarative sentence, and polar question __with and without__ clitic *li**. The section with NP constituents contains the largest number of the sentences in the testsuite. 

Each sentence example is preceeded by a comment/translation in English. The Russian sentence examples are romanized.

## Setup 
- used Encodeing: utf-8! for romanized text.
- in CONFIG section ROOTCAT changed the root from S to CP.
- in LEXENTRIES, TEMPLATES, RULES, MORPHOLOGY used (DEMO RUSSIAN).

## Phrase structure rules
The following phrase-structure rules were proposed in order to implement sentences with clitics (King, 1993, Hristov, 2021):
- CP  ->   XP  C'
- C'  ->   C  IP
- IP  ->   XP   I'

where XP is either NP, PP, AP, or AdvP. 

An XP in CP surves as a __FOCUS__, whereas XP in IP functions as a __TOPIC__ of the utterance. __Clitic__ as an interrogative complementizer is in __C__ node and assigns __FOCUS__ feature.

## Templates
The existing templates *common.templates.lfg* have been utilised. An additional template for grammatical functions (GF) has been developed.

## Remaining challenges and further research directions
In the course of implementing the grammar, we encountered the following issues:

- in the phrase-structure rules it was not feasible to unify the constituents under the common XP node. Therefore, we included NP, PP and AdvP separately in the CP root node.
- the sentences with an initial NP were parsed showing both c- and f-structure. In contrast, the examples with a PP or AdvP as a focus did not produce relevant f-stucture, but displayed only c-structure.

It is recommended that future research implement the architecture framework for a syntax-prosody interface as proposed by Bögel et al.(2010).

# Files submitted

- grammar.lfg (code with implementation)
- testsuite.lfg (example sentences with English translation)
- readme.md (.md for github)
- common.templates.lfg (for templates)
- basic-parse-tok.fst (tokenizer for parsing)
- default-gen-tokenizer.fst
- english.infl.patch.full.fst

  ## Files to ignore
- .DS Store (a file generated automatically after uploading the files via the command line)
- .gitignore! (the disturbing .DS Store file was added here)
  

# A link to GitHub repository
https://github.com/a-pixel-cloud/GD-project.git


# References

1. Bresnan, Joan. 2001. Lexical-functional syntax. Malden, Mass. [u.a.]: Blackwell.
2. Butt, Miriam et al. 1999. A grammar writer’s cookbook. Stanford, Calif.: CSLI Publications.
3. Butt, Miriam, Farhat Jabeen & Tina Bögel. 2020. Ambiguity resolution via the syntax-prosody interface: The case of kya ‘what’ in Urdu/Hindi. In Gerrit Kentner (ed.), Joost Kremers (ed.) Prosody in syntactic encoding, 85-118. Berlin: De Gruyter. https://kops.uni-konstanz.de/entities/publication/0381084e-e2ca-4c3b-a400-c9f3bf447e19.
4. Bögel, Tina et al. 2010. Second position and the prosody-syntax interface. Proceedings of the LFG10 conference. Stanford: CSLI Publications, 106-126. https://kops.uni-konstanz.de/entities/publication/82c7a535-15ff-4e7f-afcd-c72ae2e5ae12.
5. Börjars, Kersti, Rachel Nordlinger & Louisa Sadler. 2019. Lexical-functional grammar: an introduction. Cambridge, United Kingdom New York, NY, USA Port Melbourne, Australia New Delhi, India Singapore : Cambridge University Press.
7. Dalrymple, Mary.2001. Lexical functional grammar. San Diego, Calif. [u.a.]: Acad. Press.
8. Franks, Steven & King, Tracy Holloway. 2000. A Handbook of Slavic Clitics. New York [u.a.]: Oxford University Press.
9. Hristov, Bozhil. 2021. LFG and Slavic languages. In Dalrymple, Mary (ed.). Handbook of Lexical Functional Grammar, i-lii. Berlin: Language Science Press. https://www.academia.edu/50978273/LFG_and_Slavic_languages_2021_In_Dalrymple_Mary_ed_Handbook_of_Lexical_Functional_Grammar_Berlin_Language_Science_Press. 
10. King, Tracy Holloway. 1993. Configuring topic and focus in Russian. Doctoral dissertation. Stanford, Calif.: Stanford University.
11. Kroeger, Paul. 2004. Analyzing syntax: a lexical-functional approach. Cambridge [u.a.]: Cambridge University Press.



