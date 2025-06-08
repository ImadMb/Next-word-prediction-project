- we have our corpus that's around 2.28m words long which can be tested with total_word_count.py
- clean and normalize our corpus using clean_and_normalize.py to remove diacritics, numbers, english letters and symboles but we leave '.' and ',' to be able to make sentences and normalize letters and save to a new folder 'CLeaned' which is of size 2.21m
- we cut our Tech corpus to sentences using create_sentences.json and save them to sentences.json which have 75.3k sentences
- these sentences also need removing stopwords from them using filter_sentences.py which removes all stopwords that are stored in stopwords.txt (these sentences will later be used in next letter and next word)

- now we need to filter '.' and ',' from our Cleaned corpus using remove_punctuations.py
- now we go back to our Cleaned corpus to extract all distinct words using distinct_words_with_stopwords.py and storing these distinct words in distinct_words_with_stopwords.json which have 77295 distinct words including stop words saved to distinct_words_with_stopwords.json
- now we need to filter stop words from these distinct words using remove_stopwords.py which removes 441 stop words and saves the remaining words in distinct_words.json
- now we need to compare these distinct words in distinct_words.json with words in an arabic dictionary arabic_dictionary.txt using check_dictionary.py, if the word is found, it'll be saved to distinct_words_dictionary.json(66752 / 76854 (86.86%)), else it'll be saved to rejected_words_dictionary.json (10102)
- we have to apply stemming, lemmatization and ner to these files using stem_lemma_ner.py but this files only works in collab since it needs a unix environment, the processed valid words are saved to valid_words_stem_lema_ner.json, and the processed rejected words in rejected_words_stem_lema_ner.json

- we now test the rejected words by using stemming, we compare the stems of each word in rejected and if the stem exists in the dictionary then it is accepted, we use verify_stemming.py, we recognize 1885 of 10668 words (17.67%) and save them to valid_words_with_stemming.json, the rejected words are saved to rejected_stemming.json
- same thing, now we use lemmatization, we verify the lemma of each word rejected by stemming, if the lemma of the rejected word matches the lemma of the accepted words then it is added to valid_words_with_lemma.json using verify_lemma.py, we recognize 348 of 8660 words (4.02%), and the rejected are saved to rejected_lemma.json
- finally we use ner, we verify if a word in rejected_lemma.json has a valid ner value (ADJ, VERB etc..) if it does it is saved to valid_words_with_ner, if not(X) then it is saved to rejected_ner.json we recognized 731 of 8216 words (8.90%)
- so the total percentage of accepted words is 90.38% compared to distinct words without stopwords


- going back to our sentences.json, we create a next letter heat map using next_letter.py
- we create next_word.json which has the top 5 next words for all words in valid_words_with_lemma.json
- since it would be chaotic to make a 68856*68856 heat map, we only take the top 50 words with biggest count and make a heat map using next_word_heatmap.py
- finally we make a program that predicts 5 next words if the word exists in distinct_words_with_lemma.json and if it doesn't eixts it suggests possible correct words, it also predicts next letters using next_letter.json.
