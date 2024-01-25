# CHECKSUMS

Ensuring file integrity when transferring data. Checksums act as a fingerprint that allow detection of errors that may occur when transferring data.

Generate checksum md5sum for single file:

    md5sum file > file.md5

OR Generate checksum md5sum for mulitple files of same type:

    md5sum *.fastq.gz > md5sums.txt

OR To generate MD5 checksums for all of the files in the current directory and all directories beneath it, type the following command:

    find . -type f -exec md5sum {} > md5sums.txt \;

After transferring data, verify checksums:

    md5sum -c file.md5
    
Each matching checksum displays OK, while a mismatched checksum displays FAILED. If FAILED, it indicates there may have been a disruption during file transfer, and that file should be transferred again. 
