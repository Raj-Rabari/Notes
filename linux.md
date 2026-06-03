mkdir => to make directory , use -p to create nested directory if parent doesn't exist.
touch => it updates the modification time of existing file but creates new one so developers uses that to create new file.
cp => copy file, accepts two argument source & destination. use -r to copy folder & it's content.
mv => move file from one path to another path. you can use it to rename file, use -r to mv or rename folder
rm => removes file, -r to remove folder, -f forcefully deletes everything doesn't ask for confirmation if the item is write-protected. terminal doesn't have recycle bin so it got remove forever.

In linux, everything is file. Because OS treats everything as a file. It uses universal concept called file descriptor to manage them. whenever you starts any process whether it's simple ls command or react dev server or node server - it assigns three file descriptor to that process.

stdin(FD 0) => standard input from where os takes input (defaults to keyboard)
stdout(FD 1) => standard output where process writes data (defaults to your terminal)
stderr(FD 2) => where process writes error messages (also defaults to your terminal)

'>' => redirects output to any file you specify. overwrite whatever is there.
'>>' => same as '>' but appends the content

by default > , redirects stdout stream only. but if your app/process crashes then it will goes to your output screeen so you can specify file descriptor using numbers before '>' or '>>' like 2> or 2>>. use &> or &>> to redirect both

interprocess communication '|' The pipe:

    when you use | after one command OS creates annonyms buffer in RAM. It then connects stdout of left command to stdin of right command. instead of writing data to hard drive and reading them back. data streams from one process to another process in real time.

The grep (global regular expression print):

    it reads text data stream from any file or stdin of any process and prints the matching pattern.

    i.e grep "ERROR" app.log

    grep -i "ERROR" app.log // case sensitive

    grep -B 2 -A 2 "ERROR" app.log // if you want to see what happens before error and after that so this will print 2 lines before error occurs and two lines after error occurs.

Permission string: it is exactly of 10 characters. first character is file type (- normal file, d=directory,l=symbolik link), the next three are permission of owner, next three are permission of group, next three are anyone else. like

    -rwxr-xr-- => type file, owner can do anything, group member can read & execute, other only can read
    drwxr-xr-- => type directory, and as above

Math system for permssion:

    read = 4
    write = 2
    execute = 1

    7 (4+2+1) = Full access (rwx)

    6 (4+2) = Read and Write (rw-)

    5 (4+1) = Read and Execute (r-x)

    4 (4) = Read only (r--)

    0 (0) = No access (---)

    chmod 777 means full access to everyone. first 7 is for owner, then group then anyone else.
