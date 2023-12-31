# Լաբորատոր աշխատանք 4

### 1. Ստեղծել նոր ֆայլ՝ file.txt, և դրա համար սահմանել հետևյալ իրավունքները․ - rwx r-- r--

```bash
touch file.txt
chmod 744 file.txt
```
Ֆայլի ռեժիմը փոփոխելու համար օգտագործվում է `chmod` հրամանը

`7` = `rwx`

`4` = `r--`

### 2. Փոփոխել file.txt ֆայլի իրավունքները՝ բոլոր օգտատերերի համար ավելացնելով կատարելու իրավունք։ Օգտվել ֆայլի ռեժիմների սիմվոլիկ ներկայացումից։

```bash
chmod a+x file.txt
```

### 3. Փոփոխել file.txt ֆայլի իրավունքները՝ խմբի օգտատերերի և այլ օգտատերերի համար հեռացնելով կատարելու իրավունքը։ Օգտվել սիմվոլիկ ներկայացումից։

```bash
chmod go-x file.txt
```

`g` `(Group)` – Խմբին պատկանող օգտատերեր

`o` `(Other)` – Մնացած օգտատերեր

`-x` - հեռացնում է կատարելու իրավունքը

### 4. Փոփոխել file.txt ֆայլի իրավունքները՝ հեռացնելով բոլոր իրավունքները, և սահմանելով գրելու և կարդալու իրավունքներ միայն ֆայլի սեփականատիրոջ համար։ Նույն գործողությունը կատարել 2 անգամ ՝ օգտվելով ֆայլի ռեժիմների 8-ական և սիմվոլիկ ներկայացումներից։

```bash
chmod 600 file.txt
```
`0` = `---`

`6` = `rw-`

### 5.Ստեղծել նոր դիրեկտորիա՝ dir: Սահմանել հետևյալ իրավունքները․ d rw- rw- rw-։ dir դիրեկտորիայում ստեղծել նոր ֆայլ՝ file.txt։ Բացատրել ստացված հաղորդագրությունը։ Փոփոխել դիրեկտորիայի իրավունքներն այնպես, որ ֆայլը հաջողությամբ ստեղծվի։

```bash
mkdir -m 666 dir
cd dir
touch file.txt
```

### 6. dir դիրեկտորիայում ստեղծել ևս 2 ֆայլ՝ file1.txt, file2.txt։ Մեկ հրամանի կատարմամբ փոփոխել դիրեկտորիայի բոլոր ֆայլերի իրավունքները՝ սահմանելով - rwx rw- rw-։

```bash
touch dir/file1.txt dir/file2.txt
chmod 766 dir/*
```
### 7. umask հրամանի միջոցով սահմանել այնպիսի bitmask, որ նոր ստեղծվող ֆայլերը լռելյայն կերպով ունենան հետևյալ իրավունքները․ - rw- r-- ---

`umask` հրամանը ղեկավարում է ֆայլի ստեղծման պահին տրվող իրավունքները։ Հրամանի կատարման արդյունքում ցուցադրվում է `8`-ական `bitmask (0022)`, որը սահմանում է այն
իրավունքները, որոնք պետք է հեռացվեն ֆայլից։

```bash
umask 027
```

### 8.umask հրամանի միջոցով սահմանել այնպիսի bitmask, որ նոր ստեղծվող ֆայլերը լռելյայն կերպով ունենան հետևյալ իրավունքները․ - rw- --- ---: Վերադարձնել bitmask-ի լռելյայն արժեքը՝ կատարելով umask 0022 հրամանը։

```bash
umask 077
umask 022
```
 
### 9. Ստեղծել սկրիպտ, որը կարտածի /home/student դիրեկտորիայի ֆայլերի ցուցակը։ Սկրիպտի համար սահմանել - -wx r-- r-- իրավունքները։ Կատարել սկրիպտը և բացատրել ստացված հաղորդագրությունը։ Փոփոխել իրավունքներն այնպես, որ սկրիպտը կատարվի։

```bash
echo 'ls /home/student' > script.sh
chmod 741 script.sh
chmod +x script.sh
./script.sh
```

### 10. Սկրիպտը տեղադրել ~/bin դիրեկտորիայում։ Փոփոխել $PATH փոփոխականն այնպես, որ սկրիպտը հնարավոր լինի կատարել առանց հասցեն նշելու։

```bash
mkdir ~/bin
mv script.sh ~/bin
echo 'export PATH=$PATH:~/bin' >> ~/.bashrc
source ~/.bashrc
```
