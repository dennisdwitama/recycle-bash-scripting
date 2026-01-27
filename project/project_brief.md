# Recycle and Restore Project Brief
 
**Problem:** UNIX has no recycle bin at the command line. When you remove a file or directory, it is gone and cannot be restored. This project is to write a recycle script and a restore script. This will provide users with a recycle bin which can be used to safely delete and restore files. 
 
## Phase 1 -- Basic Functionality
 
Write a script called `recycle` that mimics the `rm` command. The `recycle` script should be able to accept the name of a file as a command line argument as `rm` does, but instead of deleting the file, your script should move it to a `recyclebin` directory called `recyclebin` located in your home directory. 
 
- The script name is `recycle` and will be stored in `$HOME/project`. 
- The recycle bin will be `$HOME/recyclebin`. Ensure that *your script* creates this directory. 
- The file to be deleted will be a command line argument and the script should be executed as follows: `bash recycle fileName`. 
- The script must test for the following error conditions. When any of the following are encountered, the script must display the same kind of error messages as the `rm` command, and the script must set a non-zero exit status to terminate: 
  - a) No filename provided. 
  - b) Name provided does not exist. 
  - c) Directory name provided instead of a filename. 
  - d) Filename provided is `recycle`. In this case, display the error message "Attempting to delete recycle -- operation aborted" and terminate the script with a non-zero exit status. Do not generate this error if the filename is only similar to `recycle`. For example, a file called `recycle2015` should not generate any error messages. Be sure to create a hard link for your script before testing this error. 
- The filenames in the `recyclebin` will be in the following format: `fileName_inode`. For example, if a file named `f1` with inode `1234` is recycled, the file in the `recyclebin` will be named `f1_1234`. This gets around the potential problem of deleting two files with the same name. The `recyclebin` will only contain files, not directories. 
- Create a hidden file called `.restore.info` in `$HOME`. Each record in this file will contain the name of the file in the `recyclebin`, followed by a colon, followed by the original absolute path of the file. For example, if a file called `file1`, with an inode of `1234` was recycled from the `/home/trainee1` directory, `.restore.info` will contain: `file1_1234:/home/trainee1/file1`. If another file named `file1`, with an inode of `5432`, was recycled from the `/home/trainee1/testing` directory, then `.restore.info` will contain: `file1_1234:/home/trainee1/file1` and `file1_5432:/home/trainee1/testing/file1`. 
 
## Phase 2 -- Basic Restore
 
Write a script called `restore` to restore individual files back to their original location. 
 
The user will determine which file is to be restored and use the file name with inode number in order to restore the file. For example: `bash restore f1_1234`. 
 
- Script name is `restore` and stored in `$HOME/project`. 
- The file to be restored will be a command line argument and the script should be executed as follows: `bash restore f1_1234`. This is the name of the file in `$HOME/recyclebin`. 
- The file must be restored to its original location, using the pathname stored in the `.restore.info` file. 
- The script should test for the following error conditions and display similar error messages to the `rm` command: 
  - a) No filename provided - Display an error message if no file provided as argument, and set an error exit status. 
  - b) File does not exist - Display an error message if file supplied does not exist, and terminate the script. 
- The script must check whether the file being restored already exists in the target directory. If it does, the user will be asked "Do you want to overwrite? y/n ". The script must restore the file if the user types `y`, `Y`, or any word beginning with `y` or `Y` to this prompt, and not restore it if they type *anything* else. 
- After the file has been successfully restored, the entry in the `.restore.info` file will be deleted. 
 
## Phase 3 -- Multiple Files, Wildcards and Option Flags
 
The `rm` command can remove multiple files, for example `rm file1 file2 file3`. `rm` can also use wildcards, for example `rm file*`. The `rm` command can use the `-i` option, for interactive mode, and the `-v` option for verbose mode. Add this functionality to your `recycle` script. 
 
- Ensure the script can recycle multiple files, even if some of the files provided do not exist. Wildcards should work as well. This is how `rm` works. 
- Update the script to allow the `-i` option. If used, prompt the user, asking for confirmation, in the same way as `rm -i`. A response beginning with `y` or `Y` means yes. All other responses mean no. 
- Update the script to allow the `-v` option. Display a message confirming deletion, in the same way as `rm -v`. 
- Ensure the script works with both options in either order, `-iv` and `-vi`. 
- If an invalid option is passed into the script, display an error message which shows the offending option value, and terminate the script with a non-zero exit status, just like the `rm` command. 
 
## Phase 4 -- Recycle Files Recursively
 
The `rm` command can remove directories and their contents using the `-r` option. Add this functionality to your `recycle` script. 
 
- Update the `recycle` script to support the use of the `-r` option to remove a directory and recycle its contents. 
- The `$HOME/recyclebin` directory will have a flat structure, containing only files. Do not move directories into `$HOME/recyclebin`. It is only necessary to move files. Once all files have been moved, delete the directory in question. The entry in `.restore.info` will record the same file location information as in Phase 1, item 6, for later restoration. 
 
## Phase 5 -- Restore Files Recycled Recursively
 
Update the `restore` script to enable the restoration of files that were recycled recursively. 
 
- Ensure your script is able to restore files previously recycled using `recycle -r`. 
- The script will identify the directory to restore the file to, by accessing the `.restore.info` file. It will then recreate this directory, if necessary, before restoring the file. Finally, it will remove the appropriate entry in `.restore.info`. 
 
## Testing
 
It is essential that you test it as you go along. Be sure you test each piece of functionality. It is important to get each phase working and thoroughly tested before moving onto the next phase. Later phases are dependent on a fully functional phase 1. 
 
When testing, you need to be aware that the script will be marked by someone logged in as a different user. It is important you remove any references to your personal environment, as they will cause the script to fail when being marked. 
 
## Coding Standards
 
The coding standards the script must conform to are: 
 
- Use comments to document the script. 
- Write tidy code using blank lines and indentation. 
- Remove all troubleshooting code and commented out code. 
- Only the commands taught in this course may be used in this project. 
 
## Backups
 
Ensure you backup your scripts. It is highly recommended you create hard links for `recycle` and `restore`. 
 
### Marking
 
Your scripts will be executed to check that they work. Your will be awarded 0 points if your project scripts do not execute. Any script whose logic cannot be explained or defended will similarly be awarded 0 points. 
