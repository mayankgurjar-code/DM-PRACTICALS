# ============================================================
# Discrete Mathematical Structures - All 7 Practicals
# B.Sc. (H) Computer Science - Semester II
# ============================================================


# ============================================================
# PRACTICAL 1
# Create a class SET. Create member functions to perform the
# following SET operations:
# a. is_member b. powerset c. subset d. union & intersection
# e. complement f. set difference & symmetric difference
# g. cartesian product
# Write a menu driven program to perform the above functions.
# ============================================================

class SET:
    def __init__(self, elements):
        self.elements = list(set(elements))

    def is_member(self, x):
        return x in self.elements

    def powerset(self):
        result = [[]]
        for e in self.elements:
            result += [s + [e] for s in result]
        return result

    def subset(self, other):
        return all(e in other.elements for e in self.elements)

    def union(self, other):
        return SET(self.elements + other.elements)

    def intersection(self, other):
        return SET([e for e in self.elements if e in other.elements])

    def complement(self, universal):
        return SET([e for e in universal.elements if e not in self.elements])

    def set_difference(self, other):
        return SET([e for e in self.elements if e not in other.elements])

    def symmetric_difference(self, other):
        return SET([e for e in self.elements if e not in other.elements] +
                   [e for e in other.elements if e not in self.elements])

    def cartesian_product(self, other):
        return [(a, b) for a in self.elements for b in other.elements]

    def __str__(self):
        return str(sorted(self.elements))


while True:
    print("\n--- SET Operations Menu ---")
    print("1. Is Member\n2. Power Set\n3. Subset Check\n4. Union\n5. Intersection")
    print("6. Complement\n7. Set Difference\n8. Symmetric Difference\n9. Cartesian Product\n0. Exit")
    choice = input("Enter choice: ")

    if choice == '0':
        break
    else:
        a = SET(list(map(int, input("Enter elements of Set A (space-separated): ").split())))

        if choice == '1':
            x = int(input("Enter element to check: "))
            print(f"Is member: {a.is_member(x)}")
        elif choice == '2':
            print(f"Power Set: {a.powerset()}")
        elif choice == '3':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"A is subset of B: {a.subset(b)}")
        elif choice == '4':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"Union: {a.union(b)}")
        elif choice == '5':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"Intersection: {a.intersection(b)}")
        elif choice == '6':
            u = SET(list(map(int, input("Enter Universal Set elements: ").split())))
            print(f"Complement: {a.complement(u)}")
        elif choice == '7':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"Set Difference (A-B): {a.set_difference(b)}")
        elif choice == '8':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"Symmetric Difference: {a.symmetric_difference(b)}")
        elif choice == '9':
            b = SET(list(map(int, input("Enter elements of Set B: ").split())))
            print(f"Cartesian Product: {a.cartesian_product(b)}")


# ============================================================
# PRACTICAL 2
# Create a class RELATION, use Matrix notation to represent a
# relation. Include member functions to check if the relation
# is Reflexive, Symmetric, Anti-symmetric, Transitive.
# Check whether the given relation is: Equivalence or
# Partial Order relation or None.
# ============================================================

class RELATION:
    def __init__(self, matrix):
        self.m = matrix
        self.n = len(matrix)

    def is_reflexive(self):
        return all(self.m[i][i] == 1 for i in range(self.n))

    def is_symmetric(self):
        return all(self.m[i][j] == self.m[j][i]
                   for i in range(self.n) for j in range(self.n))

    def is_antisymmetric(self):
        return all(not (self.m[i][j] == 1 and self.m[j][i] == 1)
                   for i in range(self.n) for j in range(self.n) if i != j)

    def is_transitive(self):
        for i in range(self.n):
            for j in range(self.n):
                if self.m[i][j]:
                    for k in range(self.n):
                        if self.m[j][k] and not self.m[i][k]:
                            return False
        return True

    def classify(self):
        r = self.is_reflexive()
        s = self.is_symmetric()
        a = self.is_antisymmetric()
        t = self.is_transitive()
        print(f"Reflexive: {r}, Symmetric: {s}, Anti-symmetric: {a}, Transitive: {t}")
        if r and s and t:
            print("The relation is an Equivalence Relation.")
        elif r and a and t:
            print("The relation is a Partial Order Relation.")
        else:
            print("The relation is None of the above.")


n = int(input("\nEnter number of elements: "))
print("Enter the relation matrix row by row (space-separated 0s and 1s):")
matrix = [list(map(int, input().split())) for _ in range(n)]
rel = RELATION(matrix)
rel.classify()


# ============================================================
# PRACTICAL 3
# Write a Program that generates all the permutations of a
# given set of digits, with or without repetition.
# ============================================================

from itertools import permutations, product

digits = list(map(int, input("\nEnter digits (space-separated): ").split()))
r = int(input("Enter length of permutation: "))
choice = input("Allow repetition? (yes/no): ").strip().lower()

if choice == 'yes':
    result = list(product(digits, repeat=r))
else:
    result = list(permutations(digits, r))

print(f"Total permutations: {len(result)}")
for p in result:
    print(p)


# ============================================================
# PRACTICAL 4
# For any number n, write a program to list all the solutions
# of the equation x1 + x2 + ... + xn = C, where C is a
# constant (C<=10) and x1, x2,...,xn are nonnegative integers,
# using brute force strategy.
# ============================================================

from itertools import product as iproduct

n = int(input("\nEnter number of variables (n): "))
C = int(input("Enter constant C (<=10): "))

count = 0
for combo in iproduct(range(C + 1), repeat=n):
    if sum(combo) == C:
        print(combo)
        count += 1

print(f"Total solutions: {count}")


# ============================================================
# PRACTICAL 5
# Write a Program to evaluate a polynomial function.
# (For example store f(x) = 4n2 + 2n + 9 in an array and
# for a given value of n, say n = 5, compute the value of f(n))
# ============================================================

degree = int(input("\nEnter degree of polynomial: "))
print("Enter coefficients from constant term to highest degree (e.g. for 4n^2+2n+9: enter 9 2 4):")
coeffs = list(map(float, input().split()))
n = float(input("Enter value of n: "))

result = sum(c * (n ** i) for i, c in enumerate(coeffs))
print(f"f({int(n)}) = {result}")


# ============================================================
# PRACTICAL 6
# Write a Program to check if a given graph is a complete
# graph. Represent the graph using Adjacency Matrix.
# ============================================================

def is_complete_graph(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(n):
            if i != j and matrix[i][j] != 1:
                return False
            if i == j and matrix[i][j] != 0:
                return False
    return True

n = int(input("\nEnter number of vertices: "))
print("Enter adjacency matrix row by row:")
matrix = [list(map(int, input().split())) for _ in range(n)]

if is_complete_graph(matrix):
    print("The graph is a Complete Graph.")
else:
    print("The graph is NOT a Complete Graph.")


# ============================================================
# PRACTICAL 7
# Write a Program to accept a directed graph G and compute
# the in-degree and out-degree of each vertex.
# ============================================================

n = int(input("\nEnter number of vertices: "))
print("Enter adjacency matrix of directed graph row by row:")
matrix = [list(map(int, input().split())) for _ in range(n)]

print("\nVertex | In-degree | Out-degree")
print("-" * 35)
for i in range(n):
    out_degree = sum(matrix[i])
    in_degree = sum(matrix[j][i] for j in range(n))
    print(f"  {i+1}    |     {in_degree}     |     {out_degree}")
