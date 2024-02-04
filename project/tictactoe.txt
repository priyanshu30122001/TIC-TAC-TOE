from tkinter import *
from tkinter.messagebox import showinfo
#VARIABLES
player = 'X'
bot = 'O'
x = 2
board = {1: ' ', 2: ' ', 3: ' ',
         4: ' ', 5: ' ', 6: ' ',
         7: ' ', 8: ' ', 9: ' '}
#METHODS
def spaceIsFree(position):
    if board[position] == ' ':
        return True
    else:
        return False

def checkDraw():
    for key in board.keys():
        if (board[key] == ' '):
            return False
            exit()

    return True

def checkForWin():
    if (board[1] == board[2] and board[1] == board[3] and board[1] != ' '):
        return True
    elif (board[4] == board[5] and board[4] == board[6] and board[4] != ' '):
        return True
    elif (board[7] == board[8] and board[7] == board[9] and board[7] != ' '):
        return True
    elif (board[1] == board[4] and board[1] == board[7] and board[1] != ' '):
        return True
    elif (board[2] == board[5] and board[2] == board[8] and board[2] != ' '):
        return True
    elif (board[3] == board[6] and board[3] == board[9] and board[3] != ' '):
        return True
    elif (board[1] == board[5] and board[1] == board[9] and board[1] != ' '):
        return True
    elif (board[7] == board[5] and board[7] == board[3] and board[7] != ' '):
        return True
    else:
        return False

def checkWhichMarkWon(mark):
    if board[1] == board[2] and board[1] == board[3] and board[1] == mark:
        return True
    elif (board[4] == board[5] and board[4] == board[6] and board[4] == mark):
        return True
    elif (board[7] == board[8] and board[7] == board[9] and board[7] == mark):
        return True
    elif (board[1] == board[4] and board[1] == board[7] and board[1] == mark):
        return True
    elif (board[2] == board[5] and board[2] == board[8] and board[2] == mark):
        return True
    elif (board[3] == board[6] and board[3] == board[9] and board[3] == mark):
        return True
    elif (board[1] == board[5] and board[1] == board[9] and board[1] == mark):
        return True
    elif (board[7] == board[5] and board[7] == board[3] and board[7] == mark):
        return True
    else:
        return False


def insertLetter(letter, position):
    if spaceIsFree(position):
        board[position] = letter
        if position == 1 :
            b1["text"] = letter
            if letter == 'X':
              b1.configure(background="red")
            elif letter == 'O':
              b1.configure(background="blue")

        if position == 2 :
            b2["text"] = letter
            if letter == 'X':
              b2.configure(background="red")
            elif letter == 'O':
              b2.configure(background="blue")

        if position == 3:
            b3["text"] = letter
            if letter == 'X':
              b3.configure(background="red")
            elif letter == 'O':
              b3.configure(background="blue")

        if position == 4:
            b4["text"] = letter
            if letter == 'X':
              b4.configure(background="red")
            elif letter == 'O':
              b4.configure(background="blue")

        if position == 5:
            b5["text"] = letter
            if letter == 'X':
              b5.configure(background="red")
            elif letter == 'O':
              b5.configure(background="blue")


        if position == 6:
            b6["text"] = letter
            if letter == 'X':
              b6.configure(background="red")
            elif letter == 'O':
              b6.configure(background="blue")

        if position == 7:
            b7["text"] = letter
            if letter == 'X':
              b7.configure(background="red")
            elif letter == 'O':
              b7.configure(background="blue")

        if position == 8:
            b8["text"] = letter
            if letter == 'X':
              b8.configure(background="red")
            elif letter == 'O':
              b8.configure(background="blue")

        if position == 9:
            b9["text"] = letter
            if letter == 'X':
              b9.configure(background="red")
            elif letter == 'O':
              b9.configure(background="blue")

        if (checkDraw()):
            b1.configure(background="cyan")
            b2.configure(background="cyan")
            b3.configure(background="cyan")
            b4.configure(background="cyan")
            b5.configure(background="cyan")
            b6.configure(background="cyan")
            b7.configure(background="cyan")
            b8.configure(background="cyan")
            b9.configure(background="cyan")
            showinfo("Game over !!!!", "Draw!")
            print("Draw!")
        if checkForWin():
            if letter == 'X':
                showinfo(" won!!!!!!!!", "player X has won")
                print("Bot wins!")

            else:
                showinfo(" won!!!!!!!!", "player O has won")
                print("Player wins!")

        return


def compMove():
 global x
 if x%2!=0:
    bestScore = -800
    bestMove = 0
    for key in board.keys():
        if (board[key] == ' '):
            board[key] = bot
            score = minimax(board, 0, False)
            board[key] = ' '
            if (score > bestScore):
                bestScore = score
                bestMove = key

    insertLetter(bot, bestMove)
    x=x+1
    return


def minimax(board, depth, isMaximizing):
    if (checkWhichMarkWon(bot)):
        return 1
    elif (checkWhichMarkWon(player)):
        return -1
    elif (checkDraw()):
        return 0

    if (isMaximizing):
        bestScore = -800
        for key in board.keys():
            if (board[key] == ' '):
                board[key] = bot
                score = minimax(board, depth + 1, False)
                board[key] = ' '
                if (score > bestScore):
                    bestScore = score
        return bestScore

    else:
        bestScore = 800
        for key in board.keys():
            if (board[key] == ' '):
                board[key] = player
                score = minimax(board, depth + 1, True)
                board[key] = ' '
                if (score < bestScore):
                    bestScore = score
        return bestScore




def give_number(number):
    global x
    if number == 1 and x%2==0:
        insertLetter(player, 1)
        x = x + 1
        return 1

    if number == 2 and x%2==0:
        insertLetter(player, 2)
        x = x + 1
        return 2
    if number == 3 and x%2==0:
        insertLetter(player, 3)
        x = x + 1
        return 3
    if number == 4 and x%2==0:
        insertLetter(player, 4)
        x = x + 1
        return 4
    if number == 5 and x%2==0:
        insertLetter(player, 5)
        x = x + 1
        return 5
    if number == 6 and x%2==0:
        insertLetter(player, 6)
        x = x + 1
        return 6
    if number == 7 and x%2==0:
        insertLetter(player, 7)
        x = x + 1
        return 7
    if number == 8 and x%2==0:
        insertLetter(player, 8)
        x = x + 1
        return 8
    if number == 9 and x%2==0:
        insertLetter(player, 9)
        x = x + 1
        return 9



def reset():
    global x, board
    board = {1: ' ', 2: ' ', 3: ' ',
             4: ' ', 5: ' ', 6: ' ',
             7: ' ', 8: ' ', 9: ' '}
    x = 2

    b1["text"] = " "
    b2["text"] = " "
    b3["text"] = " "
    b4["text"] = " "
    b5["text"] = " "
    b6["text"] = " "
    b7["text"] = " "
    b8["text"] = " "
    b9["text"] = " "

    b1.configure(background="SystemButtonFace")
    b2.configure(background="SystemButtonFace")
    b3.configure(background="SystemButtonFace")
    b4.configure(background="SystemButtonFace")
    b5.configure(background="SystemButtonFace")
    b6.configure(background="SystemButtonFace")
    b7.configure(background="SystemButtonFace")
    b8.configure(background="SystemButtonFace")
    b9.configure(background="SystemButtonFace")

# MAIN LOOP OF THE BOARD INCLUDES BUTTONS
root = Tk()

l0 = Label(root, text="\       \       \           \ ",font="times 15 ", background="black")
l0.grid(row=0, column=1)

l1 = Label(root, text="   TIC TAC TOE   ", font="times 15 ",background="black", foreground="white")
l1.grid(row=0, column=2)

l2 = Label(root, text="\           \       \       \ ", font="times 15", background="black")
l2.grid(row=0, column=3)

l3 = Label(root, text="Player 1 : X ", font="times 15 ")
l3.grid(row=1, column=1)

l4 = Label(root, text="     VS    ", font="times 15 ")
l4.grid(row=1, column=2)

l5 = Label(root, text="COMPUTER : O ", font="times 15 ")
l5.grid(row=1, column=3)

b1 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(1))
b1.grid(row=2, column=1)

b2 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(2))
b2.grid(row=2, column=2)

b3 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(3))
b3.grid(row=2, column=3)

b4 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(4))
b4.grid(row=5, column=1)

b5 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(5))
b5.grid(row=5, column=2)

b6 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(6))
b6.grid(row=5, column=3)

b7 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(7))
b7.grid(row=8, column=1)

b8 = Button(root, text=" ", width=20, height=10, command=lambda:give_number(8))
b8.grid(row=8, column=2)

b9 = Button(root, text=" ", width=20, height=10, command=lambda: give_number(9))
b9.grid(row=8, column=3)

btnReset = Button(root, text="RESET GAME ", width=20, height=5, command=reset)
btnReset.grid(row=9, column=1)

btnQuit = Button(root, text=" Quit \n Game  ", font="times 10", width=20, height=5, command=root.quit, background="black", foreground="white")
btnQuit.grid(row=9, column=2)

btnNext = Button(root, text="Next ", width=20, height=5, command=compMove)
btnNext.grid(row=9, column=3)

root.mainloop()
