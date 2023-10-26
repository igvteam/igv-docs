Calculates the concensus sequence for the region in view and copies the information to the clipboard. The method for
calculating the consensus is taken from Cavener, Nucleic Acids Res. 15, 1353-1361, 1987.

1. If the frequency of a single nucleotide at a specific position is greater than 50% and greater than twice the number
   of the second most frequent nucleotide it is assigned as the consensus nucleotide.

2. If the sum of the frequencies of two nucleotides is greater than 75% (but neither meet the criteria for a single
   nucleotide assignment) they are assigned as co-consensus nucleotides.

3. If no single nucleotide or pair of nucleotides meets the criteria, assign an 'N'.

