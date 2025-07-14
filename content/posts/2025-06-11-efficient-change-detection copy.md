---
title: "How to Detect Changes in Big Datasets Without Burning Your CPU"
date: 2025-06-11
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Change Data Capture", "2025", "Data Lake", "highlight"]
description: "How to quickly and efficiently detect changes between large files."
thumbnail: "images/CDC.png"
image: "/images/CDC.png"
---

Imagine you're working with big data files—maybe millions of rows in CSVs, logs, or database exports. You want to know: Has anything changed since the last time I saw this file?
Seems simple, right? But if you're not careful, checking for changes can be a slow and painful process. Let's talk about why, and how to do it better.

## The Problem: "Did This Data Change?"
Checking whether a dataset has changed is a very common task in our field.
Example:

- A new data file comes in every day.
- You want to know if it’s different from yesterday’s file.
- You don’t want to process it unless it’s actually new or updated.

If you're dealing with small files, you might just:

- Open both files (incoming and old).
- Compare each row one-by-one.

But here’s the issue... **It is a Bad Idea at Scale.**

Let’s say your file has 10 million rows. Comparing row by row means:
- Reading two huge files into memory.
- Looping through every single row.
- Possibly comparing each field in each row.

This is:

- Slow – even on a powerful machine.
- Expensive – eats up CPU, memory, and time.
- Inefficient – especially if 99% of the time the file hasn’t even changed!

Surely, there must be a better way.
## Other (Imperfect) Solutions
Relying on metadata is an interesting trick:

- Comparing file sizes – If the sizes are different, maybe something changed.
    - Problem: A file can change slightly (like a timestamp) without changing size.

- Checking last modified timestamp – Fast, but unreliable.
    - Problem: Some systems reset timestamps even if the file didn’t change.
    - For example, identical file is re-uploaded into the data lake. Contents are the same but metadata is reset. 

## The Efficient Solution: Hash the Whole File
Here’s a smarter way: fingerprint the file using a hash function.

Think of a hash like a digital fingerprint. If the file changes—even by one character—its hash will change too.

How It Works 🔑

- When you get a new file, generate a hash of its contents. (Example: using SHA-256 or MD5)
- Compare that hash to the one you saved from the previous file.
- If the hash is the same, the data hasn’t changed. Done!
- If the hash is different, then you can dive deeper to see what changed.


## Final Thoughts

This is not a new problem. And the solution is not at all complicated. But I absolutely love it as I remember how mind-blown I have been by the simplicity of it the first time I heard it. Most systems now solve these issues for us. But if you ever find yourself having to solve for data change detection, remember this article. May it save you time, processing power, and money.