# 🧠 Next Word Prediction Project (Arabic NLP)
**By Imad Eddine MOUTAAHIBE**

This project focuses on building a next word prediction model for the Arabic language using a custom NLP pipeline and corpus processing.

---

## 📚 Corpus Overview
- The raw corpus contains approximately **2.28 million words**.
- Use `total_word_count.py` to verify the total word count.

---

## 🧼 Preprocessing Pipeline

1. **Clean & Normalize**  
   Run `clean_and_normalize.py` to:
   - Remove diacritics, numbers, English letters, and symbols.
   - Keep `.` and `,` to preserve sentence structure.
   - Normalize letters.
   - Output saved in the `Cleaned` folder (≈2.21M words).

2. **Sentence Creation**  
   Use `create_sentences.py` to:
   - Split the cleaned corpus into sentences.
   - Output: `sentences.json` (≈75.3K sentences).

3. **Stopword Removal from Sentences**  
   Run `filter_sentences.py` to:
   - Remove stopwords listed in `stopwords.txt`.
   - These cleaned sentences are used for **next word** and **next letter** predictions.

4. **Punctuation Removal**  
   Run `remove_punctuations.py` to:
   - Remove `.` and `,` from the cleaned corpus.

---

## 🧾 Vocabulary Processing

1. **Distinct Words with Stopwords**  
   Run `distinct_words_with_stopwords.py` to extract all distinct words.
   - Output: `distinct_words_with_stopwords.json` (≈77,295 words).

2. **Remove Stopwords**  
   Run `remove_stopwords.py`:
   - Removes 441 stopwords.
   - Output: `distinct_words.json`.

3. **Dictionary Check**  
   Run `check_dictionary.py`:
   - Compare words in `distinct_words.json` against `arabic_dictionary.txt`.
   - Valid words saved in `distinct_words_dictionary.json` (≈66,752).
   - Rejected words saved in `rejected_words_dictionary.json` (≈10,102).
   - Match rate: **86.86%**.

---

## 🧪 NLP Verification (Google Colab Only)

> Run `stem_lemma_ner.py` (requires Unix environment)

1. **Apply Stemming, Lemmatization, and NER**  
   - Valid: `valid_words_stem_lema_ner.json`  
   - Rejected: `rejected_words_stem_lema_ner.json`

2. **Stemming Verification**  
   Run `verify_stemming.py`:
   - If stem of a rejected word exists in the dictionary → accept.
   - Output:  
     - Valid: `valid_words_with_stemming.json` (17.67% recognized)  
     - Rejected: `rejected_stemming.json`

3. **Lemmatization Verification**  
   Run `verify_lemma.py`:
   - If lemma of a rejected word matches one from valid → accept.
   - Output:  
     - Valid: `valid_words_with_lemma.json` (4.02% recognized)  
     - Rejected: `rejected_lemma.json`

4. **NER Verification**  
   - If NER tag is valid (ADJ, VERB, etc.) → accept.
   - Output:  
     - Valid: `valid_words_with_ner.json` (8.90% recognized)  
     - Rejected: `rejected_ner.json`

> ✅ **Final acceptance rate**: **90.38%** of distinct words (excluding stopwords)

---

## 🔤 NLP Applications

1. **Next Letter Prediction**  
   Run `next_letter.py`:
   - Generates a heatmap based on character transitions.

2. **Next Word Prediction**  
   Run `next_word.py`:
   - Builds `next_word.json` containing top 5 predictions for each word.

3. **Word Transition Heatmap**  
   - Use `next_word_heatmap.py` to generate a visual heatmap.
   - Limited to **top 50 most frequent words** (to reduce chaos in a 68k x 68k grid!).

---

## 🤖 Final Prediction Program

- Predicts the **top 5 next words** if the input exists in `valid_words_with_lemma.json`.
- If not found, suggests **closest valid alternatives**.
- Also predicts the **next possible letters** based on `next_letter.json`.

---

## 🧠 Technologies & Notes

- Language: Python  
- NLP tasks handled manually (no high-level libraries like spaCy/NLTK used for Arabic)
- Some scripts require **Google Colab** or **Unix** due to dependencies.
