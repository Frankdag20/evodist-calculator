# evodist-calculator

There are two main commands/functions. The first one is grab_assemblies(). This function will traverse online directories and download the necessary protein annotation files from Refseq/Genbank. An example input is as follows:

grab_assemblies(list_of_species = 
                ['Saccharomyces cerevisiae',
                 'Saccharomyces mikatae',
                 'Naumovozyma castellii',
                 'Kluyveromyces lactis',
                 'Aspergillus nidulans',
                 'Saccharomyces kudriavzevii',
                 'Yarrowia lipolytica',
                 'Schizosaccharomyces pombe',
                 'Eremothecium gossypii',
                 'Saccharomyces paradoxus',
                 'Saccharomyces bayanus'],
                 override_dict = 
                 {'Saccharomyces mikatae' : ['Smik.faa' , 'target'],
                  'Saccharomyces bayanus' : ['Sbay.faa', 'target']})
                  
The list of species is all of the species of interest. It will perform the search using these species names. It will print out its progress, and alert the user if the annotation cannot be found online. However, if an annotation is not found, this may be due to a different naming convention for the same species. There is then an optional "override_dict" argument, where you place the species name, and then a list of a file name and whether the species is a "target" or "source". This argument is in case you would like to use a protein annotation FASTA file that cannot be fetched online. This should be placed into the absense_fasta_downloads directory made after running grab_assemblies() once. A source species is where the distances will be calculated relative to, although the ordering is not really important. This function could create a file of all the necessary protein annotation files to be used by the next function.

The second function is run_evo_dist_computation(). This function will perform the evolutionary distance computation. An example input is as follows:

run_evo_dist_computation(evalue = 0.01, acc_file = 'absense_accession_codes_infile.txt')

This is also the default input. The E-value specifies the E-value cutoff for a significant homolog search within HMMER, and for how orthologs are chosen. The acc_file is default the file generated by grab_assemblies(), and specifies the annotation files of interest to be used in the evolutionary distance computation. The result should be a file called "outfile" in a directory titled protdist_infile_outfile_\*, where the \* represents the source species accession identification for their FASTA file. The distances will be in the outfile, and can be passed into abSENSE.
