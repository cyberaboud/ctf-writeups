# Writeup Simplest

## Français

Après avoir analysé le fichier, nous pouvons voir qu'il s'agit d'un binaire ELF x64 non stripped, ce qui signifie que nous pouvons décompiler le binaire pour récupérer son pseudo-code :

![Pseudo-code après décompilation](images/image1.png)

Nous le décompilons avec Ghidra et nous découvrons l'appel à la fonction `are_equal`. Nous constatons que notre entrée est comparée à `FLAG` :

![Fonction are_equal et comparaison avec FLAG](images/image2.png)

Nous vérifions ce que contient `FLAG` et essayons de le soumettre, mais sans succès :

![Vérification du contenu de FLAG](images/fakeflag.png)

Nous déboguons le binaire avec GDB pour analyser notre binaire instruction par instruction. Nous désassemblons la fonction `main` et plaçons un point d'arrêt sur l'appel à la fonction `are_equal` :

![Point d'arrêt sur la fonction are_equal](images/image4.png)

Petit rappel sur les conventions d'appel en x64 : en assembleur, lors de l'appel d'une fonction utilisant des paramètres, le premier paramètre est placé dans le registre `rdi`, le deuxième paramètre dans `rsi`, et le troisième dans `rdx`. Dans notre cas, notre entrée sera dans le registre `rdi` :

![Registre rdi avec l'entrée](images/image5.png)

Nous exécutons le binaire avec une entrée arbitraire et atteignons le point d'arrêt. Nous pouvons voir le `FLAG` dans le registre `rsi` :

![FLAG dans le registre rsi](images/image6.png)

Et nous validons le challenge avec ce `FLAG`.

![Validation du challenge avec FLAG](images/flag.png)

## English

After analyzing the file, we can see that it's an x64 ELF binary that is not stripped, so we can decompile the binary to retrieve its pseudo-code:

![Pseudo-code after decompilation](images/image1.png)

We decompile it with Ghidra and discover the call to the `are_equal` function. We can see that our input is compared to `FLAG`:

![are_equal function and FLAG comparison](images/image2.png)

We verify what the `FLAG` holds and try to submit it, but no luck:

![Verifying FLAG content](images/image3.png)

We debug the binary with GDB to analyze our binary instruction by instruction. We disassemble the `main` function and set a breakpoint on the call to the `are_equal` function:

![Breakpoint on are_equal function](images/image4.png)

Quick reminder: in x64 calling conventions in assembly, when calling a function using parameters, the first parameter is stored in the `rdi` register, the second in `rsi`, and the third in `rdx`. In our case, our input is going to be in the `rdi` register:

![rdi register with input](images/image5.png)

We run the binary with arbitrary input and reach the breakpoint. We can see the `FLAG` in the `rsi` register:

![FLAG in rsi register](images/image6.png)

And we validate the challenge with that `FLAG`.

![Challenge validated with FLAG](images/flag.png)
