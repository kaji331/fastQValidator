# FastQValidator
Contents [hide] 
1	fastQValidator Overview
1.1	Where to find it
1.1.1	Releases
1.1.2	Full Release (includes libStatGen)
1.1.3	Release of just fastQValidator (does not include libStatGen)
1.1.4	Using github
1.1.4.1	Using Git To Track the Current Development Version
1.1.4.1.1	Clone (get your own copy)
1.1.4.1.2	Get the latest Updates (update your copy)
1.1.5	Git Refresher
1.1.5.1	Downloading From GitHub Without Git
1.2	Building
1.3	Valid FastQ File Requirements
1.4	How to Use the fastQValidator Executable
1.4.1	Required Parameters
1.4.2	Optional Parameters
1.4.3	Optional Space Options for Raw Sequence (Last one specified is used)
1.4.4	Usage
1.4.5	Examples
1.4.6	Return Value
1.5	FastQ Validator Output
1.6	Libraries & Classes
1.7	Additional Features
1.8	Additional Wishlist - Not Implemented
1.9	Discussion
fastQValidator Overview

The fastQValidator validates the format of fastq files.
The initial version of a FASTQ Validator is complete. It was built using LibStatGen: FASTQ which is part of the libStatGen library.
Note: Since the FastQValidator checks for unique sequence names, it may use a large amount of memory - this can be disabled by specifying the --disableSeqIDCheck option
Where to find it

This command line tool can be obtained via:
Release Download
github: https://github.com/statgen/fastQValidator
Current development version
Available for download or using git.
Requires C++ Library: libStatGen, available at: https://github.com/statgen/libStatGen
Releases
If you prefer to run the last official release rather than the latest development version, you can download that here.
There are two versions of the release, one that include libStatGen and one that does not. If you already have libStatGen installed and want to use your own copy, use the version that does not include libStatGen.
Full Release (includes libStatGen)
To install an official release, unpack the downloaded file (tar xvf), cd into the fastQValidator_x.x.x directory and type make all.

fastQValidatorLibStatGen.0.1.1a.tgz‎ - Released 11/13/2012
fastQValidatorLibStatGen.0.1.1a Release Notes
Contains: libStatGen version 1.0.5 (update for this version)
Contains: fastQValidator version 0.1.1 (same as full release 0.1.1)
Older Releases
fastQValidatorLibStatGen.0.1.1.tgz‎ - Released 10/19/2012
Contains: libStatGen version 1.0.3
Contains: fastQValidator version 0.1.1
Validates a fastq file with options to print additional information.
Release of just fastQValidator (does not include libStatGen)
To install an official release, unpack the downloaded file (tar xvf), cd into the fastQValidator_x.x.x directory and type make all.
‎fastQValidator.0.1.1.tgz - Released 10/19/2012
fastQValidator.0.1.1 Release Notes
Validates a fastq file with options to print additional information.
Adds option to output average qualities

Older Releases
fastQValidator.0.0.1.tgz
Validates a fastq file with options to print additional information.
Using github
Using Git To Track the Current Development Version
Clone (get your own copy)
You can create your own git clone (copy) using:
git clone https://github.com/statgen/fastQValidator.git
or
git clone git://github.com/statgen/fastQValidator.git
Either of these commands create a directory called fastQValidator in the current directory.
Then just cd fastQValidator and compile.
Get the latest Updates (update your copy)
To update your copy to the latest version (a major advantage of using git):
cd pathToYourCopy/fastQValidator
make clean
git pull
make all
Git Refresher
If you decide to use git, but need a refresher, see How To Use Git or Notes on how to use git (if you have access)

Downloading From GitHub Without Git
Periodically download the latest copy from github from the "Downloads" link on the webpage: https://github.com/statgen/fastQValidator/archives/master.
The downloaded tar file is named "statgen-fastQValidator-someHexNumber.tar.gz". The directory created when it is untared shares the same base name. I recommend that you do not change the name of the directory. If you want one called fastQValidator, create a link to this directory. The hex number in the directory name identifies the version of the repository that you downloaded and is necessary to easily troubleshoot any issues you encounter. If you must rename the directory, be sure to record the hex number that was on the download for future reference.
Building

After obtaining the fastQValidator repository (either by download or from github), compile the code using make all. This creates the executable, fastQValidator, in the fastQValidator/bin/ directory, the debug executable in the fastQValidator/bin/debug/ directory, and the profiling executable in the fastQValidator/bin/profile/ directory.
NOTE: you should install the libStatGen package (or just check it out from Git) in order to compile this.
Valid FastQ File Requirements

A valid fastQ file meets the validation criteria specified in FastQ Validation Criteria.

How to Use the fastQValidator Executable

Required Parameters
       --file  :  FastQ filename with path to be processed.
Optional Parameters
       --minReadLen         : Minimum allowed read length (Defaults to 10).
       --maxErrors          : Number of errors to allow before quitting
                              reading/validating the file.
                              -1 (default) indicates to not quit until
                              the entire file is read.
                              0 indicates not to read/validate anything
       --printableErrors    : Maximum number of errors to print before
                              suppressing them (Defaults to 20).
                              Different than maxErrors since 
                              printableErrors will continue reading and
                              validating the file until the end, but
                              just doesn't print the errors.
       --ignoreErrors       : Ignore all errors (same as printableErrors = 0)
                              overwrites the printableErrors option.
       --baseComposition    : Print the Base Composition Statistics.
	--avgQual            : Print the average phred quality per cycle & overall average quality.
--disableSeqIDCheck  : Disable the unique sequence identifier check.
                              Use this option to save memory since the sequence id
                              check uses a lot of memory.
       --params             : Print the parameter settings.
       --quiet              : Suppresses the display of errors and summary statistics.
                              Does not affect the printing of Base Composition Statistics.
Optional Space Options for Raw Sequence (Last one specified is used)
       --auto       : Determine baseSpace/colorSpace from the Raw Sequence in the file (Default).
       --baseSpace  : ACTGN only
       --colorSpace : 0123. only (with 1 character primer base)
Usage
./fastQValidator --file <fileName> [--minReadLen <minReadLen>] [--maxErrors <numErrors>] [--printableErrors <printableErrors>|--ignoreErrors] [--baseComposition] [--disableSeqIDCheck] [--quiet] [--baseSpace|--colorSpace|--auto] [--params]
Examples
       ./fastQValidator --file testFile.txt
       ./fastQValidator --file testFile.txt --minReadLen 10 --baseSpace --printableErrors 100 --params
       ./fastQValidator --file test/testFile.txt --minReadLen 10 --colorSpace --ignoreErrors --disableSeqIDCheck
Return Value
0 - the fastq file is valid.
< 0 - invalid options specified.
> 0 - fastq file did not validate succesfully. One of the FastQStatus failure values is returned
FastQ Validator Output

When running the fastQValidator Executable, if the --params option is specified, the output starts with a summary of the parameters:
The following parameters are available.  Ones with "[]" are in effect:
Input Parameters
 --file [../fastqValidator/test/testFile.txt], --baseComposition,
               --disableSeqIDCheck, --quiet, --params [ON], --minReadLen [10],
               --maxErrors [-1]
  Space Type : --baseSpace, --colorSpace, --auto [ON]
      Errors : --ignoreErrors, --printableErrors [20]
The Validator Executable outputs error messages for invalid sequences based on Validation Criteria. For Example:
ERROR on Line 25: The sequence identifier line was too short.
ERROR on Line 29: First line of a sequence does not begin wtih @
ERROR on Line 33: No Sequence Identifier specified before the comment.
Base Composition Percentages by Index are printed if --printBaseComp is set to ON. For Example:
Base Composition Statistics:
Read Index	%A	%C	%G	%T	%N	Total Reads At Index
        0   100.00    0.00    0.00    0.00    0.00	20
        1     5.00   95.00    0.00    0.00    0.00	20
        2     5.00    0.00    5.00   90.00    0.00	20
Phred Quality by Index are printed if --avgQual is set to ON in a version after May 29, 2012. Only valid qualities are included in these averages. For Example:
Average Phred Quality by Read Index (starts at 0):
Read Index	Average Quality
0	44.10
1	45.55
2	51.11
3	47.68
4	47.37

Overall Average Phred Quality = 50.40

Summary of the number of lines, sequences, and errors:
Finished processing testFile.txt with 92 lines containing 20 sequences.
There were a total of 17 errors.

Libraries & Classes

C++ Library: libStatGen
ParameterList - Class for reading in Parameters.
FastQValidator.cpp - Main method for the Executable.

Additional Features

Base composition reported and tracked by position.
Supports base space and color space files.
Consumes gzipped and uncompressed text files transparently.
Prints error messages for errors up to the configurable maximum number of reportable errors.
Prints a summary of the total number of errors.
Prints the total number of lines processed as well as the total number of sequences processed.
(May 29, 2012) Average Phred Quality can be reported by cycle & overall.

Additional Wishlist - Not Implemented

There are a series of optional capabilities a FastQ Validator could implement. Among those:
To reduce memory usage, implement a two-pass algorithm that stores only a key for each sequence name (rather than complete sequence names) in memory (suggest a pair of options -1 -> one pass, high memory use, -2 -> two pass lower memory use, default is -1).
AutoDetect 64/33 illumina/standard quality scores.
Discussion

For color space, there is no specification for:
The length of read and quality string may be the same or differs by 1 (depending on whether the primer base has a corresponding quality value).
Decided to require a quality score for the primer base.
Missing values are usually presented by "." or sometimes left as a blank " ".
Tag names for paired end reads may be the same (e.g. MAQ actually enforces that), and may be in the same file (e.g. BFAST require paired reads in the same file)
It may be useful to report 2 types of information to the user: ERROR (critical failure) and WARNING (tolerable errors).
