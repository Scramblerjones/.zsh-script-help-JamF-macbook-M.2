# .zsh-script-help-JamF-macbook-M.2
#Trying to create a script that would allow me to remove apps with an attached policy. Running into errors and need help.
# The error I am getting says 

“Removing application: “““””””

jdoodle.sh: line 62: syntax error near unexpected token `done'
jdoodle.sh: line 62: `done '
Command exited with non-zero status 2
# Below I have have the script that is trying to be ran


#!/bin/bash


# Inputted variables
Keynote=“$4”

function silent_app_quit(){
    # silently kill the application.
    Keynote=“$1”
    if [[ $(pgrep -ix “$Keynote”) ]]; then
    	echo “Closing Keynote”
    	/usr/bin/osascript -e “quit app \”$Keynote\””
    	sleep 1

    	# double-check
    	countUp=0
    	while [[ $countUp -le 10 ]]; do
    		if [[ -z $(pgrep -ix “$Keynote”) ]]; then
    			echo “$Keynote closed.”
    			break
    		else
    			let countUp=$countUp+1
    			sleep 1
    		fi
    	done
        if [[ $(pgrep -x “$Keynote”) ]]; then
    	    echo “$Keynote failed to quit - killing.”
    	    /usr/bin/pkill “$Keynote”
        fi
    fi
}

if [[ -z “${Applications/Keynote.app}” ]]; then
    echo “Application Path not specified; exiting”
    exit 1
fi

# quit the app if running
silent_app_quit “$Keynote”

# Now remove the app
echo “Removing application: ${Keynote}”

# Add .app to end when providing just a name e.g. “TeamViewer”
if [[ ! $Keynote == *”.app”* ]]; then
	appName=$Keynote.app
fi

# Add standard path if none provided
if [[ ! $Keynote == *”/“* ]]; then
	appToDelete=“/Applications/$Keynote.app”
else
	appToDelete=“$Keynote”
if

# Remove the application
rm -rf “/Applications/${Keynote.app}”

echo “Removed /Applications/${Keynote.app}.”


done 
![help](https://user-images.githubusercontent.com/89668211/177645922-2c849015-2fb2-4088-9073-569e7d5bc753.jpg)
