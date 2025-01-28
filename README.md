# DirDupeExplorer
Directory Duplicate Explorer - A simple script that displays an unordered directory in an HTML file (GUI) while marking all duplicates. It is meant for finding duplicates of files (e.g. Pictures, documents and everything else) in messy directories like old backups (the reason I made it). It does not automatically modify anything in the directory, it just viasulizes the content of the directory while highlighting duplicates. Files are compared with md5 checksums.

An example output: `DirDupeExplorer-out-20250128005926.html`. Just download and open it in any webbrowser.

It does only work on Linux (maybe Mac?). It currently doesn't work on Windows because Microsoft uses backslash instead of forwardslash in there directories (those idiots). If someone actually finds this and is interested in an windows version, please let me know (open an issue).

If someone is in any other way interrested, also just open an issue. 

## Usage

No installation - pretty much no setup. Just download dirDupeExp.py and run it via:

`python dirDupeExp.py`

There it will ask you for the directory you want to scan. Just press enter if you want to scan the current directory. If you want to scan a different directory, input the desired path.

Depending on the size of the directory and the storage medium (SSD/HDD) this may take some time. In the folder you have run the script from, there will be a `.html` file created, which is opened in your browser automatically. The GUI is pretty self explanatory, it behaves like a simplistic file explorer with some settings for the UI on the top.

Here is an example image:
![image](https://github.com/user-attachments/assets/46eb2e5c-947c-4a60-adfd-4236db3e82f5)

If there are duplicates, they will be listed to the right of the file. Hover over the files to display the md5 checksums. Thats it!

### Cleanup
Two files are created when scanning a directory:

- `DirDupeExplorer-out-20250128002424.html` - The HTML file with the explorer GUI
- `rawout20250128002424.txt` - The raw output, an list of unsorted checksums and filepaths

Both can be deleted after use. *The number is just the date and time of the scan*.

### Additional ifno
One can also create an alias for that script, just add `alias dirDupe='python PATH/TO/dirDupeExp.py'` to your .bashrc file.

## How it Works
This is an messy unholy amalgamation of Bash, Pyton, JavaScript and HTML. None of this is good practise probably, so be aware.

But yeah, this is what this script does:
1. Create a list of md5 checksums for all files in the desired directory recursively via the Bash command: `find PATH/TO/DIR/ ! -empty -type f -exec md5sum {} +`.
2. Split the output into an array of checksums and files `checksumlist = checksumstr.splitlines()`.
3. Parse that array into an giant string that is just an HTML file: `pyoutvar = "var checksumlist = JSON.parse('{0}');".format(json.dumps(checksumlist))`. (I know, crazy, right?);
4. Create the HTML file and automatically open it in the browser.
5. Do some for-loop - JavaScript shenadigans to put all of that info in an somewhat-acceptable file explorer-thingy.
6. While doing step 5, it also scans for files with the same checksum and lists them next to the current file.



