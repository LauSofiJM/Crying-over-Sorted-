# Crying over sorted()
_There's a lot happening. It's surprising for me to realize how many thing I've been learning this whole month, so I'm a newbie in many things; but fortunately, I wanna learn so much._
***
### Better Comments
_This is the how I decided to use the extension.
- #Info related to the program (grey)
- #* Titles (green light)
- #? Advices or clarifications (blue)
- #todo Need to reforce (orange)
- #! Confused bout' something (red)
- #// Discarted (--)
- #- Success (yellow)
***
## 1. Basic operations
Basic operations was a code that I had to do in other opportunities but not using functions. The most challenging was to install correctly the extension "Better Comments" and to think about every possible error.

```python
#!I can not use better comments in this line, why?
#* Basic operations
# I need to create a function that allows people to do basic operations (+, -, *, /) using two numbers.

def basic_operations(num1, num2, operation):
    while True:
        if operation == "+":
            print(f"\nThe result is:  {num1 + num2}")
        elif operation == "-":
            print(f"\nThe result is:  {num1 - num2}")
        elif operation == "*":
            print(f"\nThe result is:  {num1 * num2}")
        elif operation == "/":
            if num2 != 0: #? I need to check if the second number is not zero to avoid a mathematical error.
                print(f"\nThe result is:  {num1 // num2}")
            else:
                num2 = float(input("\nYou can not divide by cero. Enter the second number: "))
                continue
        else: #? The program can not allow any other symbol.
            operation = input("\nEnter a valid operation symbol (+, -, *, /): ")
            continue
        break

num1 = float(input("Enter the first number: "))
num2 = float(input("\nEnter the second number: "))
operation = input("\nEnter the operation symbol (+, -, *, /): ")
result = basic_operations(num1, num2, operation) #todo I need to study more about functions and return values.

#- I tried to think about every possible error and I think I did it. I am happy with the result.
```
___
## 2. Palindrome or not?
At first, when I was thinking about the code, I considered using the **ord()** function to get the ASCII value of every character and then compare them from the bottom to the top of every word. However, after searching for information, I found that by using integer division (**//**) and comparing both halves of the words, I'd be able to achieve the same result.

```python

#* Palindrome or not?
#A palindrome is a sequence of characters which reads the same forward and backward.

def palindrome(word):
    word = word.lower() #? Convert the word to lowercase to avoid errors when comparing the letters.
    lst = []
    for letter in word:
        lst.append(letter) #? Convert the word to a list to compare the letters.
    for i in range(len(lst)//2): #? If is a palindrome, its first half will be the same as the second half.
        if lst[i] != lst[-i-1]: #! It compares the word from both ends. I hope it's not a kind of slicing.
            return False
    return True

word = input("Enter a word: ")
if palindrome(word):
    print(f"\n{word} is a palindrome.")
else:
    print(f"\n{word} is not a palindrome.")
    
#- I cheked many words and it did work. I liked to figured out how to compare the letters from both ends.
```
___
## 3. Prime numbers
I wanted the user to write as many integer numbers as they'd like, so I chose the letter "q" to finish that process. I also used the functions sort() and set() to organize the numbers in the list and avoid the repeated ones.

```python

#* Prime number
#A prime number is a natural number greater than 1 that is not a product of two smaller natural numbers

def is_prime(num): #! I found this way to check if a number is prime in a website. It is more efficient than the one I was using.
    if num <= 1:
        return False
    for i in range(2, int(num**0.5) + 1): #? I need to check if the number is divisible by any number from 2 to the square root of the number.
        if num % i == 0:
            return False
    return True

def get_numbers():
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ") #? I didn't want the user to write a specific number for the list to accept.
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    return numbers

def get_prime():
    numbers = get_numbers()

    prime_numbers = []
    for number in numbers:
        if is_prime(number):
            prime_numbers.append(number)

    prime_numbers.sort() #? I used the sort function to organize the numbers in ascending order.
    prime_numbers = set(prime_numbers) #? I used the set function to avoid repeated numbers.

    return prime_numbers

prime_numbers = get_prime()
print("Prime numbers:", prime_numbers)

#- It was a little tricky to figure out how to check if a number is prime and also, 
#- to find the better way to organize the code in my head previously.
```
___
## 4. Greater sum

In this code, I reused the **get_numbers()** function but when everything looked almost perfect, the code failed some tests, especially when testing negative values despite using **sorted()**. That was the moment when I was the most frustrated because nothing worked perfectly. That's why I named this repo _"Crying over sorted"_. I also had confusion about the instruction, but you can see that in the **red - #!** comments of the code. I gave up.
```python

#* Greater sum of two numbers
#I need to create a function that receives a list of numbers and returns greater sum of two consecutive numbers.

def get_numbers(): #? I reused the get_numbers function from Prime_Numbers.py.
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ")
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    numbers = list(set(numbers)) #? I used the set function to avoid repeated numbers.
    return numbers

def greater_sum(numbers): #!There is a thing that it's not working. I tried everything but I just don't know why the function 'sorted' doesen't organize well some numbers.
    if len(numbers) < 2:
        return None  # Not enough numbers to calculate sum
    max_sum = numbers[0] + numbers[1]
    for i in range(1, len(numbers)-1):
        current_sum = numbers[i] + numbers[i+1]
        max_sum = max(max_sum, current_sum)
    return max_sum

numbers = get_numbers()
result = greater_sum(sorted(numbers)) #! Sorted seems to not work properly with negative numbers.
print("The numbers are:", numbers)
print("The greater sum of two consecutive numbers is:", result)

#! I'm also confused about the code instruction... 'consecutive' in numbers is suposed to mean that they have to keep the 'natural' organization
#! so it didn't seemd to make sense when I compared my code to the test.
```
___
## 5. Anagrams
This time I wanted the words to be in the same line of code so I used the **split()** method to do it. I also cheked if there were numbers being introduced so the program would break and start again. This time **sorted()** worked properly but when I tried to use **set[]** I didn't go well so I found a solution that liked me so much and was to use **set()** to fill a set instead of a list, due to a set doesn't accept repeated values.
```python

#* Anagrams
# I need to create a function that returns the anagrams found in a list of words.

def get_words():
    while True:
        words = input("Write words separated by commas: ").split(',') #? Split the input by commas
        words = [word.strip() for word in words]
        if any(word.isdigit() for word in words): #? Check if there are numbers in the list
            print("Please enter words only. Numbers are not allowed.")
        else:
            break
    return words

def is_anagram(words):
    anagrams = set()
    for i in range(len(words)):
        for j in range(i+1, len(words)):
            if sorted(words[i]) == sorted(words[j]):
                anagrams.add(words[i])
                anagrams.add(words[j])
    return list(anagrams)

words = get_words()
print(f"\nThe original list is: {words}")
anagrams = is_anagram(words)
print(f"\nThe anagrams are: {anagrams}")
```
### That was it. Thanks for reading.
