# Shell script to list files in directory
Here I am capturing simple script to loop over the directory recursively and find a json file in it

```sh
#!/bin/bash  +x
#-----------------------------------------------------------------------------------
# Sub routine to copy the iar files into the workspace dir before running the tests
#-----------------------------------------------------------------------------------
copy_iar_to_workspace()
{
	if ls $1/*.iar 1> /dev/null 2>&1; then
		echo "Moving the iar into workspace dir"
		ls -1 $1/*.iar | xargs cp -t workspace-resources
	fi
}

#--------------------------------------------------------------
# Sub routine to run the tests inside the folder
# if it finds a subfolder then it will recursively calls itself
#--------------------------------------------------------------
run_collections_inside_the_folder()
{
  for f in $1;
  do
   if [ -d "$f" ]; then
        echo "Looking for collections in the folder $f"        
        copy_iar_to_workspace $f
        run_collections_inside_the_folder "$f/*"
   else
        if [[ $f == *".json"* ]]; then
           echo "    Running the collection $f"
        fi
   fi
  done
}



NEWMAN_COLLECTIONS=collections/$1/*
run_collections_inside_the_folder $NEWMAN_COLLECTIONS

```

This script uses lots of scripting feature which we see now
1. We can have subroutines, in shell scripts the subroutine should be declared and defined before its usage and the paramater can be accessed like $1, $2
2. The cp command in unix do not accept regex pattern as a part of it, hence we are using ls command and usings its output for copying the file
3. It also contains how to do a string comparison