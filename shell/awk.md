1. $0 代表整行 $n 代表第n列 
2. 操作符 ==(相等), ~(正则) 
  ```
  docker ps -a | awk '$2=="go:1.10" {print $1}' | xargs docker rm

  docker ps -a | awk '$2=="go:1.10" && $1 ~ /go/ {print $1}' | xargs docker rm
  ```
3. docker ps | awk '$2 == "go:1.10" {print $1}' | xargs -J % docker exec -it % bash
