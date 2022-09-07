# Curl Command cheatsheet

```
curl --help                           
Usage: curl [options...] <url>
 -d, --data <data>          HTTP POST data
 -f, --fail                 Fail fast with no output on HTTP errors
 -h, --help <category>      Get help for commands
 -i, --include              Include protocol response headers in the output
 -o, --output <file>        Write to file instead of stdout
 -O, --remote-name          Write output to a file named as the remote file
 -s, --silent               Silent mode
 -T, --upload-file <file>   Transfer local FILE to destination
 -u, --user <user:password> Server user and password
 -A, --user-agent <name>    Send User-Agent <name> to server
 -v, --verbose              Make the operation more talkative
 -V, --version              Show version number and quit
 -X, --request             Specifies a custom request method to use when communicating with the HTTP server
 ```
 
 Inspect headers and output (This can give clues on running software:
 ```
 curl -i http://192.168.208.97/
 ```
 
 Target Post method to URL:
 ```
 curl -X POST http://192.168.120.99:33333/list-running-procs
 ```
 
 If something requires content length in body of post:
 ```
 curl -d "" -X POST http://192.168.120.99:33333/list-running-procs
 ```
