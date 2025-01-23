	git init		=>	Initialized local repo.	// It will create .git directory inside that directory.

				// Create a file named abcd.sh
				// Create a file named 123.txt


	git status

	git add .		// Will add all the files
	git add *		// Will add all the files
	git add *.txt
	git add abcd.sh

				// After adding the files to staging area, you can commit those whatever you required.

	git commit -m "message here" <file-names-here>

	git commit -m "If you dont specify any file name here, it will commit all the files in the staging area not in that directory files"
	
	git commit -m "Here we are specifying the filename,So it will commit only one file"  123.txt
	

				// Configuring the Git access

	git config --global user.name satya
	git config --global user.email satyarocks1996@gmail.com
	
				// Check what commands are available

	git config --global --list
