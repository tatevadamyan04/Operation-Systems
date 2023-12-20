# Լաբորատոր աշխատանք 6

### 1. Գրել սկրիպտ, որը տրված թվի համար կարտածի հաղորդագրություն այն մասին, արդյոք թիվը դրական է, բացասական, թե՝ 0։ Թիվը վավերացնել ռեգուլյար արտահայտության միջոցով։ Պայմանների ստուգման համար օգտագործել [[ ]] օպերատորը։

```bash
#!/bin/bash

check_number() {
    if [[ $1 =~ ^[+-]?[0-9]*\.?[0-9]+$ ]]; then
        if [ "$1" -gt 0 ]; then
            echo "$1 is a positive number."
        elif [ "$1" -lt 0 ]; then
            echo "$1 is a negative number."
        else
            echo "$1 is zero."
        fi
    else
        echo "Invalid input. Please enter a valid number."
    fi
}

check_number -3.14
```
OUTPUT:
```bash
-3.14 is a negative number.
```

### 2.Կատարել 1-ին կետը՝ պայմանների ստուգման համար օգտագործելով (( )) օպերատորը։

```bash
#!/bin/bash

check_number() {
    if (( $1 > 0 )); then
        echo "$1 is a positive number."
    elif (( $1 < 0 )); then
        echo "$1 is a negative number."
    else
        echo "$1 is zero."
    fi
}

check_number -3.14
```

### 3. Գրել սկրիպտ, որը կստուգի, թե արդյոք տրված թիվը 2-ի, 3-ի `և` 5-ի բազմապատիկ է:

```bash 
#!/bin/bash

check_multiples() {
    if (( $1 % 2 == 0 && $1 % 3 == 0 && $1 % 5 == 0 )); then
        echo "$1 is a multiple of 2, 3, and 5."
    else
        echo "$1 is not a multiple of 2, 3, and 5."
    fi
}

check_multiples 30

```
OUTPUT:
```bash 
30 is a multiple of 2, 3, and 5.
```

### 4. Գրել սկրիպտ, որը կստուգի, թե արդյոք տրված թիվը 2-ի, 3-ի `կամ` 5-ի բազմապատիկ է:

```bash
#!/bin/bash

check_multiples() {
    if (( $1 % 2 == 0 || $1 % 3 == 0 || $1 % 5 == 0 )); then
        echo "$1 is a multiple of 2, 3, or 5."
    else
        echo "$1 is not a multiple of 2, 3, or 5."
    fi
}

check_multiples 30
```

### 5. Մեկ հրամանի միջոցով ստեղծել նոր ֆայլ և այդ ֆայլին ավելացնել կատարելու թույլտվություն։

```bash
echo "This is a test file." > new_file.txt && chmod +x new_file.txt
```

### 6. Մեկ հրամանի միջոցով ստուգել, թե արդյոք գոյություն ունի dir անունով դիրեկտորիա, և, եթե գոյություն չունի, ապա ստեղծել։

```bash
[ -d dir ] || mkdir dir
```

### 7. Գրել սկրիպտ, որը կստուգի, թե արդյոք տրված թիվը գտնվում է սահմանված միջակայքում։ Ստուգվող թիվը և միջակայքի սահմանների թվերը ներմուծել read հրամանի միջոցով։ Իրականացնել տվյալների վավերացում։

```bash
#!/bin/bash

read -p "Enter a number: " number

read -p "Enter the lower bound of the range: " lower_bound
read -p "Enter the upper bound of the range: " upper_bound

if [ "$number" -ge "$lower_bound" ] && [ "$number" -le "$upper_bound" ]; then
    echo "The number $number is within the specified range [$lower_bound, $upper_bound]."
else
    echo "The number $number is outside the specified range [$lower_bound, $upper_bound]."
fi

```
OUTPUT:
```bash
Enter a number: 56
Enter the lower bound of the range: 50
Enter the upper bound of the range: 100
The number 56 is within the specified range [50, 100].
```

### 8. Գրել սկրիպտ, որը որպես ներմուծվող արժեք կստանա մեկ բառ, և կստուգի արդյոք այն համընկնում է "Secret" բառի հետ։ read հրամանը կատարել այնպես, որ ներմուծված արժեք պահպանվի REPLY փոփոխականի մեջ, իսկ ներմուծումն իրականացնելիս տառերը չցուցադրվեն էկրանին։

```bash
#!/bin/bash

read -s -p "Enter a word: " REPLY
echo

if [ "$REPLY" = "Secret" ]; then
    echo "You entered the secret word!"
else
    echo "The entered word is not the secret word."
fi

```
OUTPUT:
```bash
# REPLY = SECRETE
The entered word is not the secret word.
```
### 9. Գրել սկրիպտ, որը որպես ներմուծվող արժեք կստանա ֆայլի անուն։ Վավերացնել անունը հետևյալ կանոններով․ կարող է պարունակել տառեր, թվեր, - . _ սիմվոլները։ Եթե նման ֆայլ գոյություն չունի, ապա ստեղծել։ Ցուցադրել համապատասխան հաղորդագրություն ֆայլի ստեղծման կամ առկայության մասին։

```bash
#!/bin/bash

read -p "Enter a file name: " fileName

pattern='^[a-zA-Z0-9_.-]+$'

if [[ $fileName =~ $pattern ]]; then
    echo "The entered file name is valid."
    if [ -e "$fileName" ]; then
        echo "The file \"$fileName\" already exists."
    else
        touch "$fileName"
        echo "The file \"$fileName\" has been created."
    fi
else
    echo "Invalid file name. File names can only contain letters, numbers, hyphen, underscore, and dot."
fi

```

OUTPUT:
```bash
Enter a file name: hello_world
The entered file name is valid.
The file "hello_world" has been created.
```

### 10. Գրել <<Հաշվիչ>> ծրագիր, որը կստանա ճիշտ 3 արժեք հետևյալ հաջորդականությամբ․ թիվ, գործողություն, թիվ։ Օր՝ 2 + 3։ Ստուգել ներմուծված արժեքների քանակը, և 3-ից տարբեր լինելու դեպքում արտածել հաղորդագրություն սխալի մասին։ Իրականացնել արժեքների վավերացում։ Գործողության համար սահմանել հետևյալ ընդունելի արժեքները․ + - * / **։ Արտածել գործողության արդյունքը։

```bash
#!/bin/bash

calculator() {
    case $2 in
        "+") echo $(($1 + $3));;
        "-") echo $(($1 - $3));;
        "*") echo $(($1 * $3));;
        "/") 
            if [ $3 -ne 0 ]; then
                echo $(($1 / $3))
            else
                echo "Error: Division by zero"
            fi;;
        "**") echo $(($1 ** $3));;
        *) echo "Error: Invalid operator";;
    esac
}

read -p "Enter the first number: " num1
read -p "Enter the operator (+, -, *, /, **): " operator
read -p "Enter the second number: " num2

if [[ "$operator" =~ ^[+\-*/**]$ ]]; then
    result=$(calculator $num1 "$operator" $num2)
    echo "Result: $result"
else
    echo "Error: Invalid operator"
fi

```
OUTPUT:
```bash
Enter the first number: 5
Enter the operator (+, -, *, /, **): **
Enter the second number: 3
Result: 125

```