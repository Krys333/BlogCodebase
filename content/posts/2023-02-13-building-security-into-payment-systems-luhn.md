---
title: "E-commerce payment security - The Luhn algorithm."
date: 2024-02-13
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Security", "E-commerce", "Payments", "Algorithms", "February 2023"]
description: "Discover how card validation works and how Luhn algorithm is our first line of defence."
thumbnail: "images/github-actions.jpg"
image: '/images/github-actions-hero.jpg' 
draft: true
---

## What is Luhn algorithm and why should you care? 

Luhn algorithm, also known as 10 check-sum, is a very popular method of validating numerical IDs. Think debit card numbers, government social security numbers, or even diner loyalty cards. Luhn algorithm provides a fast and convenient method to verify whether the number entered by your user is likely to be authentic.

Is it a security measure? Well... no, not really. You should not rely on this method to protect you from the numerous fraud scams out there. Why use it then? In combination with other security measures, this algorithm is a great first-line of defence. Furthermore, it is a great mechanism for early filtering of mistyped information.

## How does the Luhn algorithm work?

We will be applying the algorithm to the following 16 digit number in order to test if it is correct - 3379 5135 6110 8795

### Part 1 Calculate the weighted sum of the card number.

We will be using a weighted sum pattern of 2,1,2,1,2,1 and so on. What does this mean? Depending on the position of the number on the card, we will multiply the digit by either a 1, or a 2. For our number the pattern will look as follows.
```
 _______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|5|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|1|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
```
The top row is our card number, where bottom is the weighted sum pattern. The job now is to multiply the top digit by its lower counterpart. As an example:

```
 _______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|5|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|1|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
|6|3| | | | | | | | | | | | | | |
```
2x3=6. Then we have 1x3=3. Easy, right? Yes, but there is a small problem. The next digit is 2x7=14. As the sum is a two-digit number we need to add its individual components together. In case of 14 we do 1+4 and get 5. We do this to any sum of 10 or above.
```
 _______________________________
|3|3|7|9|5|1|3|5|6|1|1|0|8|7|9|5|
|2|1|2|1|2|1|2|1|2|1|2|1|2|1|2|1|
 ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
|6|3|5|9|1|1|6|5|3|1|2|0|7|7|9|5|
```
### Part 2 - Sum up the last row and test the divisibility.

Finally you need to sum up the last row. 
6+3+5+9+1+1+6+5+3+1+2+0+7+7+9+5 = 70

If the result is a digit with a 0 at the end, it passes the Luhn 10 check-sum validation.

## A coded example


```python
def luhn_checksum(card_number):
    def digits_of(n):
        return [int(d) for d in str(n)] #grbs the individual digits from the entire input
    digits = digits_of(card_number)
    odd_digits = digits[-1::-2]         # Split the digits into odd numbers
    even_digits = digits[-2::-2]        # Split the digits into even numbers
    checksum = 0
    checksum += sum(odd_digits)         # No need to process odd digits. We can just go ahead, sum them up and add them to our checksum total. 
    for d in even_digits:
        checksum += sum(digits_of(d*2)) # We multiply the even numbers by 2. As we are returning individual digits, we do not have to worry about numbers of 10 or more. 
    return checksum % 10                # Divide the number by 10. If it divides without a leftover float, it passess the check!


def is_luhn_valid(card_number):
    return luhn_checksum(card_number) == 0
```

I recommend using the above code in conjunction with a basic user entry character count. This will allow you to cover for the most common entry-errors, and other fishy data entries.


