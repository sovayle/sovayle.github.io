---
title: "Siber Siaga"
#categories: 
permalink: /ctfs/siber-siaga
---

> CTF siber-siaga Writeup

# Introduction

This is writeup for siber-siaga


## coding

```
import socket
import re
import statistics
import ast

def parse_question(question):
    # Try to parse the question as a Python expression
    try:
        result = ast.literal_eval(question)
        if isinstance(result, int):
            return [result]
    except (ValueError, SyntaxError):
        pass
    
    # If parsing as Python expression fails, extract numbers from the question using regular expressions
    numbers = [int(num) for num in re.findall(r'\d+', question)]
    return numbers

def handle_question(question):
    if "Max from" in question:
        numbers = parse_question(question)
        return max(numbers)
    elif "Median of" in question:
        median = statistics.median(parse_question(question))
        return median
    elif "Average of" in question:
        numbers = parse_question(question)
        return sum(numbers) / len(numbers)  # Return a float
    elif "mod" in question:
        a, b = parse_question(question)
        return a % b
    elif "Min from" in question:
        return min(parse_question(question))
    else:
        return None  # Unknown question format

def main():
    host = "math.sibersiaga2023.myctf.io"
    port = 8887

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        while True:
            data = s.recv(1024)
            if not data:
                break
            decoded_data = data.decode("latin-1")
            print(decoded_data)
            
            if b"Find: " in data:
                question_match = re.search(r"Find: (.+)", decoded_data)
                if question_match:
                    question = question_match.group(1)
                    answer = handle_question(question)
                    print("Question:", question)
                    print("Answer:", answer)
                    s.sendall(str(answer).encode() + b'\n')
                else:
                    print("Invalid question format")
            elif b"FLAG" in data:
                print(decoded_data)
                break

if __name__ == "__main__":
    main()

```
