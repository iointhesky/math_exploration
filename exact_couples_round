# question: find the number of ways for exactly k couples, out of n, to sit in a round table with m singles

from itertools import permutations

# function declaration
def input_variables():
    cpl = input('How many couples are present? Numerical input only.')
    if int_checker(cpl) is False: return None
    sgl = input('How many singles are present? Numerical input only.')
    if int_checker(sgl) is False: return None
    cpl = int_checker(cpl)
    sgl = int_checker(sgl)
    if sanity_checker(cpl, sgl) is False: return None
    tgt = input('Exactly how many couples do you want them to seat together? Numerical input only.')
    if int_checker(tgt) is False: return None
    tgt = int_checker(tgt)
    return [cpl, sgl, tgt] 
    
def int_checker(number):
    try:
        int(number)
    except:
        print('error: not an integer')
        return False
    else:
        if int(number) < 0:
            print('error: negative number')
            return False
        else:
            return int(number)

def sanity_checker(a,b):
    if not (a or b):
        print('error: no people to sit')
        return False
    else: 
        return True
        
# counters
total_possible_arrangements = 0
arrangements_k_couples = 0
        
# fix input
input_list = None
while not input_list:
    input_list = input_variables()
total_couples = input_list[0]
couples_together = input_list[2]
singles = input_list[1]
people_present = 2 * total_couples + singles

# generate linear permutations
linear_list = list(permutations(range(people_present)))

# fix circular permutations by removing rotational symmetry. set() is used to prevent duplicates
circle_list = set()
for permutation in linear_list:
    # let first person be first number in range, i.e. 0
    first_person = permutation.index(0)
    # adjust sequence such that first number is always 0
    table_hold = tuple(permutation[first_person:] + permutation[:first_person])
    # add sequence to circular permutation list
    circle_list.add(table_hold)

# find no of seating arrangements with exactly k couples together
for table in circle_list:
    # reset counters
    seat_no = 0
    couple_counter = 0
    total_possible_arrangements += 1
    # check for couples
    while seat_no < people_present:
        # pair table by total sum. of elements. singles are unpaired
        if table[seat_no] + table[(seat_no+1) % people_present] == 2 * total_couples - 1:
            couple_counter += 1
            seat_no += 2
        else:
            seat_no += 1
    # check if condition is met
    if couple_counter == couples_together:
        arrangements_k_couples += 1

# output results
print('P(exactly k couples, out of 2n+m people, sit together)')
if arrangements_k_couples:
    print('=' + str(arrangements_k_couples) + '/' + str(total_possible_arrangements))
else:
    print('= 0')
        

# simplfying fraction by dividing by gcd, which can be found with euclidian algorithm
def euclidian_algorithm(total, arr):
    a = total
    b = arr
    q = a // b
    r = a % b
    while r:
        a = b
        b = r
        q = a // b
        r = a % b
    # gcd = last b used
    s_total = total // b
    s_arr = arr // b
    return [s_total, s_arr]
if arrangements_k_couples:
    simplified = euclidian_algorithm(total_possible_arrangements, arrangements_k_couples)
    print('=' + str(simplified[1]) + '/' + str(simplified[0]))