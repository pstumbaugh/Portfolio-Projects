CS 372 - Project 2
Patrick Stumbaugh

How to run:
    On console from the folder containing the .py files, type: 
        python3 rdt_main.py
    Then hit enter and the program will start.
    Hit enter to send a new set of data packets, as instructed in the console. When all has been send, you will 
    receive a notice saying all data was received and the program will end.

This program will simulate sending packets via TCP protocol. It assumes it is sending on an unreliable channel.
The unreliable channel includes forced errors including: data errors, dropped packets, delayed packets and data out of order
This program will accomodate those errors and adjust in order to assemble the correct information.