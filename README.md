# A feladatok mind Python kódban készültek
# 1.3 feladat

total_outcomes = 6 * 6

valid_outcomes = 0

for kocka1 in range(1, 7):

    for kocka2 in range(1, 7):
        if kocka1 + kocka2 >= 4:
            valid_outcomes += 1
            
probability = valid_outcomes / total_outcomes

print(f"A valószínűség, hogy az összeg legalább 4 lesz: {probability:.2f}")

# 1.4 feladat

def conditional(p, q):

    return not p or q

def xor(p, q):
  
    return p != q

def and_operator(p, q):
    
    return p and q

def evaluate_logical_statement(ace, king, operator):

    A = ace 
    K = king 
    
    part1 = conditional(A, K)
    
    part2 = conditional(not A, K)
    
    if operator == 'or':
        result = part1 or part2
    elif operator == 'xor':
        result = xor(part1, part2)
    elif operator == 'and':
        result = and_operator(part1, part2)
    
    return result

Tesztelés

print("Logikai modellezés - King-Ace Paradox:")

    for ace in [True, False]: 
    for king in [True, False]:
        print(f"\nÁsz: {ace}, Király: {king}")
        
        
        result_or = evaluate_logical_statement(ace, king, 'or')
        print(f"  Klasszikus 'vagy': {result_or}")
        
        result_xor = evaluate_logical_statement(ace, king, 'xor')
        print(f"  Kizáró 'vagy' (XOR): {result_xor}")
        
        result_and = evaluate_logical_statement(ace, king, 'and')
        print(f"  'És' (AND): {result_and}")

# 2.1 feladat

def lemma_problem_1(A, B, C):

    #Ha A igaz, és (B vagy C) igaz, akkor vagy (A és B), vagy (A és C) igaz.
    
    if A and (B or C):  # Ha A igaz, és B vagy C igaz
        if B:  # Ha B igaz
            return (A, B)  # (A és B) igaz
        elif C:  # Ha C igaz
            return (A, C)  # (A és C) igaz
    return None  # Ha egyik sem igaz

print(lemma_problem_1(True, True, False))  
print(lemma_problem_1(True, False, True))  
print(lemma_problem_1(False, True, True))

# 2.2 feladat

def lemma_problem_2(A, B, C):

    #Ha (B -> A) és (C -> A) igaz, akkor (B \/ C -> A) is igaz.

    # Feltételezzük, hogy (B -> A) és (C -> A) igaz
    if (not B or A) and (not C or A):  # (B -> A) és (C -> A)
        # Ha B vagy C igaz, akkor A-nak igaznak kell lennie
        if B or C:  # Ha B vagy C igaz
            return A  # A igaz lesz
    return None  # Ha nem igazak a feltételek

print(lemma_problem_2(True, True, False))  
print(lemma_problem_2(True, False, True))  
print(lemma_problem_2(False, False, False))  
print(lemma_problem_2(True, True, True))  

# 2.3. feladat

def lemma_problem_3(A, B):
     
    #Ha (A \/ ~A) igaz, és ((A -> B) -> A) igaz, akkor A igaz.
    
    if A or not A:  # Ez a kizárt harmadik lehetőség (A \/ ~A)
        if (A and B) or not A:  # Ha (A -> B) -> A, akkor A-nak igaznak kell lennie
            return A  # Visszatér A értékével
    
    return None  

print(lemma_problem_3(True, True))   
print(lemma_problem_3(False, False)) 
print(lemma_problem_3(True, False))  
print(lemma_problem_3(False, True))  

# 2.4 feladat

def lemma_problem_4(A, B, U):
     
    #Ha létezik egy x, amelyre (A(x) és B(x)) igaz, akkor létezik olyan x, amelyre A(x) igaz, és létezik olyan x, amelyre B(x) igaz.
    
    # Feltételezzük, hogy létezik egy x, amelyre A(x) és B(x) is igaz
    for x in U:
        if A(x) and B(x):  # Ha A(x) és B(x) igaz egy x-re
            # Akkor létezik olyan x, amelyre A(x) igaz, és létezik olyan x, amelyre B(x) igaz
            return (True, True)
    
    return (False, False)  

# 3.1 feladat

import math

def probability():
    total_cards = 52
    kings = 4
    non_kings = total_cards - kings
    
    total_outcomes = math.comb(total_cards, 2)
    
    favorable_outcomes = kings * non_kings
    
    probability = favorable_outcomes / total_outcomes
    return probability

A valószínűség kiszámolása

result = probability()
print(f"A valószínűség, hogy az egyik király, a másik nem király: {result:.4f}")

U = [1, 2, 3]
A = lambda x: x == 2  
B = lambda x: x == 2

result = lemma_problem_4(A, B, U)
print(result)

# 3.2 feladat

from itertools import product

values = [0, 1, 2, 3]

combinations = list(product(values, repeat=3))

valid_combinations = [comb for comb in combinations if sum(comb) == 7]
total_combinations = len(combinations)
p_W_equals_7 = len(valid_combinations) / total_combinations

p_X_equals = {0: 0, 1: 0, 2: 0, 3: 0}

for comb in valid_combinations:
    X, Y, Z = comb
    p_X_equals[X] += 1
    
conditional_probabilities = {}
for X in p_X_equals:
    conditional_probabilities[X] = p_X_equals[X] / len(valid_combinations)

print(f"P(W = 7) = {p_W_equals_7:.4f}")
print("Feltételes valószínűségek P(X = x | W = 7):")
for X in conditional_probabilities:
    print(f"P(X = {X} | W = 7) = {conditional_probabilities[X]:.4f}")


