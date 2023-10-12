---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: id_Tictactoe
title: "TicTacToe in ROS"

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Tanay Ranjan
# multiple category is not supported
category: Projects
# multiple tag entries are possible
tags: [ROS, Python]
# thumbnail image for post
img: ":tictactoe_pic.png"
# disable comments on this page
#comments_disable: true

# publish date
date: 2022-01-15 10:04:30 +0900

# seo
# if not specified, date will be used.
#meta_modify_date: 2022-01-01 10:04:30 +0900
# check the meta_common_description in _data/owner/[language].yml
#meta_description: ""

# optional
# please use the "image_viewer_on" below to enable image viewer for individual pages or posts (_posts/ or [language]/_posts folders).
# image viewer can be enabled or disabled for all posts using the "image_viewer_posts: true" setting in _data/conf/main.yml.
#image_viewer_on: true
# please use the "image_lazy_loader_on" below to enable image lazy loader for individual pages or posts (_posts/ or [language]/_posts folders).
# image lazy loader can be enabled or disabled for all posts using the "image_lazy_loader_posts: true" setting in _data/conf/main.yml.
#image_lazy_loader_on: true
# exclude from on site search
#on_site_search_exclude: true
# exclude from search engines
#search_engine_exclude: true
# to disable this page, simply set published: false or delete this file
#published: false
---

# Problem Statement

Implement a TicTacToe game using services in ROS with 3 nodes - Node 1 acts as Player 1, Node 2 acts as Player 2, and Node 3 acts as the Computer (provides the board).

# Solution 

For approaching this problem, I made 4 files for Node 3 (so the code doesn't get messy) and 1 file for Node 2 and 1 file for Node 1.

## Custom Service File 

For this problem, I made custom service file for passing request and getting response

### The srv file (moe.srv) :-

``` 
int64[] gaming_data
---
int64 row
int64 col
```

In this file, 
- The array `gaming_data` present in request part of srv file, will be use to request 3x3 array which contains information of the tictactoe board, with each element of array representing each element of the board. If value of a element in the array is 0, then it means board is empty, if it is 1, then that position in the board is filled with 'X' mark, and if it is 2, then that position in the board is filled wth 'O' mark.
- The variable `row` and `col` in response part of the srv file, will be use for giving response in terms of which row and column has to be filled in the board when a player enters input from one of the nodes 'Node 1' and 'Node 2'.

We will further discuss how we will use each variable in this solution as we move on
## Node 3

Node 1 and Node 2 will take input from Player 1 and Player 2 and give to Node 3 using services, which means, Node 1 and Node 2 will act as a server and Node 3 will act as a client, which basically calls each node when their turns come.
And as mentioned already, the Node 3 is divided into 4 files - main.py, display.py, draw.py, checker.py

### The code for display.py:- 
``` python
from draw import *
import sys

class Picture_Class:
    def __init__(self):
        self.game_data = [[0 for i in range(3)] for j in range(3)]
        self.picture_data = [[' ' for i in range(41)] for j in range(17)]

        self.__setup__()

    def __setup__(self):
        for i in range(17):
            self.picture_data[i][0] = '|'
            self.picture_data[i][13] = '|'
            self.picture_data[i][26] = '|'
            self.picture_data[i][39] = '|'

        for i in range(41):
            self.picture_data[5][i] = '-'
            self.picture_data[11][i] = '-'

    def print_result(self):
        for i in range(17):
            for j in range(41):
                sys.stdout.write(str(self.picture_data[i][j]))
            sys.stdout.write('\n')

    def upload_data(self, some_array):
        self.game_data = some_array
        self.__refresh__()

    def __refresh__(self):
        for i in range(3):
            for j in range(3):
                if (self.game_data[i][j] == 1):
                    self.picture_data = draw_x(self.picture_data, i, j)
                elif (self.game_data[i][j] == 2):
                    self.picture_data = draw_o(self.picture_data, i, j)
```

This file contains code for a class which contains functions, arrays and variable which will be useful for displaying the board in terminal
In this code,
- `gaming_data` array will be array which will be storing data of the tictactoe board (same array discussed during discussion of srv file)
- `picture_data` array will contains keyboard symbols in an arranged way such that if we print each row of that array one after the another in the terminal, it will display the tictactoe board
For example :-
![tictactoe.png](:tictactoe_pic.png)
- The `__setup__()` function is initializing the `picture_data` array with filling '|' and '-' such that it will create border line of tictactoe board, and this function is called during intialization of the object
![23757b54f9b4e69b6b0852b0576e7043.png](:23757b54f9b4e69b6b0852b0576e7043.png)
- `print_result()` function prints the `picture_data` array in the terminal
- `upload_data()` fucntion uploads the `gaming_data` array and calls `__refresh__()` function
- `__refresh__()` function adds 'X' and 'O' in the `picture_data` array using `draw_x()` and `draw_o()`, which is defined in **draw.py** file

**Note** :- Here, I used `sys` for printing instead of normal print function because when we use normal print function, it automatically starts from new line. There is a way to prevent it by using `print(<something>, end='')`, but this only works in Python3 and my ROS was compatable with Python2.


### The code for draw.py:- 
``` python
def draw_x(some_data, a, b):
    x = 13*b + 2
    y = 6*a
    some_data[y][x] = 'x'
    some_data[y][x+1] = 'x'
    some_data[y][x+8] = 'x'
    some_data[y][x+9] = 'x'
    some_data[y+1][x+2] = 'x'
    some_data[y+1][x+3] = 'x'
    some_data[y+1][x+6] = 'x'
    some_data[y+1][x+7] = 'x'
    some_data[y+2][x+4] = 'x'
    some_data[y+2][x+5] = 'x'
    some_data[y+3][x+2] = 'x'
    some_data[y+3][x+3] = 'x'
    some_data[y+3][x+6] = 'x'
    some_data[y+3][x+7] = 'x'
    some_data[y+4][x] = 'x'
    some_data[y+4][x+1] = 'x'
    some_data[y+4][x+8] = 'x'
    some_data[y+4][x+9] = 'x'
    return some_data


def draw_o(some_data, a, b):
    x = 13*b + 2
    y = 6*a
    some_data[y][x+3] = 'o'
    some_data[y][x+4] = 'o'
    some_data[y][x+5] = 'o'
    some_data[y][x+6] = 'o'
    some_data[y+1][x+1] = 'o'
    some_data[y+1][x+2] = 'o'
    some_data[y+1][x+7] = 'o'
    some_data[y+1][x+8] = 'o'
    some_data[y+2][x] = 'o'
    some_data[y+2][x+1] = 'o'
    some_data[y+2][x+8] = 'o'
    some_data[y+2][x+9] = 'o'
    some_data[y+4][x+3] = 'o'
    some_data[y+4][x+4] = 'o'
    some_data[y+4][x+5] = 'o'
    some_data[y+4][x+6] = 'o'
    some_data[y+3][x+1] = 'o'
    some_data[y+3][x+2] = 'o'
    some_data[y+3][x+7] = 'o'
    some_data[y+3][x+8] = 'o'
    return some_data

```
This file contains the `draw_x()` and `draw_o()` functions which basically takes **row** and **column** of the tictactoe board and apply a certain equation that relates position of element of the board to the `picture_data` array and fills it with symbols in certain manner, such that during printing the array, it will represent 'X' and 'O'.

### The code for checker.py:-
``` python
def row_check(some_array):
    a = 0
    b = 0
    for i in range(3):
        if ((some_array[i][0] == some_array[i][1]) and (some_array[i][1] == some_array[i][2])):
            a = 1
            b = some_array[i][0]
            break
    return [a, b]


def column_check(some_array):
    a = 0
    b = 0
    for i in range(3):
        if ((some_array[0][i] == some_array[1][i]) and (some_array[1][i] == some_array[2][i])):
            a = 2
            b = some_array[0][i]
            break
    return [a, b]


def cross_check(some_array):
    if (((some_array[0][0] == some_array[1][1]) and (some_array[1][1] == some_array[2][2])) or ((some_array[0][2] == some_array[1][1]) and (some_array[1][1] == some_array[2][0]))):
        return [3, some_array[1][1]]
    return [0, 0]


def check(some_array):
    a = column_check(some_array)
    if (a[0] != 0):
        return a[1]
    a = row_check(some_array)
    if (a[0] != 0):
        return a[1]
    a = cross_check(some_array)
    if (a[0] != 0):
        return a[1]
    return 0
```
This file has functions for checking if any player has won or not
- `row_check` will take `gaming_data` array in entry and scan if any entry in every row is same or not and return an array containing 2 elements in which 1st element contain if someone has won or not in '1' and '0' and 2nd element will contain the information of player who won
- Same for `column_check` and and `cross_check` for check in column and cross direction respectively.
- These function will be called by `check()` function, and return which player won. If no one won, then it will return 0


### The code for main.py:- 
```python
1. #! /usr/bin/python2
2. import rospy
3. from tictactoe.srv import moeRequest, moe
4. from std_msgs.msg import Int64
5. from display import *
6. from draw import *
7. from checker import *
8. import sys
9. requ = moeRequest()
10. gaming_data = [[0 for i in range(3)] for j in range(3)]
11. tictactoe = Picture_Class()
12. func1 = rospy.ServiceProxy('player_one_server', moe)
13. func2 = rospy.ServiceProxy('player_two_server', moe)
14. 
15. def input_pos(a):                                           # Defining a function for taking input from each node used by players
16.     requ.gaming_data = [Int64(0) for i in range(9)]
17.     for i in range(3):
18.         for j in range(3):
19.             requ.gaming_data[j+(3*i)] = gaming_data[i][j]
20.     if (a % 2 == 0):
21.         print('1st player turn\n\n')
22.         rospy.wait_for_service('player_one_server')
23.         response = func1(requ)
24.         gaming_data[response.row-1][response.col-1] = 1
25.         
26.     else:
27.         print('2nd player turn')
28.         rospy.wait_for_service('player_two_server')
29.         response = func2(requ)
30.         gaming_data[response.row-1][response.col-1] = 2
31. 
32. def main():
33.     print('\n\n')
34.     for i in range(9):
35.         input_pos(i)
36.         tictactoe.upload_data(gaming_data)
37.         tictactoe.print_result()
38.         if (check(gaming_data) != 0):
39.             print('\n\nCongrats '),
40.             if (check(gaming_data) == 1):
41.                 sys.stdout.write(str("1st"))
42.             if (check(gaming_data) == 2):
43.                 sys.stdout.write(str('2nd'))
44.             print(' player, You won...!!\n\n')
45.             break
46.         print('\n\n')
47.     if (check(gaming_data) == 0):
48.         print('Tie...!!')
49.     if (raw_input('Do you want to play again (Y/N) : ') == "Y"):
50.         main()
51. 
52. 
53. if __name__ == '__main__':
54.     try:
55.         rospy.loginfo('Displayer Activated\n\nStarting the game for data...')
56.         main()
57.     except rospy.ROSInterruptException():
58.         pass
```

This code will be main code, and this code will be only executed for running Node 3.
- The Line 1 code is shebang which basically tells ROS that which language is this code is written
- From Line 2 to 8, I am importing all functions for display.py, checker.py and draw.py, importing service file, and Int64 data type for initializing `gaming_data` array
- In Line 15, we are defining a function which basically calls Node 1 and Node 2 using services and takes input from them, and then save the inputs to the `gaming_data` array
- Line 32 will be defining the function `main()` which will be calling all functions to run the code.
- Line 53 will call the `main()` function in a safely way, such that during some failure due to an error, we could stop the process by interuppting.


## Node 1 & Node 2
Code of Node 1 and Node 2 will be similar, so I will be explaining code of Node 1 only
### The code :-
``` python
import rospy
from tictactoe.srv import moe, moeResponse

respo = moeResponse()
rospy.init_node('player_one')

def command(req):
    input_pos(req)
    return respo


def input_pos(req):
    print('\n\nYour turn\n\n')
    b = int(input('Row number : '))
    c = int(input('Column number : '))
    if (((0 <= b and b <= 3) and (0 <= c and c <= 3)) and (req.gaming_data[((b-1)*3)+c-1] == 0)):
        respo.row = b
        respo.col = c
    else:
        print('\nWrong Input!!...Try once again\n')
        input_pos(req)



def callback():
    print('Player 1 ready.......Waiting for Displayer')
    rospy.Service('/player_one_server', moe, command)
    rospy.spin()


if __name__ == '__main__':
    try:
        rospy.loginfo('Player One Activated\n\nWaiting for data...')
        callback()
    except rospy.ROSInterruptException():
        pass

```
In this code :-
- `callback()` function will activate the server '/player_one_server', which will be called by Node 3 during player one turn
- `input_pos()` will be called by `command()` function, which will be called by the server.
- `input_pos()` when called, will take input from the player.
- Now, the `gaming_data` array is passed in request is for preventing the player from marking the position which is already being marked.