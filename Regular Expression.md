```python
def replace_characters(data):
    # Replace space, comma, and dot with a colon
    replaced_data = data.replace(' ', ':').replace(',', ':').replace('.', ':')
    return replaced_data

sample_data = 'Python Exercises, PHP exercises.'
result = replace_characters(sample_data)
print(result)
```

    Python:Exercises::PHP:exercises:
    


```python
import re

def find_words_starting_with_a_or_e(text):
    # Use regular expression to find words starting with 'a' or 'e'
    pattern = r'\b[aeAE]\w*\b'
    matched_words = re.findall(pattern, text)
    return matched_words

sample_data = "Aeroplane and cars are good transportation. Eagles are birds."
result = find_words_starting_with_a_or_e(sample_data)
print(result)

```

    ['Aeroplane', 'and', 'are', 'Eagles', 'are']
    


```python
import re

def find_words_at_least_4_characters(text):
    # Compile the regular expression pattern to match words with at least 4 characters
    pattern = re.compile(r'\b\w{4,}\b')
    # Use findall() method to find all occurrences of the pattern in the text
    matched_words = pattern.findall(text)
    return matched_words

sample_text = "i wish i can travel to must of the countries in the world."
result = find_words_at_least_4_characters(sample_text)
print(result)
```

    ['wish', 'travel', 'must', 'countries', 'world']
    


```python
import re

def find_words_with_length(text):
    # Compile the regular expression pattern to match three, four, and five-character words
    pattern = re.compile(r'\b\w{3,5}\b')
    # Use findall() method to find all occurrences of the pattern in the text
    matched_words = pattern.findall(text)
    return matched_words

sample_data = "i wish i can travel to must of the countries in the world."
result = find_words_with_length(sample_data)
print(result)
```

    ['wish', 'can', 'must', 'the', 'the', 'world']
    


```python
import re

def remove_parentheses(strings_list):
    # Compile the regular expression pattern to match parentheses and their contents
    pattern = re.compile(r'\s?\([^)]*\)')
    # Use sub() method to remove the matched patterns from each string in the list
    cleaned_strings = [pattern.sub('', s) for s in strings_list]
    return cleaned_strings

sample_data = ["example (.com)", "hr@fliprobo (.com)", "github (.com)", "Hello (Data Science World)", "Data (Scientist)"]
result = remove_parentheses(sample_data)
print(result)
```

    ['example', 'hr@fliprobo', 'github', 'Hello', 'Data']
    


```python
import re

def remove_parentheses_from_text(text):
    # Compile the regular expression pattern to match parentheses and their contents
    pattern = re.compile(r'\s?\([^)]*\)')
    # Use sub() method to remove the matched patterns from the text
    cleaned_text = pattern.sub('', text)
    return cleaned_text

sample_text = '["example (.com)", "hr@fliprobo (.com)", "github (.com)", "Hello (Data Science World)", "Data (Scientist)"]'

# Remove the parenthesis from the sample text
cleaned_text = remove_parentheses_from_text(sample_text)

# Split the cleaned_text by commas to get individual elements
cleaned_list = cleaned_text.split(',')

print(cleaned_list)
```

    ['["example"', ' "hr@fliprobo"', ' "github"', ' "Hello"', ' "Data"]']
    


```python
import re

def split_into_uppercase(text):
    # Use re.findall() to find all occurrences of uppercase letters
    uppercase_words = re.findall(r'[A-Z][a-z]*', text)
    return uppercase_words

sample_text = "ImportanceOfRegularExpressionsInPython"
result = split_into_uppercase(sample_text)
print(result)
```

    ['Importance', 'Of', 'Regular', 'Expressions', 'In', 'Python']
    


```python
import re

def insert_spaces_between_numbers(text):
    # Use re.sub() to insert space before words starting with a number
    modified_text = re.sub(r'(?<=\D)(?=\d)', ' ', text)
    return modified_text

sample_text = "RegularExpression1IsAn2ImportantTopic3InPython"
result = insert_spaces_between_numbers(sample_text)
print(result)

```

    RegularExpression 1IsAn 2ImportantTopic 3InPython
    


```python
import re

def insert_spaces_between_capitals_and_numbers(text):
    # Use re.sub() to insert space before words starting with a capital letter or a number
    modified_text = re.sub(r'(?<=[A-Z0-9])(?=[A-Z])|(?<=\D)(?=\d)', ' ', text)
    return modified_text

sample_text = "RegularExpression1IsAn2ImportantTopic3InPython"
result = insert_spaces_between_capitals_and_numbers(sample_text)
print(result)

```

    RegularExpression 1 IsAn 2 ImportantTopic 3 InPython
    


```python
import re

def extract_emails_from_text(text):
    # Use re.findall() to find all occurrences of email addresses in the text
    email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b'
    extracted_emails = re.findall(email_pattern, text)

    return extracted_emails

sample_text = """
Hello my name is Data Science and my email address is xyz@domain.com and alternate email address is xyz.abc@sdomain.domain.com.
Please contact us at hr@fliprobo.com for further information.
"""

# Extract email addresses from the sample text
extracted_emails = extract_emails_from_text(sample_text)

# Print the expected output
for email in extracted_emails:
    print(email)



```

    xyz@domain.com
    xyz.abc@sdomain.domain.com
    hr@fliprobo.com
    


```python
import re

def is_valid_string(input_string):
    # Regular expression pattern to match upper and lowercase letters, numbers, and underscores
    pattern = r'^[A-Za-z0-9_]+$'
    # Use re.fullmatch() to check if the entire string matches the pattern
    match = re.fullmatch(pattern, input_string)
    return match is not None

# Test the function
test_strings = ["Hi_World443", "345_cat", "Lowercase*", "UPPER_CASE"]
for string in test_strings:
    result = is_valid_string(string)
    print(f'{string}: {result}')

```

    Hi_World443: True
    345_cat: True
    Lowercase*: False
    UPPER_CASE: True
    


```python
import re

def starts_with_number(input_string, number):
    # Convert the number to a string and create a regular expression pattern
    number_str = str(number)
    pattern = re.compile(r'^' + number_str)

    # Use re.match() to check if the input string matches the pattern at the beginning
    match = pattern.match(input_string)
    return match is not None

# Test the function
test_string = "12345abcdef"
specific_number = 123
result = starts_with_number(test_string, specific_number)
print(result)

```

    True
    


```python
def remove_leading_zeros(ip_address):
    # Split the IP address into its components
    components = ip_address.split('.')
    
    # Remove leading zeros from each component
    components = [str(int(component)) for component in components]
    
    # Reassemble the IP address
    cleaned_ip = '.'.join(components)
    
    return cleaned_ip

# Test the function
ip_address_with_zeros = "192.168.001.001"
cleaned_ip_address = remove_leading_zeros(ip_address_with_zeros)
print(cleaned_ip_address)

```

    192.168.1.1
    


```python
import re

def extract_date_from_text(text):
    # Regular expression pattern to match the date string format
    pattern = r'\b(?:January|February|March|April|May|June|July|August|September|October|November|December)\s+\d{1,2}(?:st|nd|rd|th)?\s+\d{4}\b'
    
    # Use re.search() to find the date string in the text
    match = re.search(pattern, text)

    # If a match is found, return the matched date string, otherwise return None
    return match.group() if match else None

# Test the function with the sample text
sample_text = 'On August 15th 1947 that India was declared independent from British colonialism, and the reins of control were handed over to the leaders of the Country.'
result = extract_date_from_text(sample_text)
print(result)

```

    August 15th 1947
    


```python
def search_literals(text, searched_words):
    known_words = [word for word in searched_words if word in text]
    return known_words

sample_text = 'The quick brown fox jumps over the lazy dog.'
searched_words = ['fox', 'dog', 'horse']

known_words = search_literals(sample_text, searched_words)
print(known_words)

```

    ['fox', 'dog']
    


```python
import re

def search_literals_with_location(text, searched_word):
    # Use re.finditer() to find all occurrences of the searched word in the text
    pattern = re.compile(re.escape(searched_word))
    matches = pattern.finditer(text)

    # Collect the found word and its start and end positions
    found_words_with_location = [(match.group(), match.start(), match.end()) for match in matches]
    return found_words_with_location

sample_text = 'The quick brown fox jumps over the lazy dog.'
searched_word = 'fox'

found_words_with_location = search_literals_with_location(sample_text, searched_word)
print(found_words_with_location)

```

    [('fox', 16, 19)]
    


```python
import re

def find_substrings(text, pattern):
    # Use re.finditer() to find all occurrences of the pattern in the text
    matches = re.finditer(pattern, text)

    # Collect the start and end positions of each occurrence
    substrings_with_location = [(match.start(), match.end()) for match in matches]
    return substrings_with_location

sample_text = 'Python exercises, PHP exercises, C# exercises'
pattern = 'exercises'

substrings_with_location = find_substrings(sample_text, pattern)
print(substrings_with_location)

```

    [(7, 16), (22, 31), (36, 45)]
    


```python
import re

def find_occurrences_with_positions(text, pattern):
    # Use re.finditer() to find all occurrences of the pattern in the text
    matches = re.finditer(pattern, text)

    # Collect the occurrences and their start and end positions
    occurrences_with_positions = [(match.group(), match.start(), match.end()) for match in matches]
    return occurrences_with_positions

sample_text = 'Python exercises, PHP exercises, C# exercises, Python exercises'
pattern = 'exercises'

occurrences_with_positions = find_occurrences_with_positions(sample_text, pattern)
print(occurrences_with_positions)

```

    [('exercises', 7, 16), ('exercises', 22, 31), ('exercises', 36, 45), ('exercises', 54, 63)]
    


```python
from datetime import datetime

def convert_date_format(date_str):
    # Parse the input date string into a datetime object
    date_obj = datetime.strptime(date_str, '%Y-%m-%d')
    
    # Convert the datetime object to the desired format
    formatted_date = date_obj.strftime('%d-%m-%Y')
    
    return formatted_date

# Test the function
input_date = '2025-10-25'
output_date = convert_date_format(input_date)
print(output_date)

```

    25-10-2025
    


```python
import re

def find_decimal_numbers_with_precision(text):
    # Regular expression pattern to match decimal numbers with a precision of 1 or 2
    pattern = re.compile(r'\b\d+\.\d{1,2}\b')
    
    # Use re.findall() to find all occurrences of the pattern in the text
    decimal_numbers = pattern.findall(text)
    return decimal_numbers

# Test the function
sample_text = "The price is $13.5, the quantity is 8.0, and the total is $61.49."
decimal_numbers = find_decimal_numbers_with_precision(sample_text)
print(decimal_numbers)

```

    ['13.5', '8.0', '61.49']
    


```python
def separate_numbers_with_positions(text):
    numbers_with_positions = []
    for index, char in enumerate(text):
        if char.isdigit():
            numbers_with_positions.append((char, index))

    return numbers_with_positions

# Test the function
sample_text = "The price is $13.5, the quantity is 8, and the total is $61.49."
numbers_with_positions = separate_numbers_with_positions(sample_text)
print(numbers_with_positions)

```

    [('1', 14), ('3', 15), ('5', 17), ('8', 36), ('6', 57), ('1', 58), ('4', 60), ('9', 61)]
    


```python
import re

def extract_maximum_numeric_value(text):
    # Regular expression pattern to find all numeric values in the text
    pattern = r'\b\d+\b'
    
    # Use re.findall() to find all occurrences of the pattern in the text
    numeric_values = [int(match) for match in re.findall(pattern, text)]
    
    # Find the maximum value in the numeric_values list
    max_value = max(numeric_values)

    return max_value

# Test the function
sample_text = 'My marks in each semester are: 947, 896, 926, 524, 734, 950, 642'
maximum_value = extract_maximum_numeric_value(sample_text)
print(maximum_value)  

```

    950
    


```python
import re

def insert_spaces_between_capital_words(text):
    # Regular expression pattern to find words starting with capital letters
    pattern = r'(?<!^)(?=[A-Z])'
    
    # Use re.sub() to insert spaces between the words
    formatted_text = re.sub(pattern, ' ', text)
    
    return formatted_text

# Test the function
sample_text = "RegularExpressionIsAnImportantTopicInPython"
formatted_text = insert_spaces_between_capital_words(sample_text)
print(formatted_text) 
```

    Regular Expression Is An Important Topic In Python
    


```python
import re

def find_upper_lower_sequences(text):
    # Regular expression pattern to find sequences of one upper case letter followed by lower case letters
    pattern = r'[A-Z][a-z]+'
    
    # Use re.findall() to find all occurrences of the pattern in the text
    sequences = re.findall(pattern, text)
    return sequences

# Test the function
sample_text = "RegularExpressionIsAnImportantTopicInPython"
sequences = find_upper_lower_sequences(sample_text)
print(sequences)  
```

    ['Regular', 'Expression', 'Is', 'An', 'Important', 'Topic', 'In', 'Python']
    


```python
import re

def remove_continuous_duplicates(text):
    # Regular expression pattern to match continuous duplicate words
    pattern = r'\b(\w+)(\s+\1)+\b'
    
    # Use re.sub() to remove the continuous duplicate words
    formatted_text = re.sub(pattern, r'\1', text)
    
    return formatted_text

# Test the function
sample_text = "Hello hello world world"
formatted_text = remove_continuous_duplicates(sample_text)
print(formatted_text)  
```

    Hello hello world
    


```python
import re

def ends_with_alphanumeric(text):
    # Regular expression pattern to match a string ending with an alphanumeric character
    pattern = r'\w$'
    
    # Use re.search() to find a match at the end of the string
    match = re.search(pattern, text)
    
    # If a match is found, the string ends with an alphanumeric character
    return bool(match)

# Test the function
sample_text1 = "Hi123"
sample_text2 = "Regular_Expression!"
print(ends_with_alphanumeric(sample_text1))  
print(ends_with_alphanumeric(sample_text2))  

```

    True
    False
    


```python
import re

def extract_hashtags(text):
    # Regular expression pattern to match hashtags
    pattern = r'#\w+'
    
    # Use re.findall() to find all occurrences of the pattern in the text
    hashtags = re.findall(pattern, text)
    return hashtags

# Test the function
sample_text = """RT @kapil_kausik: #Doltiwal I mean #xyzabc is "hurt" by #Demonetization as the same has rendered USELESS <ed><U+00A0><U+00BD><ed><U+00B1><U+0089> "acquired funds" No wo"""
hashtags = extract_hashtags(sample_text)
print(hashtags) 
```

    ['#Doltiwal', '#xyzabc', '#Demonetization']
    


```python
import re

def remove_U_symbols(text):
    # Regular expression pattern to match <U+..> like symbols
    pattern = r'<U\+[A-Za-z0-9]+>'
    
    # Use re.sub() to remove the symbols
    formatted_text = re.sub(pattern, '', text)
    
    return formatted_text

# Test the function
sample_text = "@Jags123456 Bharat band on 28??<ed><U+00A0><U+00BD><ed><U+00B8><U+0082>Those who  are protesting #demonetization  are all different party leaders"
formatted_text = remove_U_symbols(sample_text)
print(formatted_text)

```

    @Jags123456 Bharat band on 28??<ed><ed>Those who  are protesting #demonetization  are all different party leaders
    


```python
import re

def extract_dates(text):
    # Regular expression pattern to match dates in the format dd-mm-yyyy
    pattern = r'\b\d{2}-\d{2}-\d{4}\b'
    
    # Use re.findall() to find all occurrences of the pattern in the text
    dates = re.findall(pattern, text)
    return dates

# Sample Text
sample_text = "Ron was born on 12-09-1992 and he was admitted to school 15-12-1999."

# Extract dates from the sample text
dates = extract_dates(sample_text)
print(dates)

```

    ['12-09-1992', '15-12-1999']
    


```python
import re

def remove_words_between_length(text):
    # Regular expression pattern to match words of length between 2 and 4
    pattern = r'\b\w{2,4}\b'
    
    # Compile the regular expression pattern
    regex = re.compile(pattern)
    
    # Use re.sub() to remove all occurrences of the pattern in the text
    formatted_text = regex.sub('', text)
    
    return formatted_text

# Sample Text
sample_text = "The following example creates an ArrayList with a capacity of 50 elements. 4 elements are then added to the ArrayList and the ArrayList is trimmed accordingly."

# Remove words of length between 2 and 4 from the sample text
formatted_text = remove_words_between_length(sample_text)
print(formatted_text)

```

     following example creates  ArrayList  a capacity   elements. 4 elements   added   ArrayList   ArrayList  trimmed accordingly.
    


```python

```
