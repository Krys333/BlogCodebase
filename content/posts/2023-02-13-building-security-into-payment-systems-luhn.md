---
title: "E-commerce payment security - The Luhn algorithm."
date: 2023-02-02
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Security", "E-commerce", "Payments", "Algorithms", "February 2023"]
description: "Discover how card validation works and how Luhn algorithm is our first line of defence against input errors."
thumbnail: "images/luhn-algorithm-thumbnail.jpg"
image: '/images/blackboard.jpg' 
---

## What is Luhn algorithm and why should you care? 

Luhn algorithm is a very popular method of validating numerical IDs. Think debit card numbers, government social security numbers, or even diner loyalty cards. Luhn algorithm provides a fast and convenient method to verify whether the number entered by your user is likely to be authentic.

Is it a security measure? Well... no, not really. You should not rely on this method to protect you from the numerous fraud scams out there. Why use it then? In combination with other security measures, this algorithm is a great first-line of defence. Furthermore, it is a great mechanism for early filtering of mistyped information.

## How does the Luhn algorithm work?

We will be applying the algorithm to the following 16 digit number in order to test if it is correct - 3379 5135 6110 8795.
It is important to know there are two types of checks. One is the "10-checksum", the second is the "last check-digit".
We are applying the last check-digit. As such before we begin, drop the last digit (5). This will be our "check number". It will be important later!

### Part 1 Calculate the weighted sum of the card number.

We will be using a weighted sum pattern of 2,1,2,1,2,1 and so on. What does this mean? Depending on the position of the number on the card, we will multiply the digit by either a 1, or a 2. For our number the pattern will look as follows. Exclude the number we have dropped. 
```
 ______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
```
The top row is our card number, where bottom is the weighted sum pattern. The job now is to multiply the top digit by its lower counterpart. As an example:

```
 ______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
|6|3| | | | | | | | | | | | | |
```
2x3=6. Then we have 1x3=3. Easy, right? Yes, but there is a small problem. The next digit is 2x7=14. As the sum is a two-digit number we need to add its individual components together. In case of 14 we do 1+4 and get 5. We do this to any sum of 10 or above.
```
 ______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
|6|3|5|9|1|1|6|5|3|1|2|0|7|7|9|

```
### Part 2 - Sum up the last row and apply the checksum calculation to the result.

If we sum up the last row we get a sum of 65.
```
6+3+5+9+1+1+6+5+3+1+2+0+7+7+9 = 65
```
Using this number we now plot the sum into the following equation: 10 - (s mod 10).
"s mod 10" refers to the modulo number we get when we divide our sum by 10.
```
10 - (65 mod 10)
10 - (5)
5
```
Remember our checksum? If our calculations match the checksum it means the number is valid!
3379 5135 6110 8795

## A coded example


```python
def split_the_check_digit(original_number):
    first_digits = original_number[:-1]
    original_check_digit = int(original_number) % 10
    return first_digits, original_check_digit

def calculate_luhn_check_digit(number):
    digits = [int(d) for d in str(number)]
    print("digits = ", digits)

    odd_digits = digits[-2::-2]
    even_digits = digits[-1::-2]
    total = sum(odd_digits)
    comp_total = 0
    for digit in even_digits:
        component = sum(divmod(digit * 2, 10))
        total += component
    return (10 - (total % 10))

def compare_actual_against_valid(original_check_digit, correct_check_digit):
    if original_check_digit == correct_check_digit:
        return "valid number"
    else:
        return "invalid number"

original_number = "3379513561108795"
first_digits, original_check_digit = split_the_check_digit(original_number)
correct_check_digit = calculate_luhn_check_digit(first_digits)
result = compare_actual_against_valid(original_check_digit, correct_check_digit)
```
I recommend using the above code in conjunction with a basic user entry character count. A common usecase are most debit cards which use 16 digits. Using the check you can cover for the most common entry-errors, and other fishy data entries.