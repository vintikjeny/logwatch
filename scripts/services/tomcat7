#!/usr/bin/perl

# Detail level
$Detail = $ENV{'LOGWATCH_DETAIL_LEVEL'} || 5;


# total number of errors in log file
my $Total_err = 0;
# hash with only unique errors, where KEY - error message, VALUE - number of errors of this type
my %unique_err = ();
# default value of error message
my $Message = "";
# total number of unique errors
my $Unique_err_num;


# main loop
while (defined($line = <STDIN>)) {
	# use tomcat7 date regex to define start of new message (or end of previous)

	if ($line =~ /^(.*\s+[1-31]+.*(:+[0-9]+[0-9]+){2}\s+(AM|PM)+)/) {
		# if previous collected message - is Error message
		if ($Message =~ /^(ERROR:|SEVERE:)/) {
			# if it is a new message, then add this message to hash
			if (!exists $unique_err{$Message}) {
				$unique_err{$Message} = 0;
			}
			# increment messages counters
			$unique_err{ $Message } = $unique_err{$Message}+1;
			$Total_err++;
		}

		# clear variable from previous message 
		$Message = "";
	# Ignorable strings (java stacktrace)
	} elsif($line =~ /^(.+(at+\s+)|(.*Hint:)|(.*Position:))|((\s+more)$)/) {
		next;
	} else {
		# construct nessesary strings to message
		$Message = $Message.$line;
	}
}

# if log detail level is NOT LOW
if ($Detail != 0) {
	# Print every error in file
	while ( my ($key, $value) = each(%unique_err) ) {
		chomp $key;
		print "Message: $key\nCount: $value\n";
		print "-------------------------------\n";
	}
}

# get total number of unique errors in file
$Unique_err_num = scalar keys %unique_err;

# Print total result
print "Unique errors: $Unique_err_num\n";
print "Total num of Errors: $Total_err\n";

