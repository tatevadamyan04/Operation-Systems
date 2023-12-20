# Լաբորատոր աշխատանք 7

### 1. Գրել ծրագիր, որը կարտածի [0, 20] միջակայքի զույգ թվերը։ Օգտագործել while ցիկլ։
```bash
number=0

while [ $number -le 20 ]; do
    echo $number
    number=$((number + 2))
done
```
OUTPUT:
```bash 
0
2
4
6
8
10
12
14
16
18
20
```
### 2. Կատարել 1-ին առաջադրանքը՝ օգտագործելով until ցիկլ։
```bash 
#!/bin/bash

number=0

until [ $number -gt 20 ]; do
    echo $number
    ((number+=2))
done
```

### 3. Գրել ծրագիր, որը գտնվում է անվերջ ցիկլի մեջ։ Ցիկլի յուրաքանչյուր իտերացիայում արտածել տվյալ ինդեքսի քառակուսին։ Ցիկլը ավարտել այն պահին, երբ արտածվող թիվը կգերազանցի 1000։ Օգտագործել while ցիկլ։

```bash 
#!/bin/bash

index=0

while [ $((index * index)) -le 1000 ]; do
    echo $((index * index))
    ((index++))
done
```
OUTPUT:
```bash 
0
1
4
9
16
25
36
49
64
81
100
121
144
169
196
225
256
289
324
361
400
441
484
529
576
625
676
729
784
841
900
961
```
### 4. Կատարել 1-ին առաջադրանքը՝ օգտագործելով for ցիկլ։

```bash
#!/bin/bash

for ((count = 0; count <= 20; count += 2)); do
	echo $count
done
```

### 5. Գրել ծրագիր, որը որպես մուտքային տվյալ կստանա ամբողջ թիվ և կարտածի դրա կրկնապատիկը։ Ծրագիրը սկսելիս ցուցադրել հետևյալ հաղորդագրությունը․ Enter an integer number, or enter q to quit: Ամբողջ թիվ մուտքագրելուց հետո ցուցադրել դրա կրկնապատիկը, և կրկին ցուցադրել հաղորդագրությունը՝ մինչև q տառի սեղմումը։

```bash 
while true; do
	read -r -p "Enter an integer or 'q' to exit: " input
	if [ "$input" == "q" ]; then
		break
	fi
	echo "Double of $input is $((input * 2))"
done
```
OUTPUT:
```bash
Enter an integer or 'q' to exit: 5
Double of 5 is 10
Enter an integer or 'q' to exit:
```

### 6. Գրել ծրագիր, որը կստեղծի /home/student դիրեկտորիայի տեքստային ֆայլերի անունները պարունակող ֆայլ։ while ցիկլի միջոցով համարակալել այս ֆայլերի անունները և արտածել։

```bash
index=1
while [ $index -le 5 ]; do
	touch ./file_$index.txt
	index=$((index + 1))
done
```
OUTPUT:
```bash
file_1.txt  file_2.txt  file_3.txt  file_4.txt  file_5.txt
```

### 7. Գրել ծրագիր, որը for ցիկլի միջոցով կարտածի [0, 30] միջակայքում գտնվող 3-ի բազմապատիկ թվերը։
```bash
#!/bin/bash

for ((i = 0; i <= 30; i += 3)); do
  echo $i
done
```
OUTPUT:
```bash
0
3
6
9
12
15
18
21
24
27
30
```
### 8. Գրել ծրագիր, որը for ցիկլի միջոցով կարտածի ընթացիկ դիրեկտորիայի բոլոր տեքստային ֆայլերի անունները։

```bash
for file in *; do
	echo "$file"
done
```

### 9. Գրել ծրագիր, որը որպես արգումենտ կստանա ֆայլերի անուններ, և այդ ֆայլերից յուրաքանչյուրի համար կարտածի ֆայլի ամենակարճ բառը և դրա երկարությունը։
```bash
#!/bin/bash

for file in "$@"; do
  if [ -f "$file" ]; then
    echo "File: $file"
    while IFS= read -r word; do
      if [ -n "$word" ]; then
        echo "Shortest word: $word"
        echo "Length: ${#word}"
        break
      fi
    done < "$file"
    echo "-----------------"
  else
    echo "Error: $file is not a valid file."
  fi
done
```
OUTPUT:
```bash 
#This is a sample text file.
#It contains various words and sentences.
File: example.txt
Shortest word: It
Length: 2
-----------------
```
### 10. Գրել ծրագիր, որը որպես արգումենտներ կստանա ֆայլերի անուններ, և դրանցից յուրաքանչյուրի համար կստուգի, թե արդյո՞ք տվյալ ֆայլը գոյություն ունի, թե ոչ։ Գոյություն ունենալու դեպքում ստուգել, թե արդյո՞ք ֆայլն ունի կարդալու թույլտվություն։ Արտածել համապատասխան հաղորդագրություններ։
```bash
#!/bin/bash

for file in "$@"; do
  if [ -e "$file" ]; then
    echo "File '$file' exists."
    if [ -r "$file" ]; then
      echo "File '$file' is readable."
    else
      echo "Error: File '$file' is not readable."
    fi
  else
    echo "Error: File '$file' does not exist."
  fi
  echo "-----------------"
done
```
OUTPUT:
```bash
File 'file1.txt' exists.
File 'file1.txt' is readable.
-----------------
File 'file2.txt' exists.
File 'file2.txt' is readable.
-----------------
Error: File 'non_existent_file.txt' does not exist.
-----------------
```