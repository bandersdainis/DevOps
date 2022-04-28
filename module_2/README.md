## 13. Salīdzināt vienādu failu (ne README) hash no mapes module_1 un module_2. Vai git redz atšķirību starp šiem failiem?

```sh
git hash-object module_1\vumc.jpg
e77b60f177dfe0ff04fe9c5dabfb90e0bf0eae95
```

```sh
git hash-object module_2\vumc.jpg
e77b60f177dfe0ff04fe9c5dabfb90e0bf0eae95
```
### Failu hash ir vienādi. 

## 15. Mapē git_repos noklonēt https://github.com/hashicorp/terraform projektu.
```sh
git clone https://github.com/hashicorp/terraform
Cloning into 'terraform'...
remote: Enumerating objects: 258456, done.
remote: Counting objects: 100% (35/35), done.
remote: Compressing objects: 100% (25/25), done.
Receiving objects: 100% (258456/258456), 190.64 MiB | 556.00 KiB/s, done.

Resolving deltas: 100% (160472/160472), done.
Updating files: 100% (3058/3058), done.
```

## 16. Pārbaudīt kādas izmaiņas tika veiktas iepriekšējās nedēļas laikā. Atrast vismaz divus veidus kā to izdarīt.
```
git log --after="2022-04-18" --before="2022-04-24 23:59:59"
git log --since="2022-04-18" --until="2022-04-24 23:59:59"
```
## 17. Atrast commit kurus veica autors - “Laura Pacilio”
```
git log --author="Laura Pacilio"
```
## 18. Atrast vai Laura ir veikusi commit pagājušā gada septembrī?
```
git log --author="Laura Pacilio" --after="2021-09-01" --before="2021-09-30 23:59:59"
```
>Jā, Laura 2021.gada septembrī ir veikusi 11 commitus
## 19. Vai Laura ir veikusi commit vakar?
```
git log --author="Laura Pacilio" --after="yesterday" --before="today"
``` 
>Nē, Laura vakar (27.04.2022) nav veikusi commit

## * Atlasot rezultātus no pagājušā gada 20 līdz 21 aprīlim var atrast commit kurš ir datēts ar 16 aprīli? Kāpēc tā ir? Atbildi apkopot module_2 > README.md un pārsūtīt rezultātu Github.
```
git log --pretty=format:"%h %ad | %s %d [%an]"  --since="2021-04-20" --until="2021-04-21"
f8493bf5c Fri Apr 16 17:11:27 2021 -0400 | update hcl  [James Bardin]
d15f7394a Tue Apr 20 16:25:34 2021 -0400 | Merge pull request #28457 from hashicorp/jbardin/provisioner-null-checks  [James Bardin]
7f571b5eb Tue Apr 20 12:31:32 2021 -0400 | additional null checks in provisioners  [James Bardin]
fabdf0bea Tue Apr 20 10:05:45 2021 -0400 | Add config_paths and drop KUBECONFIG env variable in kubernetes backend (#26997)  [John Houston]
```
>Jā, ir viens commit, kas datēts ar 16. aprīli. 16\. aprīlī tika veiks commit lokālajā repozitorijā.
