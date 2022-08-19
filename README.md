# Python-Handling-Exceptions
Examine exception handlers that have been added to the code.

Examine the code in lines 115 through 123


Lines 117 through 119 have been indented under try:. These are the statements that create the output folder if necessary and set it to be the current working directory.
Lines 121 through 123 are indented under the except: block. They report a problem with the output folder and will cause the save_list method to return False.
If any sort of exception occurs within the code under the try: block, the code under the except: block will be executed to handle the exception.
This will enable the program to deal with any sort of exception that is thrown when the statements try to create or navigate to the output folder. For example, although the code in lines 112 and 113 should succeed in getting the path to the desktop directory on most Windows and Linux computers, there are some unusual circumstances in which the desktop directory can't be identified this way. Also, in some circumstances, it is possible that the program might not have adequate rights to create the output folder.
Wrapping these statements in an exception handler provides a fail-safe for this routine, and provides helpful information to a user encountering the problem.
Examine the exception-handling code starting in line 132.


The try statement protects the code in lines 134 through 139, where the output log file is saved.
The except: block in lines 141 through 145 will execute if there is an exception due to file permissions. This exception handler can be specific about the fact that there was a problem related to file permissions.
If an exception not due to file permissions occurs, the more general handler in lines 147 through 150 will execute. This is a more general handler, so it provides less specific information about the nature of the problem.
Examine the block starting in line 152.


The else: block executes only if the entire try: block succeeded and no except: blocks had to execute.
Nested under the else: block is another complete try … except … else handler, in lines 154 through 163. This nested code tries to copy the archive file, and provides its own exception handler should something go wrong.
Run the program to create a log file.

In the Project pane, right-click wordcount.py and select Run 'wordcount'.

At the prompts, enter bartleby.txt, y, and y.

The program runs, producing a log file named bartleby_results.txt, as well as a backup file. The next time the program processes bartleby.txt, it will have to replace the bartleby_results.txt log file.

Test the exception-handling code by marking the log file as read-only.

On the desktop, right-click the Wordcount Output folder, and select Properties.

In the Attributes section, check the Read-only attribute as shown.


You may have to select the check box twice to change it to a check mark.

Select OK.


Select OK.

The output folder and files it contains will all be marked as read only.

In PyCharm, in the Project pane, right-click wordcount.py and select Run 'wordcount'.

At the prompts, enter bartleby.txt, y, and y.

Examine the Run console.


Because the old bartleby_results.txt file is marked read only, it can't be opened for writing, and it produced a PermissionError exception.
Because the PermissionError exception is handled, this problem did not cause the program to end abnormally. It simply reported the problem to the user, skipped past any remaining statements in the try: block, and resumed with the next block after the try: block and its exception handlers, producing a list of files currently in the output folder.
Revert the output folder's read-only attribute.

On the desktop, right-click the Wordcount Output folder, and select Properties.
In the Wordcount Output Properties dialog box, uncheck the Read-only attribute, and select OK.
In the Confirm Attribute Changes dialog box, select OK.
Verify that an exception handler would be useful in the routine that reads the input file.

In PyCharm, in the Project pane, right-click wordcount.py and select Run 'wordcount'.

At the prompt, enter fakefile.txt


This problem could have been avoided if the code included an error prevention routine (e.g., using os.path.isfile to check for an existing file before trying to open it) or by using try … except to handle the exception.
Because the exception is not handled by the WordCount program, the Python interpreter reports it to the user. Often, this way of dealing with exceptions is harsh and potentially confusing to an end user.
Wrap the code that reads the input file within a try … except handler.

Position the insertion point at the end of line 51 and press Enter.

Type try:

Select the statements in lines 53 through 63, and press Tab to indent them as shown.


Position the insertion point at the end of line 63, and press Enter twice.

Enter the code as shown.


If the code under try: executes without causing an exception, the read_input_file method will return True.
If any statement in the try: block causes an exception, execution of the try: block will cease with that statement. If the exception is a FileNotFoundError, then execution of the code will resume at line 66, printing a message (line 66) and causing the read_input_file method to return False (line 67).
Identify what the main script does when the read_input_file method returns False.

In the Project pane, double-click wordcount.py.

Examine the code that calls the read_input_file method.


Line 14 begins a loop that will be used to continue prompting the user for input until an acceptable value is entered.
Line 15 places the user's input into a variable named input_file.
Line 16 places the results of calling the read_input_file method (True or False) into a variable named **successful_rea**d.
If successful_read is True, then the break statement in line 18 executes, exiting the while loop. Otherwise (not a successful read), the routine loops again, prompting the user to enter another file name.
Test the new exception handler.

In PyCharm, in the Project pane, right-click wordcount.py and select Run 'wordcount'.

At the prompt, enter fakefile.txt

The read operation fails since this file doesn't exist. You are prompted again to enter a file name.

At the prompt, enter small.txt

The file is read successfully, and the input loop is exited.

In the Run window, close the wordcount tab, and select Terminate.

Add code to handle an exception when reading the word list file.

Select the wordprocess.py editor tab.

Starting in line 27, examine the operations performed in the __init__ function.


When a new WordProcess object is created, various attributes (wordlist, words_in_manuscript, and so forth) are initialized in lines 32 through 36.
In lines 42 through 44, various file operations are performed to load the word list from wordsEn.txt.
The wordsEn.txt file is an essential component of the WordCount program. It is always expected to be found in the same directory as the script it's loaded from, which is obtained by getting the value in sys.path[0] in line 40.
There is a possibility, of course, that the WordCount program may not be installed correctly on another user's computer, and the word list file might be missing. If this happens, it would be helpful to inform the user what the problem is. Also, the program should not be allowed to run until the problem is corrected, since it is required in order to function.
Indent the code in lines 42 through 44 and add the code shown here.


Lines 41 through 44 try to read the word list file.
If there is an exception when reading the word list, the program is exited in line 46, explaining that the program can't run without the word list file.
Test the exception handler.

In the Project pane, right-click wordsEn.txt, and select Show in Explorer.

In the File Explorer window, rename the wordsEn.txt file as XwordsEn.txt

This will enable you to simulate what would happen if the file is not found.

In PyCharm, in the Project pane, right-click wordcount.py and select Run 'wordcount'.


The program immediately exits with a code 1. The message explains to the user what went wrong, providing a clue on how to resolve it.

In the File Explorer window, rename the XwordsEn.txt file back to wordsEn.txt.

In PyCharm, in the Project pane, right-click wordcount.py and select Run 'wordcount'.

The program starts successfully, and prompts the user for a file to analyze.

In the Run window, close the wordcount tab, and select Terminate.

