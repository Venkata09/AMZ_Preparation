# For permutations, it's always go with the recursion, swapping of the elements with in the string/array. 

Formula for calculatin the permutations is 

you will take two variables. 
(outputString, inputString) ==> You swap the characters from input->output. ==> You can input is empty. ==> if it's empty add/print the result. 

Recusion applied to the same logic but changing the SWAP elements. 

### Formula ==> permutation( inputString.charAt(i) + outputString, inputString.subString(0, i) + inputString(i+1, endOfLenght) )
