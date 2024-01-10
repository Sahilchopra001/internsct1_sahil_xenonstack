Steps to do the Tasks : 

Step 1 :
Install Linux

Step 2 :
Firstly we have to create some files with specifix names as given in the Task List

***************** Section A Start **********************

Step 3 :
Create File named "internsct1.sh"

Step 4 :
Code for the file and name the version as given, specify the help command 

Step 5 : (Defining functions for version and help command)
The code for step 4 is given below :

VERSION="v0.1.0"
show_help() {
    echo "Usage: internsct1 [options]"
    echo "Options:"
    echo "  --help     Display help and usage information"
    echo "  --version  Display the version of internsct1"
}
case "$1" in
    --help)
        show_help
        ;;
    --version)
        echo "internsct1 $VERSION"
        ;;
    *)
        echo "Error: Unknown option. Use 'internsct1 --help' for usage information."
        exit 1
        ;;
esac

Step 6 : (Adding Manual page)
.TH internsct1 1 "January 10, 2024"
.SH NAME
internsct1 \- custom command with custom version
.SH SYNOPSIS
.B internsct1
[\fIOPTION\fR]
.SH DESCRIPTION
This manual page documents the internsct1 command.
.SH OPTIONS
.TP
.B \-\-help
Display help and usage information.
.TP
.B \-\-version
Display the version of customcmd.
.SH EXAMPLES
.PP
To display help:
.BR internsct1 --help
.PP
To display the version:
.BR internsct1 --version
.SH AUTHOR
Written by sahil.chopra025@gmail.com.
.SH COPYRIGHT
copyright by sahilchopra

Step 7 : (Making new files executable)
chmod +x internsct1.sh

Step 8 : (Adding files to the appropriate library)
sudo mv internsct1.sh /usr/local/bin/internsct1
sudo mv internsct1.1 /usr/share/man/man1/internsct1.1
Finally Update the manual page index by "sudo mandb"

Step 9 :
Now, anyone can run internsct1, internsct1 --help, and internsct1 --version, and view the manual page with man internsct1.

*************** Section A finish ****************

*************** Section B Start *******************

Step 10 :
Open the internsct1.sh file by "nano internsct1.sh"

Step 11 :
Edit the code and update as : 

VERSION="v0.1.0"
show_help() {
    echo "Usage: internsctl [command] [options]"
    echo "Commands:"
    echo "  cpu         Get CPU information"
    echo "  memory      Get memory information"
    echo ""
    echo "Options:"
    echo "  --help      Display help and usage information"
    echo "  --version   Display the version of internsctl"
}
get_cpu_info() {
    lscpu
}
get_memory_info() {
    free -h
}
case "$1" in
    cpu)
        get_cpu_info
        ;;
    memory)
        get_memory_info
        ;;
    --help)
        show_help
        ;;
    --version)
        echo "internsctl $VERSION"
        ;;
    *)
        echo "Error: Unknown command or option. Use 'internsctl --help' for usage information."
        exit 1
        ;;
esac

Step 12 : 
Now anyone can run the following commands : 
internsctl cpu getinfo  (It will provide CPU information similar to the output of lscpu)
internsctl memory getinfo   (It will provide memory information similar to the output of free )


*************** Section B Finish *****************


************** Section C start **************

Step 13 : 
Update the internsct1.sh file by below code :

VERSION="v0.1.0"
show_help() {
    echo "Usage: internsctl [command] [options]"
    echo "Commands:"
    echo "  cpu         Get CPU information"
    echo "  memory      Get memory information"
    echo "  user        User management commands"
    echo ""
    echo "Options:"
    echo "  --help      Display help and usage information"
    echo "  --version   Display the version of internsctl"
    # Add more options and descriptions as needed
}
create_user() {
    if [ -z "$2" ]; then
        echo "Error: Please provide a username. Usage: internsctl user create <username>"
        exit 1
    fi
    sudo useradd -m "$2"
    echo "User '$2' created successfully."
}
list_users() {
    cut -d: -f1 /etc/passwd
}
list_sudo_users() {
    grep -Po '^sudo.+:\K.*$' /etc/group | tr ',' '\n'
}
case "$1" in
    cpu)
        # Existing CPU command
        ;;
    memory)
        # Existing memory command
        ;;
    user)
        shift
        subcommand="$1"
        case "$subcommand" in
            create)
                shift
                create_user "$@"
                ;;
            list)
                shift
                if [ "$1" == "--sudo-only" ]; then
                    list_sudo_users
                else
                    list_users
                fi
                ;;
            *)
                echo "Error: Unknown 'user' subcommand. Use 'internsctl user --help' for usage information."
                exit 1
                ;;
        esac
        ;;
    --help)
        show_help
        ;;
    --version)
        echo "internsctl $VERSION"
        ;;
    *)
        echo "Error: Unknown command or option. Use 'internsctl --help' for usage information."
        exit 1
        ;;
esac



Step 14 : 
Now you can run following commands too : 
# Create a new user
internsctl user create <username>

# List all regular users
internsctl user list

# List users with sudo permissions
internsctl user list --sudo-only



Proof screenshots are attached in the github repo Thanks !



************** End ****************
