# MAI 5201 Homework 0: Text Processing Fundamentals

## Table of Contents
- [Introduction](#introduction)
- [Part 1: Regular Expressions (30 pts)](#part-1-regular-expressions-30-pts) - Questions 1-6
- [Part 2: Tokenization & Normalization (20 pts)](#part-2-tokenization--normalization-20-pts) - Questions 8-10, 12
- [Extra Credit (+20 pts)](#extra-credit-optional) - Questions 7, 11 (Optional)
- [Grading & Submission](#grading--submission)

## Introduction

Welcome to your first homework for MAI 5201! This assignment covers the fundamental text processing techniques that form the foundation of all NLP systems. You'll work with real-world text data and implement solutions that power everything from search engines to chatbots.

**🌟 Why This Matters:**
Every NLP system - from Google Search to ChatGPT to Grammarly - starts with the techniques you'll learn here. Text preprocessing determines whether your model sees "cats", "cat's", and "CATS" as the same concept or different ones. Get this wrong, and even the most sophisticated neural networks will struggle!

**What you'll learn:**
- **Regular Expressions**: The Swiss Army knife of text processing - used in everything from email validation to web scraping
- **Tokenization**: How to break text into meaningful units (spoiler: it's trickier than splitting on spaces!)
- **Text Normalization**: Converting messy real-world text into clean, consistent formats
- **Modern Algorithms**: BPE (used in GPT models) and edit distance (powering spell checkers everywhere)

**Real-World Applications You'll Build:**
- Extract contact information from unstructured text (like a business card scanner)
- Parse complex server logs (essential for web analytics and debugging)
- Build a spell checker using edit distance (just like your phone's autocorrect)
- Implement the same tokenization algorithm used in GPT and BERT models

**Structure:**
1. **Part 1**: Regular Expressions (30 pts) - Q1-Q6: Core pattern matching skills
2. **Part 2**: Tokenization & Normalization (20 pts) - Q8-Q10, Q12: Essential NLP preprocessing  
3. **Extra Credit**: Advanced techniques (20 pts) - Q7, Q11: Log parsing and modern tokenization algorithms (Optional)

**Due Date**: August 9, 2025 at 11:59 PM (Guyana time)

This project includes an autograder for you to test your solutions locally:
```bash
python autograder.py
```

Access all starter code and supporting files in the `src` directory: [📁](src/)

---

## Part 1: Regular Expressions (30 pts)

Regular expressions are the secret weapon of text processing - a concise way to find patterns in text that would take hundreds of lines of code otherwise. Think of them as super-powered search patterns that can find phone numbers, extract URLs, or validate email addresses with just a few characters.

**📌 Important Note**: Part 1 includes Questions 1-6 (30 points total). Question 7 (Complex Log File Parsing) is an **Extra Credit** question worth +5 points and is covered in the [Extra Credit](#extra-credit-optional) section below.

**Real-World Impact**: 
- **Google**: Uses regex for search query parsing and web crawling
- **Social Media**: Twitter, Instagram use regex to detect hashtags and mentions
- **Cybersecurity**: Regex patterns detect malicious URLs and suspicious log entries
- **Data Science**: Essential for cleaning messy datasets before analysis

**💡 Pro Tips for Success**:
- Use [regex101.com](https://regex101.com) to test your patterns interactively
- Start simple, then add complexity gradually
- Remember: `.*` is greedy (matches as much as possible), `.*?` is lazy (matches as little as possible)
- Use named groups `(?P<name>...)` for cleaner code

### Files you'll edit:
- `src/regex_exercises.py`: Your regex implementations
- `src/tokenization.py`: Your tokenization implementations

### Files you can use:
- `src/data/`: Sample text files for testing
- `src/autograder.py`: Automated testing system

---

### Q1 (5 pts): Email and URL Extraction

**🎯 What You're Building**: A smart text scanner that can automatically find and extract contact information from any text - just like business card scanning apps or CRM systems that process customer emails.

**Why It Matters**: Every day, companies process millions of documents, emails, and web pages to extract contact information. Your regex skills here directly translate to building web scrapers, data extraction pipelines, and automated contact discovery systems.

**Real-World Applications**:
- **LinkedIn**: Finds and suggests email addresses from uploaded documents
- **Sales Tools**: Automatically extract leads from business directories
- **Email Security**: Detect suspicious links and phishing attempts
- **Web Scraping**: Extract structured data from unstructured web pages

**💡 Challenge Hints**:
- URLs can start with `http://`, `https://`, or just `www.`
- Don't forget about `.edu.gy` domains (local Guyanese institutions!)
- Email regex: Start with the simple pattern, then handle edge cases like `user+tag@domain.com`

**In this question, your task is to** implement regex patterns to extract emails and URLs from text. This is commonly used in web scraping, social media analysis, and data cleaning.

**Test your implementation:**
```bash
python autograder.py -q q1
```

**Example:**
```python
text = "Contact us at info@university.edu or visit https://www.uog.edu.gy for more information."
emails = extract_emails(text)  # ['info@university.edu']
urls = extract_urls(text)      # ['https://www.uog.edu.gy']
```

---

### Q2 (5 pts): Phone Number Normalization

**🎯 What You're Building**: A smart phone number processor that can recognize phone numbers in any format and convert them to a standard format - essential for customer databases and contact management systems.

**Why It Matters**: Customer data comes in messy formats. Your e-commerce site might receive orders with phone numbers like "592 123 4567", "(592) 123-4567", or "+592-123-4567". Your system needs to recognize these are all the same number!

**Real-World Applications**:
- **Twilio/WhatsApp**: Normalize phone numbers before sending messages
- **Banking**: Verify customer phone numbers across different systems
- **Emergency Services**: Quickly parse caller information from various formats
- **Marketing**: Deduplicate customer lists and prevent spam

**🌍 Cultural Note**: In Guyana, phone numbers follow the pattern +592-XXX-XXXX. Your regex should handle local patterns while being flexible enough for international formats.

**💡 Pro Tips**:
- Use `\d` for digits, but remember some formats use letters (like 1-800-FLOWERS)
- Parentheses `()` are special in regex - escape them as `\(` and `\)` to match literally
- Consider non-breaking spaces and Unicode characters in international data

**In this question, your task is to** create regex patterns to identify and normalize phone numbers in various formats. This is essential for customer data processing and contact information standardization.

**Test your implementation:**
```bash
python autograder.py -q q2
```

**Example:**
```python
text = "Call me at (592) 123-4567 or 592.123.4567 or +592-123-4567"
phones = extract_phone_numbers(text)  # ['(592) 123-4567', '592.123.4567', '+592-123-4567']
normalized = normalize_phone_number("592.123.4567")  # "+592-123-4567"
```

---

### Q3 (5 pts): Social Media Text Processing

**🎯 What You're Building**: A social media analyzer that can extract hashtags, mentions, and emojis - the core technology behind social media monitoring tools and sentiment analysis platforms.

**Why It Matters**: Social media generates 500 million tweets daily! Companies spend billions on social media monitoring to track brand mentions, trending topics, and customer sentiment. Your regex patterns are the first step in this multi-billion dollar industry.

**Real-World Applications**:
- **Hootsuite/Buffer**: Track brand mentions across platforms
- **Election Monitoring**: Analyze political sentiment and trending topics
- **Crisis Management**: Detect negative sentiment and respond quickly
- **Influencer Marketing**: Identify trending hashtags and key influencers

**🔥 Fun Fact**: The hashtag was invented by Chris Messina in 2007 on Twitter. Now there are over 125 million hashtags used daily across all platforms!

**💡 Emoji Challenge**: 
- Modern emojis are Unicode characters that can be 1-4 bytes long
- Some "emojis" are actually combinations (👨‍👩‍👧‍👦 is 4 separate characters!)
- For this assignment, focus on the most common single-character emojis

**In this question, your task is to** implement patterns to extract hashtags, mentions, and emojis from social media text. This is crucial for sentiment analysis and social media monitoring.

**Test your implementation:**
```bash
python autograder.py -q q3
```

**Example:**
```python
tweet = "Great day at @UofG! #university #education 🎓 Looking forward to graduation! 🎉"
hashtags = extract_hashtags(tweet)  # ['university', 'education']
mentions = extract_mentions(tweet)  # ['UofG']
emojis = extract_emojis(tweet)      # ['🎓', '🎉']
```

---

### Q4 (5 pts): Date and Time Extraction

**🎯 What You're Building**: A temporal information extractor that can find dates and times in any format - the backbone of calendar applications, event processing systems, and time-series analysis.

**Why It Matters**: Every email, document, and webpage contains temporal information. Financial systems process millions of timestamped transactions, news algorithms extract event dates, and personal assistants parse "meet me next Tuesday at 3pm" into calendar events.

**Real-World Applications**:
- **Google Calendar**: Extracts event times from email invitations
- **Financial Trading**: Parse timestamps from transaction logs for fraud detection
- **News Analysis**: Extract event dates to build timelines
- **Legal Discovery**: Find relevant documents by date ranges in litigation

**⏰ Time Zone Challenge**: Different cultures format dates differently:
- **US**: MM/DD/YYYY (July 25, 2025)
- **Europe**: DD/MM/YYYY (25/07/2025)
- **ISO Standard**: YYYY-MM-DD (2025-07-25)
- **Natural Language**: "next Tuesday", "in two weeks"

**🚨 Edge Case Alert**: 
- Don't forget AM/PM indicators and 24-hour time formats!

- February 29th only exists in leap years. Your regex doesn't need to validate this, but real systems do!

**In this question, your task is to** create regex patterns to extract dates and times in multiple formats. This is important for temporal information extraction and event processing.

**Test your implementation:**
```bash
python autograder.py -q q4
```

**Example:**
```python
text = "The meeting is on July 25, 2025 at 3:30 PM. Also consider 2025-07-25 14:30:00."
dates = extract_dates(text)  # ['July 25, 2025', '2025-07-25']
times = extract_times(text)  # ['3:30 PM', '14:30:00']
```

---

### Q5 (5 pts): Document Structure Extraction

**🎯 What You're Building**: A document intelligence system that can automatically understand document structure - the technology behind PDF parsers, academic search engines, and documentation tools.

**Why It Matters**: The world generates 2.5 quintillion bytes of unstructured document data daily. Companies like Adobe, Microsoft, and Google have built billion-dollar businesses around extracting structure from documents. Your regex skills are the foundation of these systems.

**Real-World Applications**:
- **GitHub**: Automatically generates documentation navigation from README files
- **Academic Search**: Google Scholar extracts citations to build research networks
- **Legal Tech**: Contract analysis tools extract clauses and references
- **Technical Writing**: Documentation tools auto-generate table of contents

**📚 Citation Gold Mine**: Academic papers contain a wealth of structured information:
- Author names, publication years, journal names
- DOI links, page numbers, volume information
- Conference proceedings, book chapters, arXiv preprints

**💡 Markdown Mastery**:
- Headers: `#` (h1), `##` (h2), `###` (h3) - each level has specific meaning
- Code blocks can be inline `` `code` `` or fenced with triple backticks
- Citations often follow patterns like "(Author et al., 2023)" or "[1]"

**In this question, your task is to** implement patterns to extract structured information from documents, such as sections, citations, and code blocks. This is essential for document parsing and information extraction systems.

**Test your implementation:**
```bash
python autograder.py -q q5
```

**Example:**
````python
document = """
# Introduction
This is the introduction section.

## 1.1 Background
Some background information (Smith et al., 2023).

```python
print("Hello, World!")
```

"""
sections = extract_sections(document)     # ['Introduction', '1.1 Background']
citations = extract_citations(document)  # ['Smith et al., 2023']
code_blocks = extract_code_blocks(document)  # ['print("Hello, World!")']
````

---

### Q6 (5 pts): Address Extraction

**🎯 What You're Building**: A geographic information extractor that can parse addresses from unstructured text - the core technology powering delivery apps, location services, and geographic databases.

**Why It Matters**: Every day, UberEats processes millions of delivery addresses, real estate sites parse property listings, and logistics companies optimize routes based on extracted location data. Getting addresses right is literally a matter of getting your pizza delivered to the right place!

**Real-World Applications**:
- **Delivery Services**: DoorDash, UberEats extract addresses from customer messages
- **Real Estate**: Zillow parses property listings from multiple sources
- **Emergency Services**: 911 systems extract location information from calls
- **Logistics**: FedEx, UPS optimize delivery routes using address parsing

**🇬🇾 Local Flavor**: Guyanese addresses have unique patterns:
- **Georgetown**: Often include ward numbers and lot numbers
- **Regional**: Villages, counties, and traditional names
- **P.O. Boxes**: Still commonly used across the country
- **Berbice, Essequibo, Demerara**: The three historic counties

**💡 Address Parsing Challenges**:
- Street vs. Street vs. St. (abbreviation variations)
- Apartment/Unit numbers can come before or after street address
- International addresses have completely different formats
- Some addresses use landmarks instead of street numbers ("across from the market")

**In this question, your task is to** implement patterns to extract physical addresses from text. This is crucial for location-based services, delivery systems, and geographic information extraction.

**Test your implementation:**
```bash
python autograder.py -q q6
```

**Example:**
```python
text = """
Visit us at 123 Main Street, Georgetown, Guyana or 
our branch office at 456 Water St., New Amsterdam, Berbice.
Mailing address: P.O. Box 789, Georgetown, GY 12345
"""
addresses = extract_addresses(text)  
# ['123 Main Street, Georgetown, Guyana', '456 Water St., New Amsterdam, Berbice', 'P.O. Box 789, Georgetown, GY 12345']

# Extract address components
address = "123 Main Street, Georgetown, Guyana"
components = parse_address_components(address)
# {'street': '123 Main Street', 'city': 'Georgetown', 'country': 'Guyana'}
```

---

## Part 2: Tokenization & Normalization (20 pts)

Welcome to the heart of modern NLP! Tokenization and normalization might seem simple, but they're where many NLP projects succeed or fail. Every word that ChatGPT, Google Translate, or Siri processes has passed through tokenization algorithms similar to what you'll build here.

**📌 Important Note**: Part 2 includes Questions 8, 9, 10, and 12 (20 points total). Question 11 (BPE Implementation) is an **Extra Credit** question worth +15 points and is covered in the [Extra Credit](#extra-credit-optional) section below.

**🤯 Mind-Blowing Fact**: Modern language models like GPT-4 use sophisticated tokenization to handle words they've never seen before. You'll learn the fundamentals that make this possible!

**Why Tokenization Matters**:
- **Search Engines**: Google tokenizes billions of web pages daily
- **Machine Translation**: Breaking text into meaningful units is crucial for translation accuracy
- **Chatbots**: Understanding user intent depends on proper tokenization
- **Voice Assistants**: Converting speech to text requires sophisticated tokenization

**The Hidden Complexity**:
- "Don't" → ["Don", "'t"] or ["Don't"]? The choice affects your model's understanding
- "New York" → ["New", "York"] loses the fact that it's one city
- "email@company.com" → How do you preserve the email while splitting other text?
- "COVID-19" → The hyphen carries meaning - splitting it changes semantics

**� Core Skills You'll Master**:
- **Basic Tokenization**: Whitespace, punctuation, and sentence splitting
- **Advanced Patterns**: Handling contractions, URLs, and special cases
- **Text Normalization**: Converting messy real-world text into clean, consistent formats
- **Edit Distance**: The math behind spell checkers and autocorrect

### Files you'll edit:
- `src/tokenization.py`: Your tokenization implementations
- `src/normalization.py`: Text normalization functions

### Files you can use:
- `src/data/`: Sample text files for testing
- `src/autograder.py`: Automated testing system

---

### Q8 (5 pts): Basic Tokenization

**🎯 What You're Building**: The foundation of all text processing - algorithms that break text into meaningful units. This is literally the first step in every NLP pipeline, from search engines to chatbots.

**Why It's Harder Than It Looks**: 
- Spaces aren't universal separators (Chinese and Japanese don't use them!)
- Punctuation can be part of words ("U.S.A.") or separate ("Hello!")
- Contractions break normal rules ("can't" = "can" + "not"?)

**Real-World Applications**:
- **Search Engines**: Must tokenize queries and documents identically for accurate matching
- **Social Media**: Twitter's 280-character limit depends on how you count "characters" vs. "tokens"
- **Legal Tech**: Contract analysis requires precise sentence and clause boundaries
- **Academic Tools**: Citation managers must split references into component parts

**💡 Design Decisions You'll Face**:
- Should "U.S.A." be one token or three?
- Is "don't" one word or two?
- How do you handle URLs and email addresses?
- What about emoticons like ":)" ?

**⚡ Performance Tip**: Your tokenizer will process millions of words. Use efficient string operations and avoid unnecessary regex when simple splits work!

**In this question, your task is to** implement different tokenization strategies: whitespace, punctuation-aware, and sentence tokenization.

**Test your implementation:**
```bash
python autograder.py -q q8
```

**Example:**
```python
text = "Hello, world! How are you today? I'm doing well."
tokens = whitespace_tokenize(text)      # ['Hello,', 'world!', 'How', 'are', 'you', 'today?', "I'm", 'doing', 'well.']
tokens = punctuation_tokenize(text)    # ['Hello', ',', 'world', '!', 'How', 'are', 'you', 'today', '?', 'I', "'m", 'doing', 'well', '.']
sentences = sentence_tokenize(text)    # ['Hello, world!', 'How are you today?', "I'm doing well."]
```

---

### Q9 (5 pts): Contraction and Special Case Tokenization

**🎯 What You're Building**: Advanced tokenization that handles the messy realities of human language - contractions, hyphenated words, and embedded URLs. This separates amateur text processors from production-ready systems.

**The Contraction Conundrum**: 
English has hundreds of contractions, each with different rules:
- "can't" → "can" + "not" (irregular: "cannot")
- "I'll" → "I" + "will" (could also be "I shall")
- "y'all" → "you" + "all" (regional variation)
- "would've" → "would" + "have" (nested contraction)

**Real-World Applications**:
- **Voice Assistants**: Siri must understand "I'd like to..." = "I would like to..."
- **Sentiment Analysis**: "don't love" vs "do not love" - contractions affect sentiment
- **Machine Translation**: Contractions don't exist in all languages
- **Academic Analysis**: Formal vs. informal language detection

**🌐 URL Challenge**: Modern text is full of URLs that should stay intact:
- `www.example.com` - simple case
- `https://api.example.com/v1/users?id=123&format=json` - complex parameters
- `bit.ly/abc123` - shortened URLs
- `example.com/path_(with_parentheses)` - special characters

**💡 Hyphenation Hints**:
- "Twenty-first" → keep together (compound number)
- "State-of-the-art" → keep together (compound adjective)
- "Self-driving" → keep together (compound modifier)
- "Re-enter" → could split at prefix

**In this question, your task is to** handle special cases like contractions, hyphenated words, and URLs within text.

**Test your implementation:**
```bash
python autograder.py -q q9
```

**Example:**
```python
text = "I can't believe it's twenty-first century! Visit www.example.com for more info."
tokens = advanced_tokenize(text)  # ['I', 'ca', "n't", 'believe', 'it', "'s", 'twenty-first', 'century', '!', 'Visit', 'www.example.com', 'for', 'more', 'info', '.']
```

---

### Q10 (5 pts): Text Normalization

**🎯 What You're Building**: A text cleaning pipeline that converts messy, inconsistent real-world text into a standardized format. This is the secret sauce that makes search engines find "café" when you type "cafe".

**Why Normalization Saves the Day**:
- Users type "URGENT!!!" but you want to match "urgent"
- International text has accents: "naïve" should match "naive"
- Social media has creative spelling: "sooooo good" → "so good"
- Copy-paste introduces invisible Unicode characters that break everything

**Real-World Applications**:
- **Search Engines**: Google normalizes queries to match documents regardless of capitalization or accents
- **E-commerce**: Product searches must handle "iPhone" = "iphone" = "IPHONE"
- **Social Media**: Hashtag matching requires normalization (#CoffeeLover = #coffeelover)
- **Academic**: Citation matching across different formatting styles

**🌍 Unicode Challenges**:
The world has 149,186 characters in Unicode! Your normalization must handle:
- **Accented characters**: é, ñ, ü, ç (thousands of combinations)
- **Ligatures**: fi, fl (single characters that look like two)
- **Different scripts**: Cyrillic А looks identical to Latin A but has different Unicode codes
- **Emoji variants**: 👍 vs 👍🏽 (same gesture, different skin tones)

**💡 Normalization Strategy**:
1. **Case folding**: "iPhone" → "iphone" (more than just `.lower()`!)
2. **Accent removal**: "café" → "cafe" (Unicode decomposition)
3. **Punctuation handling**: "hello!!!" → "hello" (preserve meaning, remove noise)
4. **Whitespace cleanup**: "hello    world" → "hello world"

**⚠️ Cultural Sensitivity**: Some normalizations change meaning:
- Turkish has dotted and dotless I (İ/ı vs I/i)
- German ß ≠ ss in some contexts
- Chinese traditional vs simplified characters carry cultural significance

**In this question, your task is to** implement functions to normalize text: lowercase conversion, removing accents, and handling special characters.

**Test your implementation:**
```bash
python autograder.py -q q10
```

**Example:**
```python
text = "The café in São Paulo serves EXCELLENT coffee!!!"
normalized = normalize_text(text)  # 'the cafe in sao paulo serves excellent coffee'
```

---

### Q12 (8 pts): Edit Distance Applications

**🎯 The Swiss Army Knife of String Algorithms**: Implement Levenshtein edit distance and watch it power spell checkers, autocorrect systems, DNA analysis, and fraud detection. This single algorithm has applications across virtually every field involving text or sequences!

**🧬 The Fascinating History**: 
Created by Vladimir Levenshtein in 1965 for error-correcting codes, edit distance is now used in:
- **Bioinformatics**: Comparing DNA sequences to find evolutionary relationships
- **Plagiarism Detection**: Measuring document similarity
- **Version Control**: Git uses edit distance for merge conflict resolution
- **Machine Translation**: Evaluating translation quality
- **Fuzzy Matching**: Database record deduplication

**Why Dynamic Programming Is Magic**:
The naive approach to find edit distance is exponential - checking every possible sequence of edits. But with DP, you solve it in O(mn) time by building up solutions to subproblems. This is a classic example of how the right algorithm transforms an impossible problem into a trivial one!

**Part A: The Core Algorithm (5 pts)**
You'll implement the fundamental DP algorithm that answers: "What's the minimum number of single-character edits to transform string A into string B?"

**Visualization for "KITTEN" → "SITTING"**:
```
    ""  S  I  T  T  I  N  G
""   0  1  2  3  4  5  6  7
K    1  1  2  3  4  5  6  7
I    2  2  1  2  3  4  5  6
T    3  3  2  1  2  3  4  5
T    4  4  3  2  1  2  3  4
E    5  5  4  3  2  2  3  4
N    6  6  5  4  3  3  2  3
```
Answer: 3 edits (K→S, E→I, insert G)

**Part B: Spell Checker Application (3 pts)**
Build a real spell checker using a 10,000+ word English dictionary:

**The Challenge**: When someone types "recieve", your system needs to:
1. Recognize it's misspelled (not in dictionary)
2. Find candidate corrections efficiently
3. Rank suggestions by edit distance
4. Return the most likely intended words

**Real-World Optimizations**:
- **Early termination**: Stop calculating if distance exceeds threshold
- **Frequency weighting**: "the" is more likely than "teh" even with same edit distance
- **Keyboard awareness**: 'q' and 'w' are close, so "qork" → "work" is likely

**Part C: Name Matching Application (2 pts)**
Handle the chaos of real-world name variations:

**The Problem**: Customer databases are messy:
- Typos: "Jon Smith" vs "John Smith"
- Truncation: "Elizabeth" vs "Liz" vs "Beth"
- Cultural variations: "Mohammed" has 50+ common spellings
- Data entry errors: "Smith, John" vs "John Smith"

**Applications**:
- **Customer deduplication**: Merge duplicate customer records
- **Identity verification**: Match names across different systems
- **Genealogy**: Connect family tree records across databases
- **Security**: Detect potential identity fraud

**💡 Pro Tips for Success**:
- **Memoization**: Cache results for repeated subproblems
- **Space optimization**: You only need the previous row of the DP table
- **Early stopping**: If distance exceeds threshold, abandon calculation
- **Normalization**: Clean names before comparison (remove titles, fix capitalization)

**🎯 Performance Target**: Your implementation should handle 100-character strings efficiently and process spell-check queries in real-time!

**In this question, your task is to** implement the Levenshtein edit distance algorithm and apply it to two real-world scenarios: spell checking and name matching.

**Algorithm Overview:**
Edit distance measures the minimum number of single-character edits (insertions, deletions, or substitutions) needed to transform one string into another. It uses dynamic programming for efficient computation.

**Test your implementation:**
```bash
python autograder.py -q q12
```

**Part A: Core Algorithm (5 pts)**
```python
distance = edit_distance("kitten", "sitting")  # 3
distance = edit_distance("saturday", "sunday")  # 3
```

**Part B: Spell Checker Application (3 pts)**
Using a provided dictionary of 10,000+ common English words, implement a spell checker:

```python
# Load dictionary
dictionary = load_dictionary("src/data/english_words.txt")

# Find spelling suggestions
word = "recieve"  # misspelled
suggestions = spell_check(word, dictionary, max_suggestions=5)
# Returns: ["receive", "deceive", "relieve", "believe", "achieve"]

# With edit distance threshold
suggestions = spell_check("definately", dictionary, max_distance=2)
# Returns: ["definitely", "delineate"]
```

**Part C: Name Matching Application (2 pts)**
Handle variations in person names for record linkage:

```python
# Database of names with variations
names_db = ["John Smith", "Jane Doe", "Michael Johnson", "Sarah Williams"]

# Find closest matches
query = "Jon Smith"  # typo in first name
matches = name_matcher(query, names_db, threshold=2)
# Returns: [("John Smith", 1)]  # (name, edit_distance)

query = "Jane Do"  # truncated last name
matches = name_matcher(query, names_db, threshold=2)
# Returns: [("Jane Doe", 1)]
```

**Real-world Applications:**
- **Spell checking**: Autocorrect systems, search query suggestions
- **Name matching**: Customer record deduplication, identity verification
- **DNA sequence alignment**: Bioinformatics applications
- **Plagiarism detection**: Document similarity assessment

**Performance Considerations:**
Your implementation should handle strings up to 100 characters efficiently and process spell-check queries in real-time.

---

## Extra Credit (Optional)

These challenges are designed for students who want to explore more advanced text processing techniques. They're completely optional but offer valuable learning opportunities and extra points for those ready to dive deeper!

### Q7 (+5 pts): Complex Log File Parsing 

**🌟 Professional-Level Challenge**: Real production systems generate complex log files that require sophisticated parsing. This question simulates the complexity you'd encounter in industry log analysis, complete with IPv6 addresses, quoted fields, and nested data structures.

**Why This Matters**:
- **DevOps & Site Reliability**: Parse server logs to detect security threats, performance issues, and system failures
- **Data Engineering**: Extract structured data from unstructured log formats for analytics pipelines  
- **Security Analysis**: Identify attack patterns, suspicious IP addresses, and unauthorized access attempts
- **Performance Monitoring**: Track response times, error rates, and resource utilization across distributed systems

**The Challenge**: Parse complex server logs with multiple formats, escaped quotes, IPv6 addresses, and nested JSON payloads. Your regex must handle:
- Mixed IPv4/IPv6 addresses
- Quoted fields containing spaces and special characters
- Escaped quotes within quoted strings
- Variable field ordering
- Optional fields that may or may not be present

**Test your implementation:**
```bash
python autograder.py -q q7
```

### Q11 (+15 pts): Byte Pair Encoding (BPE) Implementation

**🚀 Cutting-Edge NLP**: Implement the tokenization algorithm that powers modern language models like GPT, BERT, and T5. BPE is the secret sauce behind how these models handle massive vocabularies efficiently!

**Revolutionary Impact**:
- **Modern Transformers**: Used by GPT-3/4, ChatGPT, BERT, and virtually every large language model
- **Multilingual NLP**: Handles any language without pre-defining vocabulary
- **Subword Intelligence**: Captures morphological patterns and handles out-of-vocabulary words
- **Compression**: Reduces vocabulary size while maintaining semantic meaning

**The Algorithm Magic**:
BPE iteratively merges the most frequent character pairs, building up from characters to subwords to words. This creates a vocabulary that balances between character-level flexibility and word-level efficiency.

**Why It's Challenging**:
- **Algorithmic Complexity**: Requires efficient frequency counting and priority queue management
- **Edge Case Handling**: Unicode characters, special tokens, and encoding boundaries
- **Performance**: Must handle large corpora efficiently
- **Implementation Details**: Merge rules, vocabulary management, and encoding/decoding logic

**Real-World Applications**:
- **Language Model Training**: Tokenize massive text corpora for transformer training
- **Machine Translation**: Handle vocabulary mismatches between source and target languages
- **Code Generation**: Tokenize programming code for AI coding assistants
- **Multilingual Systems**: Single model supporting 100+ languages

**Test your implementation:**
```bash
python autograder.py -q q11
```

**💡 Extra Credit Philosophy**: These questions represent the cutting edge of NLP preprocessing. Don't worry if they seem challenging - they're designed to stretch your understanding and give you a taste of advanced techniques you'll encounter in research and industry!

---

## Grading & Submission

### Assessment Breakdown

| Component | Points | Description |
|-----------|---------|-------------|
| **Part 1: Regular Expressions** | **30** | **Core pattern matching skills** |
| Q1: Email and URL Extraction | 5 | Extract emails and URLs from text |
| Q2: Phone Number Processing | 5 | Identify and normalize phone numbers |
| Q3: Social Media Processing | 5 | Extract hashtags, mentions, and emojis |
| Q4: Date and Time Extraction | 5 | Extract dates and times in multiple formats |
| Q5: Document Structure Extraction | 5 | Extract sections, citations, and code blocks |
| Q6: Address Extraction | 5 | Extract and parse physical addresses |
| **Part 2: Tokenization & Normalization** | **20** | **Essential NLP preprocessing** |
| Q8: Basic Tokenization | 5 | Whitespace, punctuation, sentence tokenization |
| Q9: Advanced Tokenization | 5 | Handle contractions, hyphenated words, URLs |
| Q10: Text Normalization | 5 | Lowercase, accent removal, character handling |
| Q12: Edit Distance Applications | 8 | Levenshtein distance with spell checking |
| **Extra Credit** | **+20** | **Advanced techniques (optional)** |
| Q7: Complex Log File Parsing | +5 | Advanced server log parsing challenge |
| Q11: BPE Implementation | +15 | Byte Pair Encoding algorithm |
| **Total Base Points** | **58** | |
| **Maximum with Extra Credit** | **78** | |

### Autograder Usage

Test your complete solution:
```bash
python autograder.py
```

Test specific questions:
```bash
python autograder.py -q q1
python autograder.py -q q2
# ... etc
```

### Practice Using Git

Throughout this homework, use git to document your progress:

**Good commit message examples:**
- "Implemented email extraction regex in Q1"
- "Fixed phone number normalization edge cases"
- "Added multilingual tokenization support"
- "Optimized edit distance algorithm"

### Final Submission

1. **Fork the Repository**: Create a fork of the course repository
2. **Create Your Submission Folder**: Add your work in `submissions/[your-name]/`
3. **Commit Your Changes**: Ensure all changes are committed with detailed messages
4. **Push Your Changes**: Push to your forked repository
5. **Create a Pull Request**: Include detailed description and answers to:
   - What challenges did you encounter?
   - Which regex patterns were most difficult to write?
   - How did you approach debugging your tokenization functions?
   - What did you learn about text preprocessing?

### Submission Requirements

Your submission folder should contain:
- All modified Python files (`regex_exercises.py`, `tokenization.py`, etc.)
- Any additional test files you created
- A `README.md` documenting your approach and any special considerations

**Due Date**: August 9, 2025 at 11:59 PM (Guyana time)

---

### Tips for Success

**🚀 Mindset Shift**: Think like a production engineer, not just a student. Every function you write could power a real application serving millions of users!

**📈 Development Strategy**:
1. **Start Early**: Regex can be deceptively tricky - give yourself time to experiment
2. **Test Incrementally**: Use the autograder frequently to catch issues early  
3. **Embrace Online Tools**: [regex101.com](https://regex101.com) and [regexpal.com](https://regexpal.com) are lifesavers
4. **Read the Data**: Examine sample files closely - they contain hints about edge cases
5. **Handle Gracefully**: Real-world data is messy - code defensively

**🎯 Regex Mastery Tips**:
- **Anchors**: `^` (start) and `$` (end) prevent partial matches
- **Quantifiers**: `*` (0+), `+` (1+), `?` (0-1), `{n,m}` (exactly n to m)
- **Character classes**: `\d` (digits), `\w` (word chars), `\s` (whitespace)
- **Grouping**: `()` for capture groups, `(?:)` for non-capturing groups
- **Lookahead/behind**: `(?=...)` and `(?<=...)` for context without consuming

**🐛 Debugging Strategies**:
- **Print intermediate results**: See what your regex actually captures
- **Test edge cases**: Empty strings, single characters, Unicode text
- **Use verbose mode**: `re.VERBOSE` lets you add comments to complex regex
- **Break complex patterns**: Split complicated regex into smaller, testable parts

**⚡ Performance Awareness**:
- **Avoid catastrophic backtracking**: Be careful with nested quantifiers like `(a*)*`
- **Use specific patterns**: `\d+` is faster than `.*` for numbers
- **Compile once**: Use `re.compile()` for patterns used repeatedly
- **Consider alternatives**: Sometimes string methods are faster than regex

**🌟 Beyond the Assignment**:
- **Explore variations**: Try your regex on different languages and formats
- **Build a toolkit**: Save useful patterns for future projects
- **Study real implementations**: Look at spaCy, NLTK, and other NLP libraries
- **Join communities**: r/regex and Stack Overflow have amazing discussions

Remember: The goal is to learn fundamental NLP preprocessing techniques that you'll use throughout the course. Focus on understanding the concepts, not just passing the tests!

**Good luck!** 🚀
