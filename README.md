# runny
A simple BASH command wrapper to exit on errors and send output to syslog and stderr

## Why
We use Docker for running most of our applications and generally have a `run.sh`
script to bootstrap the startup of the container and run our application. The
default behavior of a BASH script though is if one command fails it moves on
to the next command in the script. If a production environment this may not be
acceptable. Using `runny` to run commands will cause the script to exit if the
command returns a non-zero status code and it will also send the code and output
to syslog.

## Usage

```
$ runny /path/to/command args args args
```

## Examples

```
$ ./runny exit 43
Command exited with non-zero status (43). Output:

$ echo $?
43

$ ./runny aws s3 cp s3://not-found-bucket/file ./here
Command exited with non-zero status (1). Output: fatal error: An error occurred (404) when calling the HeadObject operation: Key "file" does not exist
```
