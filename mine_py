from random import randint
from math import ceil
from time import sleep

def fill(l, c, matrix, value):
    for i in range(0,m+2):
        for j in range(0,n+2):
            matrix[i][j] = value
    return matrix

def show(m, n, matrix, show):
    print()
    for i in range(1,m+1):
        for j in range(1,n+1):
            if show[i][j] == 1:
                if matrix[i][j] == 9:
                    print('    *',end='')
                else:
                    print('   ',matrix[i][j],end='')
            else:
                print('    _',end='')
        print('\n')

def create_matrix(m, n, matrix, value):
    line = list()
    for i in range(0,m+2):
        for j in range(0,n+2):
            line.append(value)
        matrix.append(line[:])
        line.clear()
    return matrix

def calculate_bombs(m, n, option):
    if option == 'E':
        perc = 0.12
    elif option == 'M':
        perc = 0.16
    elif option == 'H':
        perc = 0.2
    bombs = m*n*perc
    return ceil(bombs)

def sort_bombs(m, n, bombs):
    global field
    line = randint(1,m)
    column = randint(1,n)
    if field[line][column] == 9:
        return sort_bombs(m, n, bombs)
    else:
        field[line][column] = 9

def count_bombs(m, n):
    global field
    quant = 0
    for i in range(1,m+1):
        for j in range(1,n+1):
            if field[i][j] != 9:
                for k in range(i-1,i+2):
                    for l in range(j-1,j+2):
                        if field[k][l] == 9:
                            quant+=1
                field[i][j] = quant
                quant = 0

def find_area(m, n, x, y, field, zero_areas):
    global show_or_not
    positions = list()
    positions.append([x, y])
    while len(positions) > 0:
        for k in range(x-1,x+2):
            for l in range(y-1,y+2):
                show_or_not[k][l] = 1
                if field[k][l] == 0 and zero_areas[k][l] != 1 and [k,l] not in positions:
                    positions.append([k, l])
        zero_areas[x][y] = 1
        positions.pop(0)
        if len(positions) != 0:
            x = positions[0][0]
            y = positions[0][1]

def result(m, n, field, show_or_not):
    f = 0
    s = 0
    for i in range(1,m+1):
        for j in range(1,n+1):
            if field[i][j] == 9:
                f += 1
            if show_or_not[i][j] == 0:
                s += 1
    if f == s:
        return 1
                

# Main function
#   Creating the minesweeper...

m = int(input('Type the number of:\n  Lines: '))
n = int(input('  Columns: '))
option = str(input('Choose the difficulty: Easy(e)  Moderate(m)  Hard(h) ')).upper()

field = list()
field = create_matrix(m, n, field, 1)

bombs = calculate_bombs(m, n, option)
for i in range(0,bombs):
    sort_bombs(m, n, bombs)
count_bombs(m, n)

#   Playing...

show_or_not = list()
show_or_not = create_matrix(m, n, show_or_not, 0)
zero_areas = list()
zero_areas = create_matrix(m, n, zero_areas, 0)

show(m, n, field, show_or_not)
while True:
    x = int(input('Enter the coordinates:\n  x: '))
    y = int(input('  y: '))
    while show_or_not[x][y] == 1:
        x = int(input('Enter the coordinates:\n  x: '))
        y = int(input('  y: '))
    if field[x][y] == 9:
        fill(m, n, show_or_not, 1)
        show(m, n, field, show_or_not)
        print('\nYou lose.\n')
        break
    elif field[x][y] != 0:
        show_or_not[x][y] = 1
        show(m, n, field, show_or_not)
    elif field[x][y] == 0:
        find_area(m, n, x, y, field, zero_areas)
        show(m, n, field, show_or_not)
    if result(m, n, field, show_or_not) == 1:
        fill(m, n, show_or_not, 1)
        show(m, n, field, show_or_not)
        print('\nYou win.\n')
        break
sleep(30)
