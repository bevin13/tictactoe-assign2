import random
import numpy as np

def display(choice):
    print("| {} | {} | {} |".format(choice[0][0], choice[0][1], choice[0][2]))
    print("| {} | {} | {} |".format(choice[1][0], choice[1][1], choice[1][2]))
    print("| {} | {} | {} | \n".format(choice[2][0], choice[2][1], choice[2][2]))

def comp(val, sym):
    out_row = [[0, 0, 0], [1, 1, 1], [2, 2, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2]]
    out_col = [[0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 0, 0], [1, 1, 1], [2, 2, 2], [0, 1, 2], [2, 1, 0]]
    for row, col in zip(out_row, out_col):
        if val[row[0]][col[0]] == val[row[1]][col[1]] == val[row[2]][col[2]] == sym:
            return True
    return False

def play_game():
    list = [None] * 10
    flag = 0
    options = ["X", "O"]
    digits = np.array([[" ", " ", " "], [" ", " ", " "], [" ", " ", " "]])
    eg = ["00", "01", "02","10", "11", "12", "20", "21", "22"]
    for i in range(0, 9):
        if i % 2 == 00:
            while True:
                try:
                    player = str(input("Type a position :"))
                    if player in eg:
                        eg.remove(player)
                        digits[int(player[0])][int(player[1])] = options[0]
                        display(digits)
                        list[i] = digits.copy()
                        if comp(digits, options[0]):
                            result = "Player Won the Game"
                            print(result, "\n")
                            list[9] = result
                            flag = 1
                        break
                    else:
                        print("please select other position")
                        continue
                except:
                    print("please Enter correct input :")
            if flag == 1:
                break
        else:
            print("Wait for computer")
            computer = random.choice(eg)
            eg.remove(computer)
            digits[int(computer[0])][int(computer[1])] = options[1]
            display(digits)
            list[i] = digits.copy()
            if comp(digits, options[1]):
                result = "Computer Won the Game"
                print(result, "\n")
                list[9] = result
                break
    if flag == 0:
        result = "Game is Tied"
        print(result)
        list[9] = result

    return list

games = 1
k = {}
while games <= 10:
    print("Game {}:".format(games))
    display([["00", "01", "02"], ["10", "11", "12"], ["20", "21" , "22"]])
    k[games] = play_game()
    games += 1

details = int(input("Do you want to see any round :"))
for key, value in k.items():
    if key == details:
        for element in range(len(value) - 1):
            if value[element] is not None:
                print("Move {} ({})".format(element + 1, "player" if element % 2 == 0 else "computer"))
                display(value[element])
        print(value[-1])
