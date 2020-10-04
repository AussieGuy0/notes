# Linux

## List all ports being used by processes
`sudo netstat -peanut`

## Give information about application using specifed port
`lsof -i :8000`

## Curl

### Multipart file
Assuming we had a file called `file.png` that we wanted to post

`curl -F file=@file.png http://example.com/post-file`
