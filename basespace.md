# Illumina BaseSpace Command line interface

## To install

Make directory:
```
mkdir -p $HOME/bin
```

Get the program
```
wget "https://launch.basespace.illumina.com/CLI/latest/amd64-linux/bs" -O $HOME/bin/bs
```

Change permissions on the program so you can run it:
```
chmod u+x $HOME/bin/bs
```

Authenticate:
```
$HOME/bin/bs auth
```
Then follow the link provided to authenticate.

## To download data 

This runs like doing `scp` to transfer data between your local computer and NeSI, in that the download runs on your command line. I recommend that before you start, you check your computer settings to make sure it doesn't turn off/go to sleep while your files are transferring (it's not fast like Globus). 

In your web browser on the Illumina link that you receive:
Go to BaseSpace > Project > Samples
Copy Project ID from the web address (the number following `projects/`). We'll then use that on the command line to get the data. Make sure you have created your out directory.
    
    $HOME/bin/bs download project -i=[PROJECT ID] -o=[OUTDIR] --extension=fastq.gz

An alternative method to get the fastq data is to use the BioSample or Project name (here BioSample is `AG1050-001`, project name is `AG1149_revised`):
    
    $HOME/bin/bs download biosample --name AG1050-001
OR
    $HOME/bin/bs download project --name AG1149_revised --extension=fastq.gz -o [OUTDIR]

To get all associated data and QC info (which you may or may not want to archive): 
    
    $HOME/bin/bs download run --name AG1050 
