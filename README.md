# raft-demo

使用hashicorp/raft库来调试raft，基于go work环境，方便修改库hashicorp/raft

~~~
[dev]$ cat ../../go.work
go 1.19

use (
        ./src/github.com/ent/ent
        ./src/github.com/etcd-io/etcd
        ./src/github.com/hashicorp/raft
        ./src/github.com/hashicorp/raft-boltdb
        ./src/github.com/herrhu97/raft-demo
)
~~~

## Use

编译：
~~~
go build 
~~~

启动node1: 
~~~
./raft-demo --http_addr=127.0.0.1:7001 --raft_addr=127.0.0.1:7000 --raft_id=1 --raft_cluster=1/127.0.0.1:7000,2/127.0.0.1:8000,3/127.0.0.1:9000
~~~

启动node2: 
~~~
./raft-demo --http_addr=127.0.0.1:8001 --raft_addr=127.0.0.1:8000 --raft_id=2 --raft_cluster=1/127.0.0.1:7000,2/127.0.0.1:8000,3/127.0.0.1:9000
~~~

启动node3: 
~~~
./raft-demo --http_addr=127.0.0.1:9001 --raft_addr=127.0.0.1:9000 --raft_id=3 --raft_cluster=1/127.0.0.1:7000,2/127.0.0.1:8000,3/127.0.0.1:9000
~~~

set请求：
~~~
curl "http://127.0.0.1:7001/set?key=test_key&value=test_value"
~~~

get请求：
~~~
curl "http://127.0.0.1:7001/get?key=test_key"
~~~

### Reference
- 基于go vendor调试raft[https://github.com/vision9527/raft-demo]