# unix/text-processing.md

## Recursively search for a string in a directory tree
    grep -R "password" "directory_path"

## Filter CSV rows and extract a specific field
    cat world-cities.csv | grep Germany | cut -d ',' -f1 > german_cities.txt

## Create a numeric sequence wordlist (1..1000)
    for i in $(seq 1 1000); do echo $i >> ids.txt; done

## Temporarily change name & hostname

    PS1='nullvoid@nullvoidlabs:\w\$ '
