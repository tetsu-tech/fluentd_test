```bash
~/hoge/fluentd-test % docker run -d --rm --name=http_fluentd -p 9880:9880 -v `pwd`/http.conf:/fluentd/etc/http.conf fluent/fluentd:edge-debian -c /fluentd/etc/http.conf
cc3792f15cc4511577f939fee80cf923eedfa936f14ba5681684e91556d2ea5a
~/hoge/fluentd-test % curl -X POST -d 'json={"json":"message"}' http://127.0.0.1:9880/sample.test
~/hoge/fluentd-test % curl -X POST -d 'json={"json":"message"}' http://127.0.0.1:9880/sample.test
```

<details>
<summary>
コンテナのログを確認
</summary>

```bash
~/hoge/fluentd-test % docker logs http_fluentd
fluentd -c /fluentd/etc/http.conf
2021-04-18 04:14:10 +0000 [info]: parsing config file is succeeded path="/fluentd/etc/http.conf"
2021-04-18 04:14:10 +0000 [info]: gem 'fluentd' version '1.12.2'
2021-04-18 04:14:10 +0000 [warn]: define <match fluent.**> to capture fluentd logs in top level is deprecated. Use <label @FLUENT_LOG> instead
2021-04-18 04:14:10 +0000 [info]: using configuration file: <ROOT>
  <source>
    @type http
    port 9880
    bind "0.0.0.0"
  </source>
  <match **>
    @type stdout
  </match>
</ROOT>
2021-04-18 04:14:10 +0000 [info]: starting fluentd-1.12.2 pid=8 ruby="2.6.6"
2021-04-18 04:14:10 +0000 [info]: spawn command to main:  cmdline=["/usr/local/bin/ruby", "-Eascii-8bit:ascii-8bit", "/usr/local/bundle/bin/fluentd", "-c", "/fluentd/etc/http.conf", "-p", "/fluentd/plugins", "--under-supervisor"]
2021-04-18 04:14:10 +0000 [info]: adding match pattern="**" type="stdout"
2021-04-18 04:14:10 +0000 [info]: adding source type="http"
2021-04-18 04:14:10 +0000 [warn]: #0 define <match fluent.**> to capture fluentd logs in top level is deprecated. Use <label @FLUENT_LOG> instead
2021-04-18 04:14:10 +0000 [info]: #0 starting fluentd worker pid=17 ppid=8 worker=0
2021-04-18 04:14:10 +0000 [info]: #0 fluentd worker is now running worker=0
2021-04-18 04:14:10.830827500 +0000 fluent.info: {"pid":17,"ppid":8,"worker":0,"message":"starting fluentd worker pid=17 ppid=8 worker=0"}
2021-04-18 04:14:10.832301900 +0000 fluent.info: {"worker":0,"message":"fluentd worker is now running worker=0"}


2021-04-18 04:14:19.868264800 +0000 sample.test: {"json":"message"} # ログが出力されている
2021-04-18 04:14:22.337951600 +0000 sample.test: {"json":"message"} # ログが出力されている

```

</details>
