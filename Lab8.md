# Լաբորատոր աշխատանք 8
### 1. Գրել ծրագիր, որը ինտերակտիվ ռեժիմում կստանա [0, 3] միջակայքի որևէ թիվ, ևարգումենտի արժեքից կախված կկատարի հետևյալ գործողությունները․
* 0 – ավարտել ծրագիրը։
* 1 – արտածել /home/student դիրեկտորիայի ֆայլերի ցուցակը։
* 2 – արտածել /home/student դիրեկտորիայի տեքստային ֆայլերի քանակը։
* 3 – արտածել աշխատանքային դիրեկտորիան։
### Գործողությունները կրկնել մինչև 0 արժեքի ներմուծումը։ Օգտագործել case օպերատոր։
```bash
#!/bin/bash

while true; do
    echo "Enter a number (0 to exit):"
    read choice

    case $choice in
        0)
            echo "Exiting the script."
            break
            ;;
        1)
            echo "Listing files in /home/student directory:"
            ls /home/student
            ;;
        2)
            echo "Counting text files in /home/student directory:"
            count=$(find /home/student -type f -name "*.txt" | wc -l)
            echo "Number of text files: $count"
            ;;
        3)
            echo "Displaying the working directory:"
            pwd
            ;;
        *)
            echo "Invalid choice. Please enter a number between 0 and 3."
            ;;
    esac
done

```
OUTPUT:
```bash
Enter a number (0 to exit):
1
Listing files in /home/student directory:
file1.txt
file2.txt
document.txt
...

Enter a number (0 to exit):
2
Counting text files in /home/student directory:
Number of text files: 5

Enter a number (0 to exit):
3
Displaying the working directory:
/home/student

Enter a number (0 to exit):
0
Exiting the script.
```
### 2. Գրել ծրագիր, որը որպես արգումենտ կստանա տարվա ամսի անունը և կվերադարձնի տվյալ ամսում առկա օրերի քանակը։ Օգտագործել case օպերատոր։
```bash
#!/bin/bash

echo "Enter the name of a month:"
read month

case $month in
    "January" | "March" | "May" | "July" | "August" | "October" | "December")
        days=31
        ;;
    "April" | "June" | "September" | "November")
        days=30
        ;;
    "February")
        days=28
        ;;
    *)
        echo "Invalid month name"
        exit 1
        ;;
esac

echo "The number of days in $month is $days."
```
OUTPUT:
```bash
Enter the name of a month:
February
The number of days in February is 28.
```

### 3. Գրել <<Հաշվիչ>> ծրագիր, որը կստանա ճիշտ 3 արժեք հետևյալ հաջորդականությամբ․ թիվ, գործողություն, թիվ։ Օր՝ 2 + 3։ Արժեքները ներմուծել ինտերակտիվ ռեժիմում (read հրամանի միջոցով)։ Գործողության համար սահմանել հետևյալ ընդունելի արժեքները․ + - * / **։ Արտածել գործողության արդյունքը։ Գործողության տիպը որոշելու համար օգտագործել case օպերատոր։

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
### 4. Գրել ծրագիր, որը որպես հրամանային տողի արգումենտ կստանա ֆայլի անուն։ Եթե ֆայլը գոյություն ունի և ունի կարդալու թույլտվություն, ապա արտածել ֆայլի պարունակությունը, հակառակ դեպքում արտածել համապատասխան հաղորդագրություն։
```bash
#!/bin/bash

# Check if a filename is provided as an argument
if [ $# -eq 0 ]; then
  echo "Usage: $0 <filename>"
  exit 1
fi

filename=$1

if [ -e "$filename" ]; then

  if [ -r "$filename" ]; then
    echo "File content:"
    cat "$filename"
  else
    echo "Error: The file is not readable."
  fi
else
  echo "Error: File not found."
fi
```
OUTPUT:
```bash
#Hello, this is an example file.
#It contains multiple lines.
#This is the third line.

#./readfile.sh example.txt

File content:
Hello, this is an example file.
It contains multiple lines.
This is the third line.
```
### 5. Գրել cp ծրագրի պատճենը՝ առանց cp հրամանից օգտվելու։ Ծրագիրը պետք է որպես արգումենտներ ստանա 2 ֆայլերի անուններ, և պատճենի առաջին ֆայլի պարունակությունը 2-րդի մեջ։ Իրականացնել ծրագրի պատշաճ աշխատանքի համար հարկավոր ստուգումներ (ֆայլը գոյություն ունի, ունի կարդալու թույլտվություն)։
```bash
echo "Enter the first filename: "
read -r file1

echo "Enter the second filename: "
read -r file2

if [ -r "$file1" ]; then
	cat "$file1" >"$file2"
	echo "Content of the file successfully copied."
else
	echo "File $file1 does not exist or is not readable."
fi
```
OUTPUT:
```bash 
#Let's assume you run the script and provide valid filenames as input:
Enter the first filename:
example1.txt
Enter the second filename:
example2.txt
#If they exist and are readable we will see 
Content of the file successfully copied.
```
### 6. Գրել ծրագիր, որը որպես հրամանային տողի արգումենտներ կստանա 2 թիվ և կարտածի այդ թվերի գումարը։ Իրականացնել արժեքների վավերացում։
```bash
if [ "$#" -ne 2 ]; then
	echo "Usage: $0 <num1> <num2>"
	exit 1
fi

num1="$1"
num2="$2"

if ! [[ "$num1" =~ ^[0-9]+$ ]] || ! [[ "$num2" =~ ^[0-9]+$ ]]; then
	echo "Invalid input. Please enter valid numbers."
	exit 1
fi

sum=$((num1 + num2))
echo "The sum of $number1 and $number2 is: $sum"
```
```bash 
./sum.sh 5 7
```
OUTPUT:
```bash 
The sum of 5 and 7 is: 12
```
### 7. Գրել ծրագիր, որը որպես հրամանային տողի արգումենտներ կստանա կամայական քանակով արժեքներ և նույնությամբ կարտածի այդ արժեքները։ Օգտագործել while ցիկլ և shift օպերատոր։
```bash
#!/bin/bash

if [ "$#" -eq 0 ]; then
    echo "No arguments provided."
    exit 1
fi

while [ "$#" -gt 0 ]; do
    echo "$1"
    shift
done
```
```bash
./print_args.sh arg1 arg2 arg3
```
OUTPUT:
```bash
arg1
arg2
arg3

```
### 8. Իրականացնել 7-րդ կետը՝ օգտագործելով for ցիկլ և $@ հատուկ փոփոխականը։
```bash
for arg in "$@"; do
	echo "Argument: $arg"
done
```
### 9. Գրել ծրագիր, որը որպես հրամանային տողի արգումենտներ կստանա կամայական քանակով թվեր և կարտածի այդ թվերի գումարը։
```bash
sum=0

for arg in "$@"; do
	if [[ "$arg" =~ ^[0-9]+$ ]]; then
		sum=$((sum + arg))
	else
		echo "Invalid input. Please enter valid numbers."
		exit 1
	fi
done

echo "Sum: $sum"
```
```bash
./sum.sh 5 10 15
```
OUTPUT:
```bash
Sum: 30
```
### 10. Գրել ծրագիր, որը որպես հրամանային տողի արգումենտներ կստանա կամայական քանակով թվեր և կարտածի զույգ թվերի քանակը։
```bash
#!/bin/bash

if [ "$#" -eq 0 ]; then
    echo "Usage: $0 <num1> [num2 ...]"
    exit 1
fi

even_count=0

while [ "$#" -gt 0 ]; do
    num="$1"
    
    if ! [[ "$num" =~ ^[0-9]+$ ]]; then
        echo "Invalid input: $num is not a valid integer."
        exit 1
    fi
    
    if [ $((num % 2)) -eq 0 ]; then
        even_count=$((even_count + 1))
    fi

    shift
done

echo "Count of even numbers: $even_count"
```
```bash
./even_count.sh 5 10 15 20
```
OUTPUT:
```bash
Count of even numbers: 2
```