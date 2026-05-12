# DM-PRACTICALS

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
    elif choice in ['1', '2', '3', '4', '5', '6', '7', '8', '9']:
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
