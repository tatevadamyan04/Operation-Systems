# Լաբորատոր աշխատանք 5

### 1. Ստեղծել կամայական արժեքով փոփոխական՝ str: Ցուցադրել հետևյալ հրամանների աշխատանքի արդյունքի տարբերությունը. echo$str2 և  echo ${str}2։

```bash
str="HelloWorld"
echo str2         
echo ${str}2      
```
OUTPUT:
```bash
str2
HelloWorld2
```

### 2. Արտածել հետևյալ արտահայտության արժեքը․ 5<sup>2</sup> * 4/10
```bash
echo $((5 ** 2 * 4 / 10))
```

### 3. Ցուցադրել հետևյալ հրամանների աշխատանքի արդյունքի տարբերությունը․echo "The balance for user $USER is: $5.00" և  echo "The balance for user $USER is: \$5.00"

```bash
echo "The balance for user $USER is: $5,00" 
# The balance for user root is: ,00
echo "The balance for user $USER: \$5,00"  
# The balance for user root: $5,00
```

### 4. Ցուցադրել հետևյալ հրամանների աշխատանքի արդյունքի տարբերությունը․ echo '$USER $((2 + 2)) $(ls)' և echo "$USER $((2 + 2)) $(ls)"

```bash
echo '$USER $((2 + 2)) $(ls)' 
# $USER $((2 + 2)) $(ls)
echo "$USER $((2 + 2)) $(ls)" 
# root 4 labs main.sh
```

### 5. Առանձին տողերում արտածել ընթացիկ դիրեկտորիան և այնտեղ առկա տեքստային ֆայլերի քանակը։ Օգտագործել Here document:

```bash
current_dir=$(pwd)
num_files=$(ls -l | grep -c "^-")
cat <<EOF
Current directory: $current_dir
Number of files: $num_files
EOF
```

### 6. Գրել 2 թվեր գումարող ֆունկցիա։ Թվերը ֆունկցիային փոխանցել որպես արգումենտներ։

```bash
#!/bin/bash
add_numbers() {
    local result=$(( $1 + $2 ))
    echo "The sum of $1 and $2 is: $result"
}

add_numbers 5 7
```
OUTPUT:
```bash
12
```

### 7. Գրել ֆունկցիա, որը որպես արգումենտ կստանա դիրեկտորիայի անվանումը և կարտածի այնտեղ առկա ֆայլերի քանակը։

```bash
#!/bin/bash

count_files() {
    local directory="$1"
    local file_count=$(find "$directory" -type f | wc -l)
    
    echo "The number of files in '$directory' is: $file_count"
}

count_files "/path/to/directory"
```
 For example, if you run the script with the directory `"/path/to/directory"` and there are `10` files in that directory, the output would be:
 ```bash
 The number of files in '/path/to/directory' is: 10
 ```

 ### 8. Գրել սկրիպտ, որում նոր ստեղծված ֆայլի համար ստուգել, թե արդյոք այն ունի կարդալու / գրելու / կատարելու թույլտվություն, և արտածել համապատասխան հաղորդագրություն։

 ```bash
 #!/bin/bash

filename="testfile.txt"

# Ստեղծում ենք նոր ֆայլ
touch "$filename"

# Ստուգենք արդյոք այդ ֆայլը գոյություն ունի թե ոչ
if [ -e "$filename" ]; then
    # Ստուգենք կարդալու կարողությունը
    if [ -r "$filename" ]; then
        echo "The file has read permission."
    else
        echo "The file does not have read permission."
    fi

    # Ստուգենք գրելու կարողությունը
    if [ -w "$filename" ]; then
        echo "The file has write permission."
    else
        echo "The file does not have write permission."
    fi

    # Ստուգենք արտածելու կարողությունը
    if [ -x "$filename" ]; then
        echo "The file has execute permission."
    else
        echo "The file does not have execute permission."
    fi
else
    echo "The file does not exist."
fi
 ```

### 9. Գրել սկրիպտ, որը կորոշի տրված 2 թվերից մեծագույնը և կարտածի։

```bash
#!/bin/bash

find_maximum() {
    if [ "$1" -gt "$2" ]; then
        echo "$1 is greater than $2"
    elif [ "$1" -lt "$2" ]; then
        echo "$2 is greater than $1"
    else
        echo "Both numbers are equal"
    fi
}

find_maximum 8 5
```
OUTPUT:
```bash
8 is greater than 5
```

### 10. Գրել սկրիպտ, որը կորոշի տրված թիվը զույգ է, թե կենտ։ Արտածել համապատասխան հաղորդագրություն։

```bash
#!/bin/bash

check_even_odd() {
    if [ $(( $1 % 2 )) -eq 0 ]; then
        echo "$1 is an even number."
    else
        echo "$1 is an odd number."
    fi
}

check_even_odd 7
check_even_odd 6
```
OUTPUT:
```bash
7 is an odd number.
6 is an even number.
```

